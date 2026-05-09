# The Recipe Archive

This is a Spring Boot backend and Svelte/SvelteKit frontend project with a PostgreSQL database for digitizing, storing, and retrieving/viewing family recipes.

## Homepage Screenshot

![Homepage](Home.png)

## Project Overview

The repository contains two main parts:

- `src/` — Java Spring Boot backend that serves REST APIs, persistence, authentication, and business logic.
- `recipearchive-frontend/` — SvelteKit frontend application that consumes the backend APIs and delivers the user experience.

## Prerequisites

- Java 21 SDK
- Maven 3.8+ or the included Maven wrapper (`./mvnw`)
- Node.js 18+ / npm
- PostgreSQL database

## Local Setup

1. Clone the repository.
2. Create a PostgreSQL database for the application.
3. Configure the database connection in `src/main/resources/application-dev.yml` or `src/main/resources/application.properties`.
4. Start the backend and frontend services for development.

## Backend Setup and Run

From the project root:

```bash
./mvnw clean package
./mvnw spring-boot:run
```

The backend starts on `http://localhost:8080` by default.

### Common Commands

- Build: `./mvnw clean package`
- Run: `./mvnw spring-boot:run`
- Test: `./mvnw test`

## Frontend Setup and Run

From the frontend folder:

```bash
cd recipearchive-frontend
npm install
npm run dev
```

The frontend development server typically runs on `http://localhost:5173` and should be configured to point to the backend API.

## Configuration

The backend uses YAML configuration files under `src/main/resources/`:

- `application-dev.yml` — development settings
- `application-prod.yml` — production settings
- `application.properties` / `application.yaml` — shared Spring Boot configuration

Flyway migration scripts are located in `src/main/resources/db/migration/`.

## Database Design

The database uses PostgreSQL and has the following tables and table columns.

### Recipe Table

- Recipe ID: big_serial (primary key)
- User ID: big_int (foreign key)
- Title: varchar(200)
- Description: text
- Ingredients: text
- Instructions: text
- Allergies: text
- Prep Time: int
- Cooking Time: int
- Servings: int
- Created At: timestamp
- Updated At: timestamp

### User Table

- User ID: big_serial (primary key)
- First Name: varchar(50)
- Last Name: varchar(50)
- Username: varchar(50)
- Email: varchar(100)
- Password: varchar(255)
- Created At: timestamp
- Updated At: timestamp

## REST Endpoints

These are the available endpoints served by the Spring Boot server along with the controller names that handle the logic for each endpoint.

| Name                 | Method | Path                   | Controller       |
| -------------------- | ------ | ---------------------- | ---------------- |
| Login                | POST   | /auth/login            | AuthController   |
| Get all recipes      | GET    | /recipes               | RecipeController |
| Get one recipe       | GET    | /recipes/{id}          | RecipeController |
| Get a user's recipes | GET    | /recipes/user/{userId} | RecipeController |
| Create a recipe      | POST   | /recipes               | RecipeController |
| Delete a recipe      | DELETE | /recipes/{id}          | RecipeController |
| Update a recipe      | PUT    | /recipes/{id}          | RecipeController |
| Get all users        | GET    | /users                 | UserController   |
| Get a user           | GET    | /users/{id}            | UserController   |
| Register a user      | POST   | /users                 | UserController   |
| Update a user        | PUT    | /users/{id}            | UserController   |
| Delete a user        | DELETE | /users/{id}            | UserController   |

## Notes

- Use the frontend app to authenticate and manage recipes through the backend APIs.
- Flyway applies database schema migrations automatically when the backend starts.
- The project uses YAML configuration by default, with separate files for development and production profiles.

## Frontend Folder

The frontend source is located in `recipearchive-frontend/` and includes the SvelteKit application, route files, and UI components.

## License

This project includes the `LICENSE` file in the repository root directory.