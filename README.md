### Overview
The system is designed to enable an Angular frontend to communicate with a Java backend, which then makes REST API calls to a 3rd party API. The 3rd party API sends its response through an MQ, which the Java backend polls for. After receiving the response, the Java backend persists the data into an Oracle database and processes certain data from the response before sending an email notification. The Java backend also makes three additional REST API calls to a vendor API using OAuth authentication and persists their responses into the Oracle database.

### Components
The system consists of the following components:

### Angular Frontend
The Angular frontend is responsible for sending REST API calls to the Java backend.

### Java Backend
The Java backend is responsible for receiving REST API calls from the Angular frontend and making corresponding REST API calls to the 3rd party API. It also polls the MQ for the response, persists the response data into an Oracle database, processes certain data from the response, sends an email notification, and makes three additional REST API calls to a vendor API using OAuth authentication and persists their responses into the Oracle database.

### Third-party API
The third-party API is responsible for processing requests and sending the response through an MQ.

### IBM MQ (Message Queue)
The IBM MQ is responsible for receiving and storing the response from the third-party API.

### Oracle Database
The Oracle database is responsible for persisting the response data from the 3rd party API and vendor APIs.

### Email Notification
The email notification component is responsible for sending an email notification to a designated recipient after processing certain data from the response.

### OAuth Provider
The OAuth provider is responsible for authenticating and authorizing the Java backend to make REST API calls to the vendor API.

### endor API
The vendor API is responsible for processing requests and sending responses to the Java backend.

### Data Flow
The system follows this data flow:

The Angular frontend sends a REST API call to the Java backend.
The Java backend receives the REST API call and makes corresponding REST API calls to the 3rd party API.
The 3rd party API processes the request and sends the response through an MQ.
The IBM MQ places the response in the queue.
The Java backend polls the IBM MQ for the response.
The Java backend persists the response data into the Oracle database.
The Java backend processes certain data from the response.
The Java backend sends an email notification.
The third-party API receives the poll request and sends the response back to the Java backend.
The Java backend receives the response and makes three additional REST API calls to the vendor API using OAuth authentication.
The vendor API processes the requests and sends responses to the Java backend.
The Java backend persists the responses from the vendor API into the Oracle database.
The Angular frontend receives the response and uses the data or displays the result of the action to the user.
Implementation Details
Angular Frontend
The Angular frontend will be implemented using Angular version 11 or later. It will make REST API calls to the Java backend using the Angular HTTP module.

### Java Backend
The Java backend will be implemented using the Spring Boot framework. It will use the Spring Web module to receive REST API calls from the Angular frontend and make corresponding REST API calls to the 3rd party API. It will use the Spring JMS module to poll the IBM MQ for the response. It will use the Spring Data module to persist the response data into an Oracle database. It will use the JavaMail API to send email notifications. It will use the Spring Security module for OAuth authentication with the OAuth provider.

### Third-party API
The third-party API is responsible for processing requests and sending the response through an MQ.

### IBM MQ
IBM MQ will be used as the messaging middleware to receive and store the response from the third-party API. It will be configured and managed using IBM MQ Explorer.

### Oracle Database
Oracle Database will be used as the database to persist the response data from the 3rd party API and vendor APIs. The database schema will be designed and implemented using Oracle SQL Developer. The database will be hosted on an Oracle Database Server.

### Email Notification
The email notification component will use the JavaMail API to send an email notification to a designated recipient after processing certain data from the response. The email server will be hosted by a third-party email service provider.

### OAuth Provider
The OAuth provider will be used to authenticate and authorize the Java backend to make REST API calls to the vendor API. The provider will be configured and managed using its respective provider management console.

### Vendor API
The vendor API will be implemented using RESTful architecture and OAuth2 authentication. The API will be hosted by the vendor and will require authentication and authorization to access the resources.

### Security Considerations
The system will implement the following security measures:

Authentication and authorization will be implemented using OAuth2 for the vendor API and the OAuth provider.
HTTPS will be used for all REST API calls.
The Java backend will implement input validation and output encoding to prevent SQL injection attacks and other vulnerabilities.
Access to the Oracle database will be restricted to authorized personnel only.
Access to the email server will be restricted to authorized personnel only.
Deployment Diagram
The deployment diagram shows the deployment architecture of the system:

      +------------------------------------+
      |          Angular Frontend           |
      +------------------------------------+
                          |
                 REST API Calls
                          |
                          v
      +------------------------------------+
      |            Java Backend             |
      +------------------------------------+
                 |              |
            REST API Calls     JMS Poll
                 |              |
                 v              v
      +------------------------+--------+
      |          Third-party API           |
      +------------------------------------+
                          |
                     MQ Response
                          |
                          v
      +------------------------------------+
      |              IBM MQ                |
      +------------------------------------+
                          |
                     JMS Poll
                          |
                          v
      +------------------------------------+
      |            Oracle DBMS              |
      +------------------------------------+
                          |
                     JDBC Query
                          |
                          v
      +------------------------------------+
      |          Email Notification         |
      +------------------------------------+
                          |
                 Email Notification
                          |
                          v
      +------------------------------------+
      |            OAuth Provider           |
      +------------------------------------+
                          |
                OAuth2 Authentication
                          |
                          v
      +------------------------------------+
      |             Vendor API              |
      +------------------------------------+
                          |
                 RESTful Response
                          |
                          v
      +------------------------------------+
      |            Oracle DBMS              |
      +------------------------------------+

### Conclusion
The system is designed to enable an Angular frontend to communicate with a Java backend, which then makes REST API calls to a 3rd party API. After processing the response, the Java backend makes three additional REST API calls to a vendor API using OAuth authentication and persists their responses into the Oracle database. The system is secure, reliable, and scalable, with each component designed to perform its respective function effectively.
