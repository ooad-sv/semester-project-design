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
    * Observer- user and station
    * State- Station enabled/disabled
    * Object Pool- DB connections
    * MVC- Everything tied together
    * Composite- HTML DOM