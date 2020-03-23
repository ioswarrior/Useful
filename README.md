# Useful

# Keyboard:

override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
    self.view.endEditing(true)
}
  
  
# IQKeyboardManager

# Pods:
pod 'IQKeyboardManager' #iOS8 and later
pod 'IQKeyboardManagerSwift'

# Code:
import IQKeyboardManagerSwift

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

      IQKeyboardManager.shared().isEnabled = true

      return true
    }
}
