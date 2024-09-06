# Book Management API

This project is a RESTful API for managing books, built using Spring Boot, Maven, and Java 22. The API provides CRUD operations to create, read, update, and delete book records. It uses Spring Boot 3.3.3 along with Spring Data JPA for database operations, and it uses an H2 in-memory database for data persistence.

## Project Setup

The project was initialized using Spring Initializr with the following dependencies:
- **Spring Boot Starter Web:** For building RESTful web services.
- **Spring Boot Starter Data JPA:** For database interaction using JPA.
- **H2 Database:** For an in-memory database during development.

## Design Choices

### 1. **Entity Design:**
   - **Book Entity:** A simple entity with attributes `id`, `title`, `author`, and `publicationYear` was created to represent the book records.
   - **Rationale:** This design keeps the entity straightforward and focused on the essential information needed for a book.

### 2. **Repository Layer:**
   - **BookRepository:** An interface extending `JpaRepository` was created to handle CRUD operations for the Book entity.
   - **Rationale:** Leveraging Spring Data JPA simplifies database interactions and reduces boilerplate code by providing built-in methods for CRUD operations.

### 3. **Service Layer:**
   - **BookService:** A service class was implemented to handle the business logic and interact with the `BookRepository`.
   - **Rationale:** The service layer provides a clean separation of concerns, ensuring that the controller does not directly handle business logic.

### 4. **Controller Layer:**
   - **BookController:** A REST controller was developed with endpoints for retrieving all books, retrieving a book by ID, adding a new book, updating an existing book, and deleting a book.
   - **Rationale:** This structure adheres to RESTful principles, utilizing clear and predictable endpoint naming and HTTP methods (GET, POST, PUT, DELETE).

### 5. **Path Variables and Request Parameters:**
   - Path variables were used to pass book IDs in URL paths for GET, PUT, and DELETE requests.
   - Request body parameters were used for POST and PUT requests to send book details.
   - **Rationale:** This approach aligns with RESTful design practices, making the API intuitive and easy to use.

## Challenges Faced and Solutions

### 1. **Challenge: Handling HTTP Status Codes Properly**
   - **Issue:** Initially, the API returned default HTTP status codes, which were not always appropriate for the operation performed (e.g., returning 200 OK for a resource not found).
   - **Solution:** We used `ResponseEntity` to explicitly set appropriate HTTP status codes (e.g., 201 for created, 404 for not found, 204 for no content).

### 2. **Challenge: Testing Endpoints with Path Variables**
   - **Issue:** Testing path variable handling required careful attention to endpoint formatting and validation of IDs.
   - **Solution:** Used Postman to manually test endpoints, ensuring correct handling of various edge cases, such as non-existent IDs and malformed requests.

### 3. **Challenge: Managing Data Persistence in Development**
   - **Issue:** Using an in-memory H2 database caused data loss upon application restart, which was inconvenient for testing.
   - **Solution:** Configured the H2 console for easy viewing and verification of database contents, and ensured the application setup was smooth for testing scenarios.

### 4. **Challenge: Handling Null Values and Optional Data**
   - **Issue:** Encountered null values for optional fields or when retrieving non-existent resources.
   - **Solution:** Implemented null checks and utilized `Optional` where applicable in the service layer, enhancing the robustness of the API.

## How to Use the API

### 1. **Run the Application:**
   - Ensure you have Java 22 and Maven.
   - Run the application

### 2. **Access the H2 Console:**
   - Go to `http://localhost:8080/h2-console`.
   - Use the JDBC URL `jdbc:h2:mem:testdb`, username `sa`, and password `password` to connect.

### 3. **Test Endpoints Using Postman:**
   - **Retrieve all books:** `GET http://localhost:8080/api/books`
   - **Retrieve a book by ID:** `GET http://localhost:8080/api/books/{id}`
   - **Add a new book:** `POST http://localhost:8080/api/books`
     - Body: `{ "title": "Book Title", "author": "Author Name", "publicationYear": 2023 }`
   - **Update a book by ID:** `PUT http://localhost:8080/api/books/{id}`
     - Body: `{ "title": "Updated Title", "author": "Updated Author", "publicationYear": 2024 }`
   - **Delete a book by ID:** `DELETE http://localhost:8080/api/books/{id}`
