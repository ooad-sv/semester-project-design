# semester-project-design

## Deliverables
* Project Summary- Vimal
  * Title: Weather Monitoring System
  * Team: Sagar Pathare and Vimal Kakaraparthi
  * Overview: TODO
* Requirements- Sagar
  * Functional requirements
    * System
      * We propose a Weather Monitoring System which monitors the weather at multiple locations and sends notifications about weather to the users.
      * The system will consist of weather stations based on Raspberry Pi and a web server that manages the stations and sends the notifications.
      * Each weather station will measure temperature, pressure, humidity, and altitude values using multiple sensors connected to the Raspberry Pi.
      * These values are hereafter referred to as 'weather values' and will be sent to the web server, which will update them in the database and notify users as required. Users can also view these values from their dashboard.
      * A web UI will be provided for the end users.  
    * Notifications
      * There are two types of notifications sent by the system- Interval notifications and Alarm notifications
      * User can enable or disable each type of notification he wants to receive.
      * Interval notifications are sent to the users in fixed time intervals, like every 4 or 6 hours. This interval is accepted as user input during registration and can be updated at any point.
      * Alarm notifications are sent to the users when the weather station values are in the alarm ranges. Minimum and maximum values for the weather values are accepted from the user during registration and can be updated at any point.
      * Notifications will be sent to the user via email to the email address he used during the registration. We will use a third-party email service to achieve this.
    * End Users
      * There are two types of end-users- Admin and User.
      * Admin will be responsible for managing the state of the weather stations. He can enable or disable them. There will be only one admin in the system.
      * User can register using the web UI. User will provide the following information during registration-
        * Name
        * Email
        * Password
        * Weather stations he wants to subscribe to
        * Enable interval notifications? If yes, time interval
        * Enable alarm notifications? If yes, minimum and maximum values for the weather values
      * User can subscribe to zero to many weather stations.
      * User can see the list of the weather stations he's subscribed to on his dashboard after login, along with their weather values.
      * User can update his profile data, subscription, and notification preferences at any point except for email.
  * Interface requirements
    * A web UI will be provided for the end users.
    * Hardware requirements
      * We're implementing the weather station using a Raspberry Pi 4
      * Sensor X to measure temperature
      * Sensor Y to measure humidity
      * Sensor Z to measure pressure and altitude
    * Software requirements
      * Node.js with Express.js for the web server
      * PostgreSQL for the database
      * Third-party service like Gmail or Yandex for the email notifications 
  * Non-functional requirements
    * Scalability
      * More weather sensors to measure wind speed, rainfall, etc., can be added to each weather station if needed.
      * Currently, we plan to have 4 weather stations in the system for this project, and so the system is not designed to handle a large number of weather stations with a large number of users subscribed to them. However, the system can be made scalable using more advanced technologies.
    * Security
      * We plan to implement basic user authentication using email and password. A sophisticated authentication system can be implemented if needed, but it's beyond this project's scope.
    * Reliability
      * The timely delivery of emails depends on the reliability of the third-party email service we will use.
 
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