# Useful

# Keyboard:

    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        self.view.endEditing(true)
    }
  
  
# IQKeyboardManager

IQKeyboardManager (Swift): IQKeyboardManagerSwift is available through CocoaPods. To install it, simply add the following line to your Podfile: (#236)

Swift 5.1, 5.0, 4.2, 4.0, 3.2, 3.0 (Xcode 11)

`pod 'IQKeyboardManagerSwift'`

In AppDelegate.swift, just import IQKeyboardManagerSwift framework and enable IQKeyboardManager.

   import IQKeyboardManagerSwift

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

      IQKeyboardManager.shared.enable = true

      return true
    }
}
