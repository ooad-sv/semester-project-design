# semester-project-design

## Deliverables
* Project Summary- Vimal
* Requirements- Sagar
  * 2 types of notifications
    * Regular interval updates
    * Uncomfortable value updates
  * Registration inputs
    * Basic info
      * First name
      * last name
      * email
      * password
    * Manage subscription
      * weather station subscriptions
    * Manage notifications
      * notification preference for regular interval updates- yes/no
      * regular interval- like 2h, 6h, etc.
      * notification preference for uncomfortable value updates- yes/no
      * comfortable ranges- 8 inputs- min/max for all 4
  * User update profile- everything can be updated except email
* Use Cases- Use Case Diagram- Sagar  
  ![Use Case Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/use-case/diagram.png)
* Activity or State Diagram- Activity- Vimal- Registration
* Architecture Diagram- Sagar
  ![Architecture Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/architecture/diagram.png)
* Data Storage- ER Diagram- Sagar  
  ![ER Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/er/diagram.png)
* UI Mockups/Sketches- Vimal- Login, Registration, User Dashboard, Admin Dashboard, User profile, User update
* User Interactions- 3 Sequence Diagrams- Vimal- Registration, Notification, Subscribe
  * Registration
    * User -> WebServer : Enter all registration details
    * Webserver -> Database : Check user with email
    * Database -> Webserver : yes/no
    * Webserver -> User : User with email already exits/continue
    * Webserver -> Database : Create user
    * Webserver -> Database : Update user station subscriptions
    * Webserver -> Database : Update user notification preferences
    * Webserver -> User : Created user
  * Alarm Notification
    * Sensor -> Station : Updated value
    * Station -> WebServer : Updated value
    * WebServer -> Database : Updated value
    * WebServer -> Database : Get subscribed users
    * -> return data
    * WebServer -> Database : Get user alarm ranges
    * -> return data
    * WebServer -> User : Notify
  * Update subscriptions
    * User -> WebServer : Updated subscription preferences
    * WebServer -> Database : Update user station subscriptions
    * -> return Updated!
* Class Diagram- Sagar  
  ![Class Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/class/diagram.png)
  * Patterns:
    * `Observer`: The `User` class implements the `Observer` interface. The `Station` class implements the `Publisher` interface and stores references to the `Observer` interface and implements `attachObserver`, `detachObserver` and `notify` methods. The station class has two other notify methods named `intervalNotify` and `alarmNotify`, which internally call the same `notify` method.
    * `State`: The `Station` class stores a reference to the `State` interface which stores its state. Concrete classes `EnabledState` and `DisabledState` implement the `State` interface and override the `intervalNotify`, `alarmNotify`, `enable` and `disable` methods.
    * `Object Pool`: We are using Node.js for the web server and PostgreSQL for the database. The `WebServer` will get an instance of the `DBConnectionPool` using the `getInstance` method. It will get an instance of `ReusableConnection` using the `acquireReusable` method and later release it using the `releaseReusable` method.
    * `MVC`: We are using Node.js for the web server along with the Express.js framework. We're applying the `MVC` pattern where user interacts with the `View`, `Controller` changes the `Model` state and renders the `View` and `Model` updates the `View`. For example, a webpage for displaying user information will involve `UserModel` to store the user information, `UserView` to display it and `UserController` to update the state and render the `UserView`.
    * `Composite`: We are using HTML to display the web UI. The DOM tree in HTML is a good example of the `Composite` pattern. Each element in the DOM tree implements the `HTMLComponent` interface. An element can either be an `HTMLComposite`, which further contains more elements, or it could be an `HTMLLeaf`, the leaf of that tree node. Both `HTMLLeaf` and `HTMLComposite` implement the `HTMLComponent` interface.