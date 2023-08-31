---
title: Explore rendering for spatial computing
---

### [Explore rendering for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10095/)

The next step Apple suggest is to learn about the tools, learn to use Reality kit to render a  improved look and feel of your apps. 

"Find out how you can take control of RealityKit rendering to improve the look and feel of your apps and games on visionOS. Discover how you can customize lighting, add grounding shadows, and control tone mapping for your content. We'll also go over best practices for two key treatments on the platform: rasterization rate maps and dynamic content scaling." -Apple

#### Lighting and shadows
- Image based lighting
    - Environment probe texture
    - System IBL texture
        - Adds extra highlights
    - Combined together for IBL texture

```swift 
RealityView { content in
    async let satellite = Entity(named: "Satellite", in: worldAssetsBundle)
    async let environment = EnvironmentResource(named: "Sunlight")

    if let satellite = try? await satellite, let environment = try? await environment {
        content.add(satellite)

        satellite.components.set(ImageBasedLightComponent(
           source: .single(environment)))

        satellite.components.set(ImageBasedLightReceiverComponent(
           imageBasedLight: satellite))
   }
}
```
- Shadow: Clear demonstrate position of item in space

```swift
RealityView { content in
    if let vase = try? await Entity(named: "flower_tulip") {
        content.add(vase)

        vase.components.set(GroundingShadowComponent(castsShadow: true))
    }
} 
```

#### Material
- PhysicallyBasedMaterial 
    - Reacts to lighting 
- SimpleMaterial
    - lesser reaction to lighting
    - quick experiment
- UnlitMaterial
    - No lighting reaction
- VideoMaterial
    - UnlitMaterial that maps video on top
- ShaderGraphMaterial
    - Learn more in [Explore materials in Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10202) 
- Tone Mapping
    - Enabled by deault in RealityKit
    - Allow more natural perceived colors
        - Re-mapping values above 1 int ovisible range
        
    - Disable Tone Mapping to match SwiftUI color
    
```swift
RealityView { content in
    if let trafficLight = try? await Entity(named: "traffic_light") {
        content.add(trafficLight)

        if let lamp = trafficLight.findEntity(named: "red_light") {
            if var model = lamp.components[ModelComponent.self] {
                let material = UnlitMaterial(color: .init(color), 
                                             applyPostProcessToneMap: false)

                model.materials = [material]

                lamp.components[ModelComponent.self] = model
            }
        }
    }
}
```

#### Rasterization rate maps
- Lower detailed assets are needed when objects are far away from users focal point, in order to reduce flickering. Lower detailed assets can make due with less cpu and gpu time.
    - For more see [Rendering at Different Rasterization Rates](https://developer.apple.com/documentation/metal/render_passes/rendering_at_different_rasterization_rates)


#### Dynamic content scaling

<img src="/assets/RasterizationRateMaps.png"/>

- To draw content at the right scale. 
    - Text label are scaled to different size
        - largest in the center
        - Middle nearby center
        - smallest outside center
- UIKit, SwiftUI auto enabled
- CoreAnimation Available

```swift
// Enable dynamic content scaling on CALayer with:

var wantsDynamicContentScaling: Bool { get set }
```
