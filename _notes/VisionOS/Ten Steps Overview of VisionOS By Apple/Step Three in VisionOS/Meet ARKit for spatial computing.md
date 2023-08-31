---
title: Meet ARKit for spatial computing
---

### [Meet ARKit for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10082/)

This video provides several key tips on creating SwiftUI ARKit for visionOS, specfically Hand Tracking and Scene Geometry. Placing object into the real world, that you can interact with using hands.

#### Overview 2:30

- Available in Swift and C
- Use any combination of features together
- Privacy-first design for secure access to data
- 3 Components
    - Anchors
        - Position and orientation in real world
    - DataProvider
        - Observe data like anchor changes
    - ARKitSession
        - A set of data providers 
- Privacy
    - Daemon filters data before reaching app
    - Full space 
    - Authoritized 
```swift
// Privacy
// Authorization

session = ARKitSession()

Task {
    let authorizationResult = await session.requestAuthorization(for: [.handTracking])

    for (authorizationType, authorizationStatus) in authorizationResult {
        print("Authorization status for \(authorizationType): \(authorizationStatus)")

        switch authorizationStatus {
        case .allowed:
            // All good!
            break
        case .denied:
            // Need to handle this.
            break
        ...
        }
    }
}
```

#### World Tracking 5:30

- Allow anchor object into real world
    - WorldTrackingProviders
        - Add WorldAnchors for anchoring virtual content
            - WorldAnchor Origin used to hold vitrual content in place
        - Automatic Persistance
            - location is saved along with World Anchor
        - Get the device's pose relative to the app's origin
            - Position and orientation of the device relative to the app's origin
            - Primarily targeted at developers doing their own rendering
            - Querying for the pose is a relatively expensive operation
            - For more see 
                - [Discover Metal for immersive apps](https://developer.apple.com/videos/play/wwdc2023/10089)
                - [Optimize app power and performance for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10100)

#### Scene Understanding 11:50

- Inform you about your surroundings
    - Plane Detection
        - PlaneDetectionProvider
        - Each plane is provided as a PlaneAnchor
        - Useful for content placement or low-fidelity physics simulations
        - PlaneAnchor
            - alignment: oriention of plane, horizontal or veritical
            - geometry: dimensions of plane
            - classification: type of plane, .wall, .floor, .ceiling, .table, .seat, .window, .door
    - Scene Geometry
        - Polygonial mesh the represents the real world
        - SceneReconstructionProvider
            - Mesh geometry is provided as MeshAnchors
            - Useful for content placement or high-fidelity physics simulations
                - geometry
                    - vertices
                    - normals
                    - faces
                    - classifications
                        - .wall, .floor, .ceiling, .table, .seat, .window, .door, .stairs, .bed, .cabinet, .homeAppliance, .tv, .plant
    - Image Tracking
        - Detection 2D images in real world
        - ImageTrackingProvider
            - Specify a set of ReferenceImages to detect
                - loadReferenceImages
                - CGImage 
                - PixelBuffer
            - Detect images are provided as ImageAnchors
                - estimatedScaleFactor: size of image compares to specified physical size
                - referenceImage 
            -Useful for placing content at known, statically placed images
                - information next to a movie poster.

#### Hand Tracking 15:22

- Skeletal data for your hands
    - HandTrackingAnchor is a trackable anchor
        - skeleton:
            - joint
                - parentJoint
                - name
                - localTransform: relative to parent joint
                - rootTransform: relative to root joint
                - isTracked
        - chirality: left hand or right hand
        - transform: wrist transform relative to app
        - ![](https://hackmd.io/_uploads/SJVK5h9n2.png)
- Each hand is provided as a HandAnchor
- Useful for content placement or detecting custom gestures
- Poll for latest handAnchors or receive HandAnchors when updates are available

#### Example 18:00

- App and view model
```swift 
// App

@main
struct TimeForCube: App {
   @StateObject var model = TimeForCubeViewModel()

    var body: some SwiftUI.Scene {
        ImmersiveSpace {
            RealityView { content in
                content.add(model.setupContentEntity())
            }
            .task {
                await model.runSession()
            }
            .task {
                await model.processHandUpdates()
            }
            .task {
                await model.processReconstructionUpdates()
            }
            .gesture(SpatialTapGesture().targetedToAnyEntity().onEnded({ value in
                let location3D = value.convert(value.location3D, from: .global, to: .scene)
                model.addCube(tapLocation: location3D)
            }))
        }
    }
}
```
```swift 
// View model

@MainActor class TimeForCubeViewModel: ObservableObject {
    private let session = ARKitSession()
    private let handTracking = HandTrackingProvider()
    private let sceneReconstruction = SceneReconstructionProvider()

    private var contentEntity = Entity()

    private var meshEntities = [UUID: ModelEntity]()

    private let fingerEntities: [HandAnchor.Chirality: ModelEntity] = [
        .left: .createFingertip(),
        .right: .createFingertip()
    ]

    func setupContentEntity() { ... }

    func runSession() async { ... }

    func processHandUpdates() async { ... }

    func processReconstructionUpdates() async { ... }

    func addCube(tapLocation: SIMD3<Float>) { ... }
}
```
- Session initialization
    - runSession()
- Hand colliders
    - process Hand Updates
```swift 
class TimeForCubeViewModel: ObservableObject {
    ...
    private let fingerEntities: [HandAnchor.Chirality: ModelEntity] = [
        .left: .createFingertip(),
        .right: .createFingertip()
    ]

    ...
    func processHandUpdates() async {
        for await update in handTracking.anchorUpdates {
            let handAnchor = update.anchor

            guard handAnchor.isTracked else { continue }

            let fingertip = handAnchor.skeleton.joint(named: .handIndexFingerTip)

            guard fingertip.isTracked else { continue }

            let originFromWrist = handAnchor.transform
            let wristFromIndex = fingertip.rootTransform
            let originFromIndex = originFromWrist * wristFromIndex

            fingerEntities[handAnchor.chirality]?.setTransformMatrix(originFromIndex,             relativeTo: nil)
        }
```
- Scene colliders

```swift 
func processReconstructionUpdates() async {
        for await update in sceneReconstruction.anchorUpdates {
            let meshAnchor = update.anchor
            
            guard let shape = try? await ShapeResource.generateStaticMesh(from: meshAnchor)             else { continue }
            
            switch update.event {
            case .added:
                let entity = ModelEntity()
                entity.transform = Transform(matrix: meshAnchor.transform)
                entity.collision = CollisionComponent(shapes: [shape], isStatic: true)
                entity.physicsBody = PhysicsBodyComponent()
                entity.components.set(InputTargetComponent())

                meshEntities[meshAnchor.id] = entity
                contentEntity.addChild(entity)
            case .updated:
                guard let entity = meshEntities[meshAnchor.id] else { fatalError("...") }
                entity.transform = Transform(matrix: meshAnchor.transform)
                entity.collision?.shapes = [shape]
            case .removed:
                meshEntities[meshAnchor.id]?.removeFromParent()
                meshEntities.removeValue(forKey: meshAnchor.id)
            @unknown default:
                fatalError("Unsupported anchor event")
            }
        }
    }
```
- Cubes
```swift 
class TimeForCubeViewModel: ObservableObject {
    func addCube(tapLocation: SIMD3<Float>) {
        let placementLocation = tapLocation + SIMD3<Float>(0, 0.2, 0)

        let entity = ModelEntity(
            mesh: .generateBox(size: 0.1, cornerRadius: 0.0),
            materials: [SimpleMaterial(color: .systemPink, isMetallic: false)],
            collisionShape: .generateBox(size: SIMD3<Float>(repeating: 0.1)),
            mass: 1.0)

        entity.setPosition(placementLocation, relativeTo: nil)
        entity.components.set(InputTargetComponent(allowedInputTypes: .indirect))

        let material = PhysicsMaterialResource.generate(friction: 0.8, restitution: 0.0)
        entity.components.set(PhysicsBodyComponent(shapes: entity.collision!.shapes,
                                                   mass: 1.0,
                                                   material: material,
                                                   mode: .dynamic))

        contentEntity.addChild(entity)
    }
}
```
