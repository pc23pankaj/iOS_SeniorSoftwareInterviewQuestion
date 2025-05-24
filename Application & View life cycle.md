# 📱 Application Life Cycle

| **Phase**        | **UIKit** (AppDelegate / SceneDelegate)                             | **SwiftUI** (App protocol)                               |
| ---------------- | ------------------------------------------------------------------- | -------------------------------------------------------- |
| App Launch       | `application(_:didFinishLaunchingWithOptions:)`                     | `@main` struct conforming to `App`                       |
| Scene Connection | `scene(_:willConnectTo:options:)`                                   | `WindowGroup` scene in `App` struct                      |
| Become Active    | `applicationDidBecomeActive(_:)` / `sceneDidBecomeActive(_:)`       | Use `@Environment(\.scenePhase)` with `.active`          |
| Enter Background | `applicationDidEnterBackground(_:)` / `sceneDidEnterBackground(_:)` | `@Environment(\.scenePhase)` with `.background`          |
| Terminate        | `applicationWillTerminate(_:)`                                      | No direct method, use scene phase or `onDisappear` logic |


# 🧩 View Life Cycle

| **Phase**     | **UIKit (UIViewController)**                           | **SwiftUI (View)**                                     |
| ------------- | ------------------------------------------------------ | ------------------------------------------------------ |
| View Loaded   | `viewDidLoad()`                                        | No direct equivalent (use `onAppear {}`)               |
| Appeared      | `viewWillAppear()` / `viewDidAppear()`                 | `onAppear {}`                                          |
| Disappeared   | `viewWillDisappear()` / `viewDidDisappear()`           | `onDisappear {}`                                       |
| Layout Change | `viewWillLayoutSubviews()` / `viewDidLayoutSubviews()` | No direct equivalent; rely on `GeometryReader`         |
| Deinit        | `deinit {}` in `UIViewController`                      | Use `onDisappear {}` or `deinit` in `ObservableObject` |



**🔑 Summary**
- UIKit uses AppDelegate, SceneDelegate, and UIViewController methods.
- SwiftUI uses declarative lifecycle with App, Scene, @Environment, and onAppear/onDisappear.
