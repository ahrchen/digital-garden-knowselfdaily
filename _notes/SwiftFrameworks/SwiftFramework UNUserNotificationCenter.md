---
title: Swift Framework UNUserNotificationCenter
---

### Main Idea
Use UNCalendarNotificationTrigger + UNUserNotificationCenter to create repeated notifications. 

Note: This bypasses the need to get the .weekdays, .hours, and .minutes  from a specific date, allowing for reminder notifications without knowing the specific date. 

see site for more specific examples- https://www.reddit.com/r/iOSProgramming/comments/rd4lzj/how_is_it_possible_to_create_highly_customised/

Example
```swift
var dateComponents = DateComponents()
dateComponents.calendar = Calendar.current

//
// Repeat every Monday, 3:00 AM
//
dateComponents.weekday = 2

dateComponents.hour = 3
dateComponents.minute = 0

let trigger = UNCalendarNotificationTrigger(
    dateMatching: dateComponents,
    repeats: true
)
```

Use Case
```swift
public struct NotificationHelper: Codable, Hashable {
    static let secondsInMinute = 60.0
    static let minutesInHour = 60.0
    static let hoursInDays = 24.0

    static func scheduleNotifications(notificationTimer: NotificationTimer, saveIdentifier: (String) -> ()) {
        let calendar = Calendar.current
        let year = Calendar.current.component(.year, from: Date())
        for weekday in notificationTimer.weekdays {
            let startHour = calendar.component(.hour, from: notificationTimer.start)
            let startMinutes = calendar.component(.minute, from: notificationTimer.start)
            let endHour = calendar.component(.hour, from: notificationTimer.end)
            let endMinutes = calendar.component(.minute, from: notificationTimer.end)
            let startTime = startHour * Int(NotificationHelper.minutesInHour) + startMinutes
            let endTime = endHour * Int(NotificationHelper.minutesInHour) + endMinutes
            
            let intervalTime = notificationTimer.intervalHours * Int(self.minutesInHour) + notificationTimer.intervalMinutes
            for minutes in stride(from: startTime, through: endTime, by: intervalTime) {
                let hour = (minutes / Int(minutesInHour))
                let minute = (minutes % Int(minutesInHour))
                let trigger = createTrigger(weekday: weekday, hour: hour, minute: minute, year: year)
                let identifier = UUID().uuidString
                addNotification(at: trigger, body: notificationTimer.body, title: notificationTimer.title, identifier: identifier)
                saveIdentifier(identifier)
            }
            
        }
    }
    
    
    static private func createTrigger(weekday: Weekday, hour: Int, minute: Int, year: Int)-> UNCalendarNotificationTrigger {
        var components = DateComponents()
        components.hour = hour
        components.minute = minute
        components.weekday = weekday.rawValue
        components.timeZone = .current
        let trigger = UNCalendarNotificationTrigger(
            dateMatching: components,
            repeats: true
        )
        return trigger
    }
    
    static private func addNotification(at trigger: UNCalendarNotificationTrigger, body: String, title: String, identifier: String) {
        let center = UNUserNotificationCenter.current()
        
        let addRequest = {
            let content = UNMutableNotificationContent()
            content.title = title
            content.subtitle = body
            content.sound = UNNotificationSound.default
            content.interruptionLevel = .timeSensitive
            let request = UNNotificationRequest(identifier: identifier, content: content, trigger: trigger)
            center.add(request) { error in
                guard let error = error else { return }
                print("Error: \(error)")
            }
        }
        
        center.getNotificationSettings { settings in
            if settings.authorizationStatus == .authorized {
                addRequest()
                
            } else {
                center.requestAuthorization(options: [.alert,.badge,.sound]) { success, error in
                    if success {
                        addRequest()
                    } else {
                        print("D'oh")
                    }
                }
            }
            
        }
    }
