
Library Management API
This project implements a simple Library Management System using ASP.NET Core Web API. It exposes endpoints for performing CRUD operations on book records.
1. Steps to Run the API
### Prerequisites
Before you start, make sure you have the following installed:
- .NET 6.0 or later (Download from https://dotnet.microsoft.com/)
- Visual Studio or Visual Studio Code (Optional, but recommended)
- Swagger UI (comes pre-configured with the project)

### Running the API
1. Clone the Repository:
   ```bash
   git clone https://github.com/your-username/library-management-api.git
   cd library-management-api
   ```

2. Restore Dependencies:
   In the project folder, restore the NuGet dependencies:
   ```bash
   dotnet restore
   ```

3. Build the Project:
   Build the project using the following command:
   ```bash
   dotnet build
   ```

4. Run the API:
   Start the application with the following command:
   ```bash
   dotnet run
   ```

5. Access Swagger UI:
   Once the API is running, open your browser and navigate to:
   ```
   http://localhost:5000/swagger
   ```

   This will open the Swagger UI where you can interact with the API using a visual interface.
2. Sample Requests for Each Endpoint
POST /api/books
Add a new book to the library.

#### Request Body:
```json
{
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "isbn": "1234567890",
    "available": true
}
```

#### Response:
- **Status**: `201 Created`
- **Body**:
```json
{
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "isbn": "1234567890",
    "available": true
}
```

#### Description:
- Adds a new book to the library.
- ISBN must be unique; if a duplicate ISBN is added, a `409 Conflict` will be returned.
GET /api/books
Retrieve all books in the library.

#### Response:
- **Status**: `200 OK`
- **Body**:
```json
[
    {
        "title": "The Great Gatsby",
        "author": "F. Scott Fitzgerald",
        "isbn": "1234567890",
        "available": true
    }
]
```

#### Description:
- Retrieves a list of all books currently available in the library.
GET /api/books/{title}
Search for books in the library by title.

#### Request:
- **Example**: Search for books with titles containing "Gatsby".
- **URL**: `/api/books/Gatsby`

#### Response:
- **Status**: `200 OK`
- **Body**:
```json
[
    {
        "title": "The Great Gatsby",
        "author": "F. Scott Fitzgerald",
        "isbn": "1234567890",
        "available": true
    }
]
```

#### Description:
- Retrieves books whose title contains the search term. The search is case-insensitive.
PUT /api/books/{isbn}
Update the details of an existing book by ISBN.

#### Request Body:
```json
{
    "title": "The Great Gatsby - Revised",
    "author": "F. Scott Fitzgerald",
    "isbn": "1234567890",
    "available": false
}
```

#### Response:
- **Status**: `200 OK`
- **Body**:
```json
{
    "title": "The Great Gatsby - Revised",
    "author": "F. Scott Fitzgerald",
    "isbn": "1234567890",
    "available": false
}
```

#### Description:
- Updates the book with the provided ISBN. If the book is not found, a `404 Not Found` will be returned.
DELETE /api/books/{isbn}
Remove a book from the library by ISBN.

#### Request:
- **URL**: `/api/books/1234567890`

#### Response:
- **Status**: `204 No Content`
- **Body**: None

#### Description:
- Deletes the book with the provided ISBN from the library. If the book is not found, a `404 Not Found` will be returned.
3. Error Handling
Here are some common error responses that you might encounter:

1. **400 Bad Request** - When the input data is invalid (e.g., missing required fields).
   - Example:
     ```json
     {
         "title": ["The title field is required."],
         "isbn": ["The ISBN field is required."]
     }
     ```

2. **404 Not Found** - When the book cannot be found (e.g., attempting to update or delete a non-existent book).
   - Example:
     ```json
     {
         "Message": "Book not found."
     }
     ```

3. **409 Conflict** - When trying to add a book with a duplicate ISBN.
   - Example:
     ```json
     {
         "Message": "A book with this ISBN already exists."
     }
     ```

4. **500 Internal Server Error** - If an unexpected error occurs.
