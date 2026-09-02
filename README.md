# Student Management API

A simple FastAPI application for viewing, searching, sorting, and creating student records stored in `students.json`.

## Requirements

- Python 3.9 or newer
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

From the project directory, start the development server:

```bash
uvicorn main:app --reload
```

The API will be available at `http://127.0.0.1:8000`.

Interactive API documentation is available at:

- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

## Endpoints

| Method | Endpoint                        | Description                            |
| ------ | ------------------------------- | -------------------------------------- |
| GET    | `/`                             | Check that the API is running          |
| GET    | `/about`                        | View a short description of the API    |
| GET    | `/view`                         | View all students                      |
| GET    | `/view/{student_id}`            | View one student, such as `/view/s001` |
| GET    | `/sort?sorted_by=age&order=asc` | Sort students by a supported field     |
| POST   | `/create`                       | Add a student record                   |

The sort endpoint accepts `age`, `class`, `roll`, `Math marks`, `English marks`, or `Science marks` and supports `asc` or `desc` order.

## Data format

Students are stored in `students.json` using IDs as keys:

```json
{
    "s001": {
        "roll": 1,
        "name": "Alice Johnson",
        "age": 15,
        "email": "alice.johnson@example.com",
        "class": "Grade 10",
        "math marks": 72,
        "english marks": 88,
        "science marks": 81
    }
}
```

When creating a student, include an `id` in the request body. The API uses it as the JSON key and removes it from the stored student object.
