---
title: Swift Framework CoreData
---

### Main Idea
First, the basics: Core Data is an object graph and persistence framework, which is a fancy way of saying it lets us define objects and properties of those objects, then lets us read and write them from permanent storage.

On the surface this sounds like using Codable and UserDefaults, but it’s much more advanced than that: Core Data is capable of sorting and filtering of our data, and can work with much larger data – there’s effectively no limit to how much data it can store. Even better, Core Data implements all sorts of more advanced functionality for when you really need to lean on it: data validation, lazy loading of data, undo and redo, and much more.


```swift
// Follow instructions here: https://www.hackingwithswift.com/books/ios-swiftui/how-to-combine-core-data-and-swiftui

// Create a file called Bookworm.xcdatamodel and create a student class with name and id

// Create DataController as an ObservableObject as it needs to be passed around via a Environment PropertyWrapper

import CoreData
import Foundation

class DataController: ObservableObject {
    // create a container with class NSPersistentContainer, which is the Core Data type responsible for loading a data model and giving us access to the data inside
    let container = NSPersistentContainer(name: "Bookworm")
    
    init() {
        // To actually load the data model we need to call loadPersistentStores() on our container, which tells Core Data to access our saved data according to the data model in Bookworm.xcdatamodeld.
        container.loadPersistentStores { description, error in
            if let error = error {
                print("Core Data failed to load: \(error.localizedDescription)")
            }
        }
    }
}



// creates our data controller, and now we can place it into SwiftUI’s environment by adding a new modifier to the ContentView() line:
@main
struct BookwormApp: App {
    @StateObject private var dataController = DataController()
    
    var body: some Scene {
        WindowGroup {
            ContentView()
                .environment(\.managedObjectContext, dataController.container.viewContext)
        }
    }
}



struct ContentView: View {
    // Get the managedObjectContext from the environment
    @Environment(\.managedObjectContext) var moc
    
    // Retrieving information from Core Data is done using a fetch request – we describe what we want, how it should sorted, and whether any filters should be used, and Core Data sends back all the matching data. We need to make sure that this fetch request stays up to date over time, so that as students are created or removed our UI stays synchronized.
    @FetchRequest(sortDescriptors: []) var students: FetchedResults<Student>
    
    var body: some View {
    VStack {
        List(students) { student in
            Text(student.name ?? "Unknown")
        }
        
        Button("Add") {
            let firstNames = ["Ginny", "Harry", "Hermione", "Luna", "Ron"]
            let lastNames = ["Granger", "Lovegood", "Potter", "Weasley"]
            
            let chosenFirstName = firstNames.randomElement()!
            let chosenLastName = lastNames.randomElement()!
            
            // Create student from managedObjectContext 
            let student = Student(context: moc)
            student.id = UUID()
            student.name = "\(chosenFirstName) \(chosenLastName)"
            
            // Save new data in to our dataController via the managedObjectContext
            try? moc.save()
            
        }
    }
}

```

(Create your own NSManaged Class )[https://www.hackingwithswift.com/books/ios-swiftui/creating-nsmanagedobject-subclasses]

(Check changes before saving)[https://www.hackingwithswift.com/books/ios-swiftui/conditional-saving-of-nsmanagedobjectcontext]

```swift
if moc.hasChanges {
    try? moc.save()
}
```

(Unique Core Data)[https://www.hackingwithswift.com/books/ios-swiftui/ensuring-core-data-objects-are-unique-using-constraints]


```swift
class DataController: ObservableObject {
    let container = NSPersistentContainer(name: "CoreDataProject")
    
    init() {
        container.loadPersistentStores { description, error in
            if let error = error {
                print("Core Data failed to load: \(error.localizedDescription)")
            }
            
            self.container.viewContext.mergePolicy = NSMergePolicy.mergeByPropertyObjectTrump
        }
    }
}

```

(Filter Fetch Results with NSPredicate)[https://www.hackingwithswift.com/books/ios-swiftui/filtering-fetchrequest-using-nspredicate]


```swift
    @FetchRequest(sortDescriptors: [], predicate: NSPredicate(format:"universe IN %@", ["Aliens", "Firefly", "Star Trek"])) var ships: FetchedResults<Ship>
```

(dynamically filtering @FetchRequest)[https://www.hackingwithswift.com/books/ios-swiftui/dynamically-filtering-fetchrequest-with-swiftui]

(one-many relationship)[https://www.hackingwithswift.com/books/ios-swiftui/one-to-many-relationships-with-core-data-swiftui-and-fetchrequest]

(Sorting Fetch Request with SortDescriptor)[https://www.hackingwithswift.com/books/ios-swiftui/sorting-fetch-requests-with-sortdescriptor]
