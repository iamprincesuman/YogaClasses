
## Yoga Admission System

### Description

This repository contains the code for a Yoga Admission System, which includes a client-side application and a server-side application. The system allows users to enroll in yoga classes, change their batch timings, and make monthly payments.




### Technologies Used
    Client-Side: HTML, CSS, JavaScript, Fetch API

    Server-Side: Node.js, Express, MySQL
    

### Installation

Follow these steps to install and run the Yoga Admission System project

##### Clone the Repository :
```bash
  git clone https://github.com/iamprincesuman/YogaClasses
```

##### Navigate to the Project Directory :
```bash
  cd server
```
##### Install Dependencies : 
```bash
  npm install
```

##### Set Up the Database : 
``` bash
    Create a MySQL database using the script createAdmissionDatabase.sql.
````

##### Configure Environment Variables :
``` bash
    Create a .env file in the server directory and set the following variables :
    DB_HOST=[your_database_host]
    DB_USER=[your_database_user]
    DB_PASSWORD=[your_database_password]
    DB_NAME=[your_database_name]
    PORT=[your_preferred_port]
```
##### Run the Server :
``` bash 
    npm start
```


## Documentation

The project is organized into two main directories: Client and Server. The Client directory contains HTML, CSS, and JavaScript files for the front-end, while the Server directory contains the back-end logic, including controllers, models, routes, services, and utility functions.

### Client Structure
    index: Main HTML file for the Yoga Admission Form.
    batch-change: HTML file for the Batch Change Form.
    monthly-payment: HTML file for the Monthly Payment Form.
    scripts: JavaScript file containing client-side logic for form submission.
    styles: Cascading Style Sheets file for styling the HTML pages.

### Server Structure
    Controllers:
        enrollmentController.js: Handles HTTP requests related to participant enrollment, batch changes, and monthly payments.

    Db:
        createAdmissionDatabase.sql: SQL script to create the necessary database and tables.
        db.js: Database connection configuration.

    Models:
        enrollmentModel.js: Implements functions for enrolling participants, shifting batches, and making monthly payments.

    Routes:
        enrollment.js: Defines API routes for participant enrollment, batch changes, and monthly payments.

    Services:
        paymentService.js: Simulates the payment processing logic.

    Utils:
        errorHandler.js: Utility function for handling errors and sending appropriate responses.

    index.js: Main server file, sets up Express, middleware, and listens for incoming requests.

### Database Structure
The `batches` table manages information related to yoga class schedules. Each batch is assigned a unique `BatchID`, and details such as start time and end time are recorded for effective class organization.

| Field            | Type          | Constraints                      |
|------------------|---------------|----------------------------------|
| BatchID          | INT           | Primary Key, Auto Increment      |
| StartTime        | TIME          | Not NULL                         |
| EndTime          | TIME          | Not NULL                         |

### Payments Table

The `payments` table tracks financial transactions related to participant payments. Each payment is assigned a unique `PaymentID`, and details such as participant ID, payment date, and payment amount are recorded. The `ParticipantID` column is a foreign key linking to the corresponding participant in the `participants` table.

| Field            | Type          | Constraints                      |
|------------------|---------------|----------------------------------|
| PaymentID        | INT           | Primary Key, Auto Increment      |
| ParticipantID    | INT           | Not NULL, Foreign Key (participants) |
| PaymentDate      | TIMESTAMP     | Default: Current Timestamp      |
| Amount           | DECIMAL(10, 2)| Not NULL                         |

### Participants Table

The `participants` table serves as the central repository for information about individuals enrolled in yoga classes. Each participant is uniquely identified by a `ParticipantID`, and crucial details such as their name, age, and enrollment date are recorded. The `BatchID` column establishes a relationship with the corresponding batch in the `batches` table, facilitating the organization of participants into specific class schedules.

| Field            | Type          | Constraints                      |
|------------------|---------------|----------------------------------|
| ParticipantID    | INT           | Primary Key, Auto Increment      |
| Name             | VARCHAR(255)  | Not NULL                         |
| Age              | INT           | Not NULL                         |
| BatchID          | INT           | Not NULL, Foreign Key (batches)  |
| EnrollmentDate   | TIMESTAMP     | Default: Current Timestamp      |
| EndDate          | TIMESTAMP     | Default: Current Timestamp      |

This table establishes a connection with the `batches` table through the `BatchID` foreign key, enabling the efficient management and retrieval of participant information within the context of specific yoga class schedules.

### Entity-Relationship Diagram

![ER Diagram](https://github.com/iamprincesuman/YogaClasses/raw/main/server/db/ERD%20flexmoneyassignment.png)

### API Endpoints

The System exposes several API endpoints to handle ```participant enrollment``` , ```batch changes``` , and ```monthly payments``` . The API follows RESTful conventions and communicates with the server using ```
HTTP POST``` requests. 

    Enroll Participant
        POST /enroll
            Enrolls a participant.
            Request Body: { "name": "Participant Name", "age": 25, "batch": 2 }
            Response: { "success": true, "message": "Enrollment successful! Your ID is 123" }
            Error Response: { "error": "Invalid age. Must be between 18 and 65." }

    Shift Batch
        POST /shift-batch
            Changes a participant's batch.
            Request Body: { "enrollmentId": "ABC123", "newBatch": 3 }
            Response: { "success": true, "message": "Batch shifted successfully" }
            Error Response: { "error": "Must remain in the same batch for the current month." }

    Make Monthly Payment
        POST /make-payment
            Makes a monthly payment.
            Request Body: { "enrollmentId": "ABC123" }
            Response: { "success": true, "message": "Payment made successfully" }
            Error Response: { "error": "Payment for the current month has been made" }


### Features and Process Flow

    Participant Enrollment:
        The process starts when a participant initiates enrollment by providing their name, age, and preferred batch.
        The system validates the information, ensuring it meets the criteria (e.g., age between 18 and 65).
        If the information is valid, the participant is enrolled, and an Enrollment ID is generated.
        The system then proceeds to process the payment for the monthly fee.

    Batch Shifting:
        Participants cannot request to shift to a different batch within the same month.
        The system checks if the participant is currently enrolled and if they are not attempting to shift within the same month.
        If conditions are met, the system updates the participant's batch information.

    Monthly Payment:
        Participants can make monthly payments.
        The system checks if the participant is currently enrolled and if a payment for the current month has not been made.
        If conditions are met, the system processes the monthly payment.

    End:
        The process ends, and the system waits for the next participant action. 

## Conclusion

In summary, the [YogaClasses](https://github.com/iamprincesuman/YogaClasses) project, authored by [Princesuman](https://github.com/iamprincesuman/), is designed with a clear separation between the client and server components. Each serves a specific role in managing participant enrollments, batch changes, and monthly payments for yoga classes. The database structure is carefully organized, with tables such as `batches`, `participants`, and `payments` interlinked to facilitate efficient data management.

The Entity-Relationship Diagram (ERD) visually represents the relationships between these database entities, offering a quick overview of the data flow within the system. The API endpoints follow RESTful conventions, providing a straightforward and consistent interface for interacting with the server.

Whether you are a developer looking to understand the project's architecture or a user exploring the available features, this documentation serves as a comprehensive guide to the YogaClasses system. For any additional information or inquiries, please refer to the respective sections or feel free to reach out to [Princesuman](https://github.com/iamprincesuman/) — the project's author.

