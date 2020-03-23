# Useful

# Keyboard:

   ```swift 
   override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        self.view.endEditing(true)
    }
   ```
  
# IQKeyboardManager

IQKeyboardManager (Swift): IQKeyboardManagerSwift is available through CocoaPods. To install it, simply add the following line to your Podfile: (#236)

Swift 5.1, 5.0, 4.2, 4.0, 3.2, 3.0 (Xcode 11)

```swift
pod 'IQKeyboardManagerSwift'
```

In AppDelegate.swift, just import IQKeyboardManagerSwift framework and enable IQKeyboardManager.
```swift import IQKeyboardManagerSwift

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

      IQKeyboardManager.shared.enable = true

      return true
    }
}
```

# Defaults
```swift
final class Defaults {
    static let current = Defaults()

    private static let authTokenKey = "current_token"
    private static let currencyKey = "currency"
    private static let accountKey = "organisation"
    private static let playerIdKey = "playerId"
    private static let shiftHoursKey = "shiftHours"
    private static let billingKey = "billing"

    var playerId: String? {
        get {
            if let playerId = UserDefaults.standard.object(forKey: Defaults.playerIdKey) as? String {
                return playerId
            }
            return .none
        } set {
            saveToDefaults(newValue: newValue, forKey: Defaults.playerIdKey)
        }
    }

    var authToken: String? {
        get {
            if let token = UserDefaults.standard.object(forKey: Defaults.authTokenKey) as? String {
                return token
            }
            return .none
        } set {
            saveToDefaults(newValue: newValue, forKey: Defaults.authTokenKey)
        }
    }

    var currency: Currency? {
        get {
            if let data = UserDefaults.standard.object(forKey: Defaults.currencyKey) as? Data {
                if let currency = NSKeyedUnarchiver.unarchiveObject(with: data) as? Currency {
                    return currency
                } else {
                    return .none
                }
            } else {
                return .none
            }
        } set {
            if let currency = newValue {
                UserDefaults.standard.set(NSKeyedArchiver.archivedData(withRootObject: currency), forKey: Defaults.currencyKey)
            } else {
                UserDefaults.standard.removeObject(forKey: Defaults.currencyKey)
            }
            UserDefaults.standard.synchronize()
        }
    }

    var organisation: Account? {
        get {
            if let data = UserDefaults.standard.object(forKey: Defaults.accountKey) as? Data {
                if let account = NSKeyedUnarchiver.unarchiveObject(with: data) as? Account {
                    return account
                } else {
                    return .none
                }
            } else {
                return .none
            }
        } set {
            if let organisation = newValue {
                UserDefaults.standard.set(NSKeyedArchiver.archivedData(withRootObject: organisation), forKey: Defaults.accountKey)
            } else {
                UserDefaults.standard.removeObject(forKey: Defaults.accountKey)
            }
            UserDefaults.standard.synchronize()
        }
    }

    var hoursShift: Int {
        get {
            if let hours = UserDefaults.standard.value(forKey: Defaults.shiftHoursKey) as? Int {
                return hours
            }
            return 0
        } set {
            saveToDefaults(newValue: newValue, forKey: Defaults.shiftHoursKey)
        }
    }

    var billingInfo: BillingInfo? {
        get {
            if let data = UserDefaults.standard.object(forKey: Defaults.billingKey) as? Data {
                if let billing = NSKeyedUnarchiver.unarchiveObject(with: data) as? BillingInfo {
                    return billing
                } else {
                    return .none
                }
            } else {
                return .none
            }
        } set {
            NotificationService.sendBillingnfoNotification()
            if let billing = newValue {
                UserDefaults.standard.set(NSKeyedArchiver.archivedData(withRootObject: billing), forKey: Defaults.billingKey)
            } else {
                UserDefaults.standard.removeObject(forKey: Defaults.billingKey)
            }
            UserDefaults.standard.synchronize()
        }
    }
}

func saveToDefaults(newValue: Any?, forKey: String) {
    if newValue != nil {
        UserDefaults.standard.set(newValue!, forKey: forKey)
        UserDefaults.standard.synchronize()
    }
}
```
