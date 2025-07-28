# Student Management System - Testing Project

This project focuses on testing a Student Management System composed of a Spring Boot backend API and an Angular frontend application. The testing suite includes both API tests (using Postman) and UI tests (using Selenium IDE exported to Java with JUnit). The goal is to identify and document bugs within the provided applications, focusing on CRUD operations for student data.

## Project Description

This project is designed to comprehensively test a student management system. The system consists of two main components: a Spring Boot application acting as the backend API, providing "mock" data without a database, and an Angular application serving as the frontend user interface. The primary objective of this project is to identify and document defects related to the core CRUD (Create, Read, Update, Delete) operations for student records.

The testing approach involves:
1.  **API Testing with Postman**: To verify the correctness of the backend REST endpoints.
2.  **UI Testing with Selenium IDE & Java/JUnit**: To validate data display and interaction within the client-side application.

A key aspect of this project is the focus on documenting the identified bugs in detail, including steps to reproduce them.

## System Under Test

### Backend (Spring Boot)

* **Port**: Runs on `http://localhost:8080`
* **Data**: Provides "mock" data; no database required.
* **Endpoints**: Standard CRUD endpoints for `/student` (GET all, GET by ID, POST, PUT, DELETE).
    * **Note**: Includes `404 NOT FOUND` status codes for cases where a student is not found, aligning with Exercise 8 specifications.

### Frontend (Angular)

* **Port**: Runs on `http://localhost:4200`
* **Functionality**: User interface for interacting with the student data via the backend API.
* **Testing Focus**: Displayed student data and main elements related to CRUD actions. Other components (labels, search, menu content, etc.) are explicitly excluded from the testing scope.

## Testing Tools & Methodologies

### API Testing (Postman)

* **`Students.postman_collection.json`**: Contains a collection of API requests for CRUD operations on student data, including tests to assert expected responses and status codes.
* **`Students.postman_test_run.json`**: A report of a Postman test run, showcasing the results (passes/failures) of the API tests.

### UI Testing (Selenium IDE & Java/JUnit)

* **`Projekat2_tests.side`**: The original Selenium IDE project file, containing recorded UI test cases.
* **Java Test Files**:
    * `DefaultSuiteTest.java`
    * `InsertstudentTest.java`
    * `Test1Test.java`
    * `UpdatestudentTest.java`
    * `DeletestudentTest.java`
    These Java files are exported from Selenium IDE and use JUnit for execution, interacting with the Angular frontend to perform and verify CRUD operations.

## Identified Bugs

A detailed report of identified bugs can be found in `Izvjestaj.docx`. Below is a summary:

### Backend Bugs

* **PUT Method Data Corruption**: During student data updates via the PUT method, all three fields (name, email, branch) incorrectly adopt the value provided for the `studentName` field.
* **GET After Incomplete Update**: Attempting to retrieve an updated student (e.g., with ID 1) fails because the update operation itself was not correctly processed, leading to incorrect data persistence.
* **Incorrect Status Code After Deletion**: After deleting a student (e.g., student with ID 1), a subsequent GET request for that student returns a `200 OK` status code with an empty response body, instead of the expected `404 NOT FOUND`.

### Frontend Bugs

* **Add Student Form Data Mismatch**: When adding a new student through the client application, the entered `email` value is displayed in the 'Name' column in the table, and the `studentBranch` value is displayed in the 'Email' column.
* **Update Student Form Data Corruption on Display**: When updating student data, all three fields in the display table will adopt the value entered for the `studentName` field.
* **Null Value Submission**: It is possible to add a student with null values in the fields through the "Add Student" form, leading to incomplete or invalid student records.
