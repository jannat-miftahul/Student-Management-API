# Student Management API

A FastAPI-based student management system for creating, viewing, updating, deleting, and sorting student records stored in `students.json`.

## Features

- View all students
- View a single student by ID
- Sort students by a supported field
- Create new student records
- Update existing student data
- Delete student records

## Requirements

- Python 3.9+
- FastAPI
- Uvicorn

## Setup

Create and activate a virtual environment, then install the dependencies:

```bash
python -m venv .venv

# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate

pip install fastapi uvicorn
```

## Run the API

From the project root, start the server:

```bash
uvicorn main:app --reload
```

The API runs at:

- `http://127.0.0.1:8000`
- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

## API Endpoints

| Method | Endpoint                        | Description                             |
| ------ | ------------------------------- | --------------------------------------- |
| GET    | `/`                             | Returns a welcome message               |
| GET    | `/about`                        | Returns a short description of the API  |
| GET    | `/view`                         | Lists all students                      |
| GET    | `/view/{student_id}`            | Fetches one student by ID               |
| GET    | `/sort?sorted_by=age&order=asc` | Sorts students by a valid field         |
| POST   | `/create`                       | Creates a new student                   |
| PUT    | `/edit/{student_id}`            | Updates one or more fields of a student |
| DELETE | `/delete/{student_id}`          | Deletes a student                       |

### Supported sort fields

The `sorted_by` query parameter accepts:

- `age`
- `student_class`
- `roll`
- `Math_marks`
- `English_marks`
- `Science_marks`

The `order` query parameter accepts:

- `asc`
- `desc`

## Student schema

The API expects the following student payload format when creating a record:

```json
{
    "id": "s001",
    "name": "Alice Johnson",
    "age": 15,
    "student_class": 10,
    "roll": 1,
    "Math_marks": 72,
    "English_marks": 88,
    "Science_marks": 81,
    "phone": "01700000000"
}
```

### Validation rules

- `age` must be between 1 and 99
- `student_class` must be between 1 and 12
- `roll` must be between 1 and 100
- `Math_marks`, `English_marks`, and `Science_marks` must each be between 1 and 100
- `id` must be unique

## Update payload example

You can send partial data for updates:

```json
{
    "age": 16,
    "phone": "01711111111"
}
```

Only the provided fields are updated.

## Data storage

Student records are stored in `students.json` using student IDs as keys. The API removes the `id` field from the stored object and uses it as the dictionary key.

Example:

```json
{
    "s001": {
        "name": "Alice Johnson",
        "age": 15,
        "student_class": 10,
        "roll": 1,
        "Math_marks": 72,
        "English_marks": 88,
        "Science_marks": 81,
        "phone": "01700000000"
    }
}
```
