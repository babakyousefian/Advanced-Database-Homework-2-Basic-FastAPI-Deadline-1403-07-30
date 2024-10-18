# Advanced-Database-Homework-2-Basic-FastAPI-Deadline-1403-07-30
Advanced Database Homework 2 Basic FastAPI Deadline: 1403/07/30

---
---
---

# project one

---


# FastAPI Number Manipulation API

This FastAPI application allows users to perform various operations on numbers, including filtering even numbers, adding numbers to a list, updating numbers at specific indexes, and deleting numbers from the list.

## Features

- **Get Even Digits**: Filters even digits from a number and returns them separated by asterisks (`*`).
- **Add Number to List**: Adds a number to a global list.
- **Update Number in List**: Updates a number at a specific index in the global list.
- **Delete Number from List**: Deletes a specific number from the global list.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn (for running the FastAPI server)

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
---
How to Run the Application

    Save your FastAPI Python file (e.g., app.py).
    Open a terminal and navigate to the directory containing your Python file.
    Run the FastAPI application using Uvicorn:

bash

uvicorn app:app --reload

This will start a local server, and the application will be accessible at:

arduino

http://127.0.0.1:8000

FastAPI automatically generates interactive API documentation. You can access it at:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Get Even Numbers Separated (GET /items/)

This endpoint takes a number as input, filters out all the even digits, and returns them separated by asterisks (*).

    URL: /items/
    Method: GET
    Query Parameter:
        number (int, optional, default=0): The number from which even digits will be filtered.

Example Request:

bash

GET http://127.0.0.1:8000/items/?number=123456

Example Response:

json

{
  "key": "2*4*6"
}

Explanation

    Purpose: This endpoint retrieves only the even digits from the provided number.
    Functionality: The digits of the number are evaluated one by one, and if a digit is even, it's added to the result list.
    Return Value: The even digits are returned in a string, separated by an asterisk (*).

2. Add a Number to List (POST /add/{number})

This endpoint adds a number to a global list maintained in the application.

    URL: /add/{number}
    Method: POST
    Path Parameter:
        number (int, required): The number to be added to the list.

Example Request:

bash

POST http://127.0.0.1:8000/add/10

Example Response:

json

{
  "key": "[10]"
}

Explanation

    Purpose: Adds a number to the list stored in the result global variable.
    Functionality: The number provided in the request is appended to the result list.
    Return Value: The updated list is returned as a JSON response.

3. Update a Number in List (PUT /put/{number})

This endpoint updates a number at a specific index in the global list.

    URL: /put/{number}
    Method: PUT
    Path Parameter:
        number (int, required): The new number that will replace the existing number at the specified index.
    Query Parameter:
        index (int, required): The index at which the number in the list should be replaced.

Example Request:

bash

PUT http://127.0.0.1:8000/put/50?index=0

Example Response:

json

{
  "key": "[50]"
}

Explanation

    Purpose: Replaces a number at a specific position (index) in the result list.
    Functionality: The number at the specified index is replaced with the new number provided in the path.
    Return Value: The updated list is returned after the number is replaced.

4. Delete a Number from List (DELETE /delete/{number})

This endpoint removes a number from the global list.

    URL: /delete/{number}
    Method: DELETE
    Path Parameter:
        number (int, required): The number to be removed from the list.

Example Request:

bash

DELETE http://127.0.0.1:8000/delete/50

Example Response:

json

{
  "key": "[]"
}

Explanation

    Purpose: Removes the given number from the result list.
    Functionality: The remove() function is used to delete the number if it exists in the list.
    Return Value: The updated list is returned after the number has been removed.

Global Variable

python

result = list()

This is a global variable that stores numbers added to it via the /add/{number} endpoint. The same variable is accessed and modified by all the other endpoints (/put/, /delete/, etc.).
Functionality Breakdown
1. print_even_separated(number: int)

This function processes the number digit by digit, checking whether each digit is even. If a digit is even, it is appended to a list, and the final result is returned with even digits separated by an asterisk (*).
2. addNumbers(number: int)

This function appends the provided number to the global result list.
3. putNumbers(number: int, index: int)

This function updates a number in the result list at the specified index. The old value is replaced by the new number provided in the request.
4. deleteNumber(number: int)

This function removes the specified number from the global result list using the remove() method.
Testing the API

You can test the API endpoints using tools like curl, Postman, or even the FastAPI documentation at /docs in your browser.
Example Requests with curl
1. Add a Number to the List

bash

curl -X POST "http://127.0.0.1:8000/add/5"

2. Retrieve Even Numbers from a Number

bash

curl -X GET "http://127.0.0.1:8000/items/?number=123456"

3. Update a Number in the List

bash

curl -X PUT "http://127.0.0.1:8000/put/10?index=0"

4. Delete a Number from the List

bash

curl -X DELETE "http://127.0.0.1:8000/delete/5"

Conclusion

This FastAPI application demonstrates how to create RESTful endpoints for manipulating and managing numbers in a list. The API supports adding, updating, deleting, and filtering even numbers. It also includes basic input validation to ensure proper data types are handled.

Feel free to expand this project by adding more features or integrating it with a database to persist the list beyond the server session.
License

This project is licensed under the MIT License.

vbnet


This Markdown document explains the code in detail and provides instructions on how to set up, run, and test the FastAPI application. Let me know if you'd like any changes or further elaborations!


ChatG
```

---
---
---

# Project two

---
