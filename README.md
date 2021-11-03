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
* Data Storage- ER Diagram- Sagar  
  ![ER Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/er/diagram.png)
* UI Mockups/Sketches- Vimal- Login, Registration, User Dashboard, Admin Dashboard, User profile, User update
* User Interactions- 3 Sequence Diagrams- Vimal- Registration, Notification, Subscribe
* Class Diagram- 1 or 2 Class Diagrams (RPi and Server)- Sagar  
  ![Class Diagram](https://github.com/ooad-sv/semester-project-design/blob/main/diagrams/class/diagram.png)
  * Patterns:
    * Observer- user and station
    * State- Station enabled/disabled
    * Object Pool- DB connections
    * MVC- Everything tied together
    * Composite- HTML DOM