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
# FastAPI High Precision Expression Calculation API

This FastAPI application computes an alternating sum of factorial expressions using the `decimal` module to handle high-precision calculations. The formula involves calculating factorials for terms and dividing them by specific divisor expressions, with alternating signs.

## Features

- **High-Precision Calculations**: Using Python's `decimal.Decimal` for precision up to 1000 decimal places.
- **Factorial Computation**: Factorial of terms computed in a loop and used in the alternating sum.
- **Alternating Sign Series**: The result is the sum of a series with alternating positive and negative terms.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
```
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
1. Compute Expression (GET /items/)

This endpoint takes a number n and computes the sum of a series involving factorials, with alternating signs. The expression is:

css

term = (factorial(2 * i + 3)) / (i + 2 + (9 - 2 * i))

    URL: /items/
    Method: GET
    Query Parameter:
        n (int, optional, default=0): The number of terms to include in the series.

Example Request:

bash

GET http://127.0.0.1:8000/items/?n=10

Example Response:

json

{
  "result": "a high-precision decimal result"
}

Explanation

    Purpose: This endpoint computes a mathematical expression involving factorials and alternating signs. The goal is to compute the sum of terms, where each term involves the factorial of (2 * i + 3) divided by an expression (i + 2 + (9 - 2 * i)).
    Factorial Calculation: The function Factorial(n) computes the factorial of the number n by iterating through numbers from 1 to n.
    Alternating Sign: The sign alternates between positive and negative for each term in the sum.
    Precision: The Decimal class from the decimal module is used for high-precision calculations, ensuring the result is computed accurately up to 1000 decimal places.

Return Value

The endpoint returns the computed result as a high-precision decimal number in JSON format.
Code Details
Factorial Function

python

def Factorial(n: int) -> int:
    if not isinstance(n, int):
        raise TypeError("\n\n An ERROR occurred...!!!")
    
    fact = 1
    if n == 0 or n == 1:
        return 1
    else:
        for i in range(2, n+1, 1):
            fact *= i

    return fact

    Input: Takes an integer n.
    Output: Returns the factorial of n. If n is 0 or 1, the function returns 1. Otherwise, it multiplies all integers from 1 to n.
    Error Handling: Raises a TypeError if the input is not an integer.

Main Function: compute_expression

python

@app.get("/items/")
async def compute_expression(n: int = 0):
    result = Decimal(0)
    sign = 1

    n1 = int(n)
    for i in range(0, n1 + 1, 1):
        factorial_part = ((2 * i) + 3)
        divisor = Decimal(i + 2)
        constant = Decimal(9 - (2 * i))

        if divisor + constant == 0:
            continue

        term = (Decimal(Factorial(factorial_part))) / (divisor + constant)
        result += sign * term
        sign *= -1

    return result

    Input: Takes an integer n from the request as a query parameter.
    Processing:
        Loops from i = 0 to n.
        For each i, computes the factorial of (2 * i + 3).
        Divides the factorial by (i + 2 + (9 - 2 * i)), skipping terms that would result in division by zero.
        Alternates the sign of each term (positive, negative, positive, etc.).
        Adds the term to the result using high-precision Decimal.
    Output: Returns the final sum as a high-precision Decimal.

High Precision with decimal.Decimal

python

from decimal import Decimal, getcontext
getcontext().prec = 1000

    Precision: The getcontext().prec = 1000 line sets the precision for all Decimal calculations to 1000 digits. This ensures accurate calculations, especially when dealing with large numbers and factorials.
    Why Decimal?: The Decimal type provides greater control over precision and rounding than Python's built-in float, which is essential for handling large numbers generated by the factorial function.

Example

Let’s say you want to compute the sum of 5 terms using the expression:

bash

GET http://127.0.0.1:8000/items/?n=5

    The first term would compute the factorial of 2 * 0 + 3 = 3, divided by 0 + 2 + (9 - 2 * 0) = 11.
    The second term would compute the factorial of 2 * 1 + 3 = 5, divided by 1 + 2 + (9 - 2 * 1) = 10, but this term would be subtracted due to the alternating sign.
    The next terms would follow the same pattern, alternating between addition and subtraction, and involving larger factorials as i increases.

The result will be returned in high precision.
License

This project is licensed under the MIT License.

vbnet


This `README.md` explains the structure of your FastAPI application, how it works, and details the purpose of each function and endpoint. Let me know if you’d like to expand further on any section!


---
---
---

# project 3rd
---

# FastAPI Application: Filter 4-Digit Numbers Based on Conditions

This FastAPI application filters 4-digit numbers within a given range (`n1` to `n2`) and returns numbers where the sum of the last two digits equals the product of the first two digits.

## Features

- **Input Range**: The application accepts two numbers, `n1` and `n2`, which define the range of 4-digit numbers to check.
- **Number Filtering**: For each number in the range, it checks if the sum of the last two digits is equal to the product of the first two digits.
- **FastAPI Integration**: The application uses FastAPI to expose this logic through an HTTP GET request.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
```

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
1. Check 4-Digit Numbers (GET /items/)

This endpoint checks all 4-digit numbers between n1 and n2 (both inclusive) and returns a list of numbers where the sum of the last two digits equals the product of the first two digits.

    URL: /items/
    Method: GET
    Query Parameters:
        n1 (str, required): The lower bound of the range (inclusive).
        n2 (str, required): The upper bound of the range (exclusive).

Example Request:

bash

GET http://127.0.0.1:8000/items/?n1=1000&n2=9999

Example Response:

json

{
  "key": ["2025", "4312", "6216"]
}

The key field contains a list of all numbers between n1 and n2 that satisfy the condition.
Code Breakdown
Main Function: print_All_4_Digits

python

@app.get("/items/")
async def print_All_4_Digits(n1: (str) = 0, n2: (str) = 0) -> dict:
    if not isinstance(n1, str) or not isinstance(n2, str):
        raise TypeError("\n\n An ERROR occur...!!!")
    else:
        l = list()
        p1 = 0
        p2 = 0
        l2 = list()
        n1_str = int(n1)
        n2_str = int(n2)
        for i in range(n1_str, n2_str, 1):
            l = list(str(i))
            p1 = int(int(l[len(str(i)) - 1]) + int(l[len(str(i)) - 2]))
            p2 = int(int(l[0]) * int(l[1]))
            if p1 == p2:
                l2.append(str(i))
            else:
                continue
        return {"key": l2}

Explanation

    Input: The function accepts two parameters, n1 and n2, both of which are strings representing the lower and upper bounds of the range.
        n1: The start of the range (inclusive).
        n2: The end of the range (exclusive).
    Validation: The function checks if n1 and n2 are strings. If not, it raises a TypeError.
    Conversion: The input strings n1 and n2 are converted to integers (n1_str and n2_str) for use in the loop.

Processing Loop

    The loop iterates over each number i between n1_str and n2_str.
    Each number i is converted to a string and stored in a list l, where each digit is a separate list element.
    Condition:
        The sum of the last two digits (p1) is computed as:

        python

p1 = int(l[len(str(i)) - 1]) + int(l[len(str(i)) - 2])

The product of the first two digits (p2) is computed as:

python

        p2 = int(l[0]) * int(l[1])

        If the sum of the last two digits equals the product of the first two digits (p1 == p2), the number is added to the result list l2.

Return Value

    Output: The function returns a dictionary containing the list of numbers l2 where the condition is met, with the key being "key".

Example of Logic

Let’s say the number is 2025. Here’s how the function processes it:

    The last two digits are 2 and 5, so their sum is 2 + 5 = 7.
    The first two digits are 2 and 0, so their product is 2 * 0 = 0.
    Since the sum 7 is not equal to the product 0, 2025 would not be included in the result list.

Error Handling

    If the input n1 or n2 is not a string, the function raises a TypeError with the message:

    vbnet

    An ERROR occur...!!!

Example

Let’s assume you want to check for all numbers between 1000 and 2000. Here’s what you can do:

bash

GET http://127.0.0.1:8000/items/?n1=1000&n2=2000

The result might look like this:

json

{
  "key": ["2025", "3126"]
}

This means that 2025 and 3126 are numbers within this range where the sum of the last two digits equals the product of the first two digits.
License

This project is licensed under the MIT License.

vbnet


This `README.md` explains how the FastAPI application works, including how to run it, the purpose of the API, and how each part of the code functions. Let me know if you'd like to add any more details!


---
---
---

# 4th project

# FastAPI Application: Filter 3-Digit Numbers with Even Digits

This FastAPI application filters 3-digit numbers within a given range (`n1` to `n2`), returning only those numbers where all digits are even.

## Features

- **Input Range**: The application accepts two numbers, `n1` and `n2`, which define the range of 3-digit numbers to check.
- **Even Digits Filter**: For each number in the range, it checks if all digits are even.
- **FastAPI Integration**: The application uses FastAPI to expose this logic through an HTTP GET request.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
```

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
1. Filter 3-Digit Numbers with Even Digits (GET /items/)

This endpoint filters all numbers between n1 and n2 (both inclusive) and returns numbers where all digits are even.

    URL: /items/
    Method: GET
    Query Parameters:
        n1 (str, required): The lower bound of the range (inclusive).
        n2 (str, required): The upper bound of the range (exclusive).

Example Request:

bash

GET http://127.0.0.1:8000/items/?n1=200&n2=500

Example Response:

json

{
  "key": ["200", "202", "204", "206", "208", "220", "222", "224"]
}

The key field contains a list of all numbers between n1 and n2 where all digits are even.
Code Breakdown
Main Function: print_all_3_digits_numbers

python

@app.get("/items/")
async def print_all_3_digits_numbers(n1: (str) = "0", n2: (str) = "0") -> dict:
    if not isinstance(n1, str) or not isinstance(n2, str):
        raise TypeError("\n\n An ERROR occur...!!!")
    else:
        n1_str = int(n1)
        n2_str = int(n2)
        l = list()
        for i in range(n1_str, n2_str, 1):
            number = str(i)
            if all(int(digits) % 2 == 0 for digits in number):
                l.append(str(i))
            else:
                continue
        return {"key": l}

Explanation

    Input: The function accepts two parameters, n1 and n2, both of which are strings representing the lower and upper bounds of the range.
        n1: The start of the range (inclusive).
        n2: The end of the range (exclusive).
    Validation: The function checks if n1 and n2 are strings. If not, it raises a TypeError.
    Conversion: The input strings n1 and n2 are converted to integers (n1_str and n2_str) for use in the loop.

Processing Loop

    The loop iterates over each number i between n1_str and n2_str.
    Each number i is converted to a string, and the digits are checked one by one.
    Condition:
        The all function checks if each digit in the number is even:

        python

        all(int(digits) % 2 == 0 for digits in number)

        If all digits of the number are even, the number is appended to the list l.

Return Value

    Output: The function returns a dictionary containing the list of numbers l where all digits are even, with the key being "key".

Example of Logic

Let’s say the range is from 200 to 250. Here’s how the function processes this:

    It iterates over each number in the range.
    For each number, it checks if all the digits are even. For example:
        For 202: All digits are even, so it's added to the list.
        For 203: Not all digits are even (3 is odd), so it's skipped.

Error Handling

    If the input n1 or n2 is not a string, the function raises a TypeError with the message:

    vbnet

    An ERROR occur...!!!

Example

Let’s assume you want to check for all 3-digit numbers between 200 and 500 where all digits are even. Here’s what you can do:

bash

GET http://127.0.0.1:8000/items/?n1=200&n2=500

The result might look like this:

json

{
  "key": ["200", "202", "204", "206", "208", "220", "222", "224"]
}

This means that these numbers between 200 and 500 have all even digits.
License

This project is licensed under the MIT License.

css


This `README.md` file provides a detailed explanation of the code, including how it works, how to run it, and what it does.



---
---
---

# 5th project

# FastAPI Application: Print Multiplication Pattern

This FastAPI application generates a multiplication pattern based on the input number `n`. The multiplication pattern consists of rows, where each row contains the products of a number and its preceding integers. The number of rows is determined by the input parameter `n`.

## Features

- **Pattern Generation**: For a given integer `n`, the application generates a multiplication pattern with `n` rows. Each row contains the multiplication products of a number from `1` to `n`.
- **FastAPI Integration**: The application is accessible via an HTTP GET request.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

Install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
```

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
1. Generate Multiplication Pattern (GET /items/)

This endpoint generates a multiplication pattern for a given number n. The pattern is in the form of a list of lists, where each row contains the multiplication products of the row number and the column number.

    URL: /items/
    Method: GET
    Query Parameters:
        n (int, optional, default=8): The number of rows to generate in the multiplication pattern.

Example Request:

bash

GET http://127.0.0.1:8000/items/?n=5

Example Response:

json

{
  "pattern": [
    [1],
    [2, 4],
    [3, 6, 9],
    [4, 8, 12, 16],
    [5, 10, 15, 20, 25]
  ]
}

The pattern field contains a list of lists where each list represents a row of the multiplication pattern.
Code Breakdown
Main Function: print_pattern

python

@app.get("/items/")
async def print_pattern(n: int = 8):
    pattern = []
    for i in range(1, n + 1):
        row = []
        for j in range(1, i + 1):
            row.append(i * j)
        pattern.append(row)
    return {"pattern": pattern}

Explanation

    Input:
        The function accepts an integer n which represents the number of rows to generate in the multiplication pattern.
        By default, n is set to 8, so if the user does not provide a value for n, it will generate a pattern for n = 8.

    Pattern Generation:
        The function creates an empty list pattern to hold the rows of the multiplication table.
        The outer loop iterates over i from 1 to n (inclusive), where i represents the row number.
        The inner loop iterates over j from 1 to i (inclusive), where j represents the column number.
        For each i and j, the product i * j is calculated and added to the current row.
        The row is appended to the pattern list.

Example of Logic

Let’s say n = 5. Here’s how the function processes this:

    Step 1: Create an empty list pattern.
    Step 2: For each row i from 1 to 5:
        For row 1: Only the number 1 (1*1) is added.
        For row 2: The numbers 2 (2*1) and 4 (2*2) are added.
        For row 3: The numbers 3 (3*1), 6 (3*2), and 9 (3*3) are added.
        And so on.

Return Value

    Output: The function returns a dictionary with the key "pattern", containing a list of lists where each list represents a row in the multiplication pattern.

Example of n = 5

Here’s what the pattern would look like for n = 5:

csharp

[
    [1],
    [2, 4],
    [3, 6, 9],
    [4, 8, 12, 16],
    [5, 10, 15, 20, 25]
]

Error Handling

    There is no specific error handling in this function for invalid inputs. However, FastAPI will automatically handle validation errors (e.g., if a non-integer is provided for n).

Example

Let’s assume you want to generate a multiplication pattern for n = 4. Here’s what you can do:

bash

GET http://127.0.0.1:8000/items/?n=4

The result might look like this:

json

{
  "pattern": [
    [1],
    [2, 4],
    [3, 6, 9],
    [4, 8, 12, 16]
  ]
}

License

This project is licensed under the MIT License.

css


This `README.md` file provides a detailed explanation of the FastAPI code, including how it works, how to run it, and what it does.


---
---
---

# 6th project

# FastAPI Application: Statistical Operations on a List of Numbers

This FastAPI application performs basic statistical operations on a list of five numbers provided by the user. The operations include calculating the **maximum**, **minimum**, **average**, and **standard deviation**. Additionally, it provides functionality to add new numbers to the list and update specific elements in the list.

## Features

1. **Input**: Five numbers (`n1`, `n2`, `n3`, `n4`, `n5`) passed as query parameters, with `n1` and `n2` being strings and the rest as integers.
2. **Output**: Returns the maximum, minimum, average, and standard deviation of the numbers.
3. **CRUD Operations**:
   - **POST**: Add a new number to the list.
   - **PUT**: Update an element in the list at a specific index.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn
```

Here is a README.md file for your FastAPI project:

markdown

# FastAPI Application: Statistical Operations on a List of Numbers

This FastAPI application performs basic statistical operations on a list of five numbers provided by the user. The operations include calculating the **maximum**, **minimum**, **average**, and **standard deviation**. Additionally, it provides functionality to add new numbers to the list and update specific elements in the list.

## Features

1. **Input**: Five numbers (`n1`, `n2`, `n3`, `n4`, `n5`) passed as query parameters, with `n1` and `n2` being strings and the rest as integers.
2. **Output**: Returns the maximum, minimum, average, and standard deviation of the numbers.
3. **CRUD Operations**:
   - **POST**: Add a new number to the list.
   - **PUT**: Update an element in the list at a specific index.

## Requirements

- Python 3.7+
- FastAPI
- Uvicorn

You can install the required libraries using `pip`:

```bash
pip install fastapi uvicorn

How to Run the Application

    Save your FastAPI Python file (e.g., app.py).
    Open a terminal and navigate to the directory containing your Python file.
    Run the FastAPI application using Uvicorn:

bash

uvicorn app:app --reload

This will start a local server, and the application will be accessible at:

arduino

http://127.0.0.1:8000

You can access the interactive API documentation here:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Calculate Statistics (GET /items/)

This endpoint calculates the maximum, minimum, average, and standard deviation for five input numbers. The first two numbers (n1 and n2) are passed as strings, and the rest (n3, n4, n5) as integers.

    URL: /items/
    Method: GET
    Query Parameters:
        n1 (str, default="0"): The first number (string format).
        n2 (str, default="0"): The second number (string format).
        n3 (int, default=0): The third number.
        n4 (int, default=0): The fourth number.
        n5 (int, default=0): The fifth number.

Example Request:

bash

GET http://127.0.0.1:8000/items/?n1=3&n2=5&n3=7&n4=9&n5=2

Example Response:

json

{
  "Maximum": 9,
  "Minimum": 2,
  "Average": 5.2,
  "Standard Deviation": 2.682160327836416
}

2. Add a Number to the List (POST /items/{number
})

This endpoint adds a new number to the list l.

    URL: /items/{number:int}
    Method: POST
    Path Parameter:
        number (int): The number to add to the list.

Example Request:

bash

POST http://127.0.0.1:8000/items/10

Example Response:

json

{
  "updated_list": [3, 5, 7, 9, 2, 10]
}

3. Update a Number in the List (PUT /items/put/)

This endpoint updates a number at a specific index in the list.

    URL: /items/put/
    Method: PUT
    Query Parameters:
        number (int, default=0): The new number to replace the current one.
        index (int, default=0): The index at which the number should be replaced.

Example Request:

bash

PUT http://127.0.0.1:8000/items/put/?number=15&index=2

Example Response:

json

{
  "updated_list": [3, 5, 15, 9, 2]
}

If the index is out of range, the API will return an error:

json

{
  "error": "Index out of range"
}

Code Breakdown
Main Function: calculateN

python

@app.get("/items/")
async def calculateN(n1: str = "0", n2: str = "0", n3: int = 0, n4: int = 0, n5: int = 0):
    try:
        n1, n2 = int(n1), int(n2)
    except ValueError:
        return {"error": "n1 and n2 must be valid integers"}

    l.clear()
    l.extend([n1, n2, n3, n4, n5])

    maximum = max(l)
    minimum = min(l)
    sum_values = sum(l)
    average = sum_values / len(l)

    N = len(l)
    mu = average
    variance_sum = sum((x - mu) ** 2 for x in l)
    variance = variance_sum / N
    standard_deviation = sqrt(variance)

    return {
        "Maximum": maximum,
        "Minimum": minimum,
        "Average": average,
        "Standard Deviation": standard_deviation
    }

    Input Handling: The first two inputs n1 and n2 are passed as strings and then converted to integers. If the conversion fails, the function raises a ValueError and returns an error message.
    Operations: The function calculates the following:
        Maximum: The largest value in the list.
        Minimum: The smallest value in the list.
        Average: The sum of the values divided by the number of elements.
        Standard Deviation: The square root of the variance (how spread out the numbers are).

Adding and Updating Numbers

    addNumber: Appends a new number to the list l.
    putNumber: Replaces the number at a given index with a new number, if the index is valid. Otherwise, it returns an error.

Example

Let’s assume you want to calculate the statistics for five numbers: 3, 5, 7, 9, and 2.

    You can call the API like this:

bash

GET http://127.0.0.1:8000/items/?n1=3&n2=5&n3=7&n4=9&n5=2

    The result might look like this:

json

{
  "Maximum": 9,
  "Minimum": 2,
  "Average": 5.2,
  "Standard Deviation": 2.682160327836416
}

License

This project is licensed under the MIT License.

css


This `README.md` file gives a complete explanation of the code, including its functionality, usage, and examples.

```

---
---
---

# 7th project

# FastAPI Application: Statistical Functions for a List of Integers

This FastAPI application calculates basic statistical metrics—**maximum**, **minimum**, **average**, and **standard deviation**—from a list of five integers provided as query parameters.

## Features

- **Input**: Accepts five integers (`n1`, `n2`, `n3`, `n4`, `n5`) via query parameters.
- **Output**: Returns a JSON object containing:
  - Maximum value of the list.
  - Minimum value of the list.
  - Average (mean) value of the list.
  - Standard deviation of the values in the list.

## Requirements

- **Python 3.7+**
- **FastAPI**
- **Uvicorn** for running the application.

Install the required dependencies with:

```bash
pip install fastapi uvicorn
```

How to Run the Application

    Save your FastAPI code in a Python file, e.g., main.py.
    Open a terminal in the same directory where the file is located.
    Run the application using Uvicorn:

bash

uvicorn main:app --reload

The application will start, and you can access it at:

arduino

http://127.0.0.1:8000

You can view the API's interactive documentation here:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Calculate Statistical Metrics (GET /items/)

This endpoint computes the maximum, minimum, average, and standard deviation of five integers passed as query parameters.

    URL: /items/
    Method: GET
    Query Parameters:
        n1 (int): The first integer.
        n2 (int): The second integer.
        n3 (int): The third integer.
        n4 (int): The fourth integer.
        n5 (int): The fifth integer.

Example Request

bash

GET http://127.0.0.1:8000/items/?n1=10&n2=20&n3=30&n4=40&n5=50

Example Response

json

{
  "maximum": 50,
  "minimum": 10,
  "average": 30.0,
  "standard_deviation": 14.142135623730951
}

Code Explanation
1. Max1 Function

The Max1 function calculates the maximum value from the list of integers.

python

async def Max1(l: list) -> int:
    maximum = int(l[0])
    for i in range(1, len(l), 1):
        if int(l[i]) > maximum:
            maximum = int(l[i])
    return maximum

    Iterates through the list and compares each value to find the maximum.
    Returns the maximum value.

2. Min1 Function

The Min1 function calculates the minimum value from the list.

python

async def Min1(l: list) -> int:
    minimum = int(l[0])
    for i in range(1, len(l), 1):
        if int(l[i]) < minimum:
            minimum = int(l[i])
    return minimum

    Iterates through the list and compares each value to find the minimum.
    Returns the minimum value.

3. Ave1 Function

The Ave1 function calculates the average (mean) of the list.

python

async def Ave1(l: list) -> float:
    total_sum = 0
    for i in range(len(l)):
        total_sum += int(l[i])
    length = len(l)
    return total_sum / length

    Sums all the values in the list and divides the sum by the number of elements to calculate the average.

4. STD1 Function

The STD1 function calculates the standard deviation of the list.

python

async def STD1(l: list) -> float:
    length = len(l)
    average = await Ave1(l)
    sumation = 0
    for i in range(len(l)):
        sumation += ((int(l[i])) - average) ** 2
    variance = sumation / length
    return sqrt(variance)

    Standard deviation is calculated as the square root of the variance, where variance is the average of the squared differences between each number and the mean.

Main Endpoint: calculate_some_functions

The main endpoint /items/ is responsible for computing all the statistical metrics.

python

@app.get("/items/")
async def calculate_some_functions(n1: int = 0, n2: int = 0, n3: int = 0, n4: int = 0, n5: int = 0) -> dict:
    if not all(isinstance(i, int) for i in [n1, n2, n3, n4, n5]):
        raise TypeError("\n\n Please enter valid integer numbers...!!!")
    else:
        numbers_list.clear()
        numbers_list.extend([n1, n2, n3, n4, n5])

        maximum_number = await Max1(numbers_list)
        minimum_number = await Min1(numbers_list)
        average = await Ave1(numbers_list)
        standard_deviation = await STD1(numbers_list)

        return {
            "maximum": maximum_number,
            "minimum": minimum_number,
            "average": average,
            "standard_deviation": standard_deviation
        }

    Input: Receives five integer values via query parameters (n1, n2, n3, n4, n5).
    Output: Returns a JSON object with the following:
        maximum: The maximum value from the list.
        minimum: The minimum value from the list.
        average: The average (mean) value.
        standard_deviation: The standard deviation.

Error Handling

    If the input is not a valid integer, a TypeError is raised:

python

if not all(isinstance(i, int) for i in [n1, n2, n3, n4, n5]):
    raise TypeError("\n\n Please enter valid integer numbers...!!!")

Example

Let’s calculate the statistical metrics for the integers: 10, 20, 30, 40, 50.

bash

GET http://127.0.0.1:8000/items/?n1=10&n2=20&n3=30&n4=40&n5=50

The response will be:

json

{
  "maximum": 50,
  "minimum": 10,
  "average": 30.0,
  "standard_deviation": 14.142135623730951
}

License

This project is licensed under the MIT License.

css


This `README.md` file provides a detailed description of your FastAPI project, explaining the code, API endpoints, and example usage.


---
---
---

# 8th project

# FastAPI Application: Find Maximum Digit and Remove It

This FastAPI application performs two main tasks with a given 5-digit number:

1. **Finds the maximum digit** in the number.
2. **Removes the first occurrence** of the maximum digit from the number and returns the modified number.

## Features

- **Input**: A 5-digit integer passed as a query parameter.
- **Output**: A JSON response containing:
  - The maximum digit found in the number.
  - The number after removing the first occurrence of the maximum digit.

## Requirements

- **Python 3.7+**
- **FastAPI**
- **Uvicorn** to run the application.

To install the required dependencies, run:

```bash
pip install fastapi uvicorn
```


How to Run the Application

    Save your FastAPI code in a Python file, e.g., main.py.
    Open a terminal in the same directory where the file is located.
    Run the application using Uvicorn:

bash

uvicorn main:app --reload

The application will start, and you can access it at:

arduino

http://127.0.0.1:8000

You can view the API's interactive documentation here:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Calculate Maximum Digit and Remove It (GET /items/)

This endpoint performs the following operations on the provided 5-digit number:

    Finds the maximum digit.

    Removes the first occurrence of the maximum digit from the number.

    URL: /items/

    Method: GET

    Query Parameters:
        number (int): The 5-digit integer on which the calculations will be performed.

Example Request

bash

GET http://127.0.0.1:8000/items/?number=54321

Example Response

json

{
  "max-digit": 5,
  "final-number": 4321
}

Code Explanation
1. F1 Function: Find Maximum Digit

The F1 function takes the 5-digit number as input, converts it to a string, and then finds the maximum digit.

python

def F1(number):
    max_digit = max(str(number))
    return int(max_digit)

    Converts the number to a string.
    Uses the max() function to find the largest digit.
    Converts the result back to an integer and returns it.

2. F2 Function: Remove First Occurrence of Maximum Digit

The F2 function removes the first occurrence of the maximum digit from the number.

python

def F2(number, max_digit):
    number_str = str(number)
    number_str = number_str.replace(str(max_digit), '', 1)
    return int(number_str) if number_str else 0

    Converts the number to a string.
    Uses the replace() method to remove the first occurrence of the maximum digit.
    Converts the modified string back to an integer and returns it.

3. Main Endpoint: calculate_n

This endpoint performs the main task of calculating the maximum digit and the modified number.

python

@app.get("/items/")
async def calculate_n(number: int) -> dict:
    if len(str(number)) != 5:
        raise HTTPException(status_code=400, detail="Please enter a 5-digit number.")

    max_digit = F1(number)
    final_number = F2(number, max_digit)

    return {"max-digit": max_digit, "final-number": final_number}

    Input: Accepts a number (int) as a query parameter.
    Validation: If the number is not exactly 5 digits long, it raises a 400 error with a relevant message.
    Output: Returns a JSON object with two values:
        max-digit: The largest digit in the number.
        final-number: The number after removing the first occurrence of the largest digit.

Error Handling

If the input is not a 5-digit number, the following exception is raised:

python

raise HTTPException(status_code=400, detail="Please enter a 5-digit number.")

This ensures that only valid 5-digit numbers are processed.
Example

Let’s calculate the maximum digit and modified number for the integer 54321.

bash

GET http://127.0.0.1:8000/items/?number=54321

The response will be:

json

{
  "max-digit": 5,
  "final-number": 4321
}

If you try to enter a number that is not 5 digits, you will receive a 400 error:

json

{
  "detail": "Please enter a 5-digit number."
}

License

This project is licensed under the MIT License.

css


This `README.md` provides a comprehensive description of your FastAPI project, explaining its functionality, the endpoints, example requests and responses, and the logic behind the code.


---
---
---

# 9th project

# FastAPI Application: Local and Global Variable Demonstration

This FastAPI application demonstrates the usage of local and global variables in Python, specifically within asynchronous functions.

## Features

- **Asynchronous functions** that manipulate local and global variables.
- **Logging** of variable access to show which variables are accessible globally and which are confined locally to their respective functions.

## Requirements

- **Python 3.7+**
- **FastAPI**
- **Uvicorn** to run the application.

To install the required dependencies, run:

```bash
pip install fastapi uvicorn
```

How to Run the Application

    Save the FastAPI code in a Python file, e.g., main.py.
    Open a terminal in the same directory where the file is located.
    Run the application using Uvicorn:

bash

uvicorn main:app --reload

The application will start, and you can access it at:

arduino

http://127.0.0.1:8000

You can view the API's interactive documentation here:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Check Local and Global Variable Behavior (GET /items/)

This endpoint demonstrates how local and global variables work in Python asynchronous functions.

    URL: /items/
    Method: GET

Example Request

bash

GET http://127.0.0.1:8000/items/

Example Response

json

{
  "p1": "I live in Khorramabad",
  "p2": "I live in Khorramabad",
  "p3": "I live in Khorramabad",
  "p4": "I live in Khorramabad"
}

Code Explanation
1. P1 Function: Local Variable

The P1 function defines a local variable s1 and returns it:

python

async def P1() -> str:
    s1 = "I live in Khorramabad"
    return s1

2. P2 Function: Local Variable with Print Statement

The P2 function defines a local variable s2, prints it inside the function, and returns it:

python

async def P2() -> str:
    s2 = "I live in Khorramabad"
    print("inside function:", s2)
    return s2

3. P3 Function: Global Variable

The P3 function defines and sets a global variable s3. The value of s3 is accessible outside the function because it’s global:

python

async def P3() -> str:
    global s3
    s3 = "I live in Khorramabad"
    print(s3)
    return s3

4. P4 Function: Local Variable

The P4 function defines another local variable s4 and prints it:

python

async def P4() -> str:
    s4 = "I live in Khorramabad"
    print(s4)
    return s4

5. Main Endpoint: check_global_or_local_variable

This endpoint calls the asynchronous functions and checks whether global and local variables can be accessed:

python

@app.get("/items/")
async def check_global_or_local_variable() -> dict:
    p1 = await P1()
    p2 = await P2()
    p3 = await P3()
    p4 = await P4()

    print("\nCan we read s2 here? No, it's a local variable.")
    print(f"Global variable s3 after P3 call: {s3}")

    return {
        "p1": p1,
        "p2": p2,
        "p3": p3,
        "p4": p4
    }

    Local Variables: s1, s2, and s4 are local to their respective functions.
    Global Variable: s3 is declared global, meaning it can be accessed outside of the P3 function.

Key Points:

    s2 is local to the P2 function, and cannot be accessed globally.
    s3 is global, so it can be printed after the P3 function has been executed.

Example Output

After calling the /items/ endpoint, the following values will be returned:

    p1: "I live in Khorramabad" (Local variable in P1)
    p2: "I live in Khorramabad" (Local variable in P2)
    p3: "I live in Khorramabad" (Global variable from P3)
    p4: "I live in Khorramabad" (Local variable in P4)

Console Output Example

In the console, you will see the following printed:

less

inside function: I live in Khorramabad
I live in Khorramabad

Can we read s2 here? No, it's a local variable.
Global variable s3 after P3 call: I live in Khorramabad

License

This project is licensed under the MIT License.

css


This `README.md` file provides a detailed explanation of your FastAPI project, covering its functionality, endpoints, code explanation, and sample outputs.


---
---
---

# 10th project

# FastAPI Application: Recursive Factorial Calculation

This FastAPI application demonstrates how to calculate the factorial of a number recursively using Python's `async` capabilities.

## Features

- **Asynchronous Factorial Calculation**: This application calculates the factorial of a given number recursively in an asynchronous way using FastAPI.
- **Error Handling**: The application checks if the input number is a valid string that can be converted to an integer and raises an error for invalid inputs.

## Requirements

- **Python 3.7+**
- **FastAPI**
- **Uvicorn** to run the application.

To install the required dependencies, run:

```bash
pip install fastapi uvicorn
```

---
---
---

How to Run the Application

    Save the FastAPI code in a Python file, e.g., main.py.
    Open a terminal in the same directory where the file is located.
    Run the application using Uvicorn:

bash

uvicorn main:app --reload

The application will start, and you can access it at:

arduino

http://127.0.0.1:8000

You can view the API's interactive documentation here:

arduino

http://127.0.0.1:8000/docs

API Endpoints
1. Recursive Factorial Function (GET /items/)

This endpoint calculates the factorial of a given number recursively.

    URL: /items/
    Method: GET
    Parameters:
        number (str): The number as a string input for which the factorial needs to be calculated.

Example Request

bash

GET http://127.0.0.1:8000/items/?number=5

Example Response

json

{
  "result": 120
}

Code Explanation
1. factorial Function (Recursive)

This function calculates the factorial of a given number using recursion.

    If the number is 1 (base case), it returns 1.
    Otherwise, it recursively multiplies the current number by the factorial of the number minus one.

python

async def factorial(x:int=0) -> int:
    if x == 1: # This is the base case
        return 1
    else: # This is the recursive case
        return (x * await factorial(x-1))

2. Recursive_Function Endpoint

This endpoint receives the number as a string, converts it to an integer, and calls the factorial function asynchronously.

    If the input is not a string, it raises a TypeError.
    The factorial of the number is calculated using the factorial function and returned in a dictionary.

python

@app.get("/items/")
async def Recursive_Function(number:str="0") -> dict:
    if not isinstance(number,str):
        raise TypeError("\n\n An ERROR occur...!!!")
    else:
        n = int(number)
        fact = await factorial(n)
        return {"result":fact}

Error Handling

    TypeError: If the input number is not a string, the application raises a TypeError and stops execution.

Example Error Response

json

{
  "detail": "An ERROR occur...!!!"
}

How the Application Works

    The application starts a FastAPI web server using Uvicorn.
    The /items/ endpoint takes a number as a string parameter.
    The number is passed to the recursive factorial function asynchronously.
    The function calculates the factorial using recursion.
    The result is returned as a JSON response.

License

This project is licensed under the MIT License.

css


This `README.md` file provides a detailed explanation of the FastAPI project, including how it works, its features, API details, and sample outputs.



---
---
---

Author : babak yousefian
