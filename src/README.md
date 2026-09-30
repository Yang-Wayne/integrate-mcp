# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teachers can register and unregister students after logging in
- Students can view activities and participant lists without logging in

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure the teacher credentials in your environment (do not commit real credentials):

   ```
   export TEACHER_USERNAME='teacher'
   export TEACHER_PASSWORD='replace-with-a-long-random-secret'
   ```

3. Run the application:

   ```
   uvicorn src.app:app --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/teacher-login`                                                  | Validate teacher credentials                                        |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Register a student (teacher authentication required)                 |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)             |

Teacher authentication uses HTTP Basic credentials from environment variables. Use HTTPS in deployments because Basic credentials are not encrypted by themselves. If credentials are not configured, write operations are disabled.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
