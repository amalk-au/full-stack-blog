# Full Stack Blog — Backend

The backend API for [Full Stack Blog](https://github.com/amalk-au/full-stack-blog), a full-stack blogging application built with Node.js, Express.js, PostgreSQL, and Prisma ORM.

It provides RESTful endpoints for user registration, authentication, blog post management, and comments. JWT-based authentication and role-based access control (RBAC) protect restricted operations and writer functionality.

## Live Application

- **Frontend:** [Full Stack Blog](https://www.amalk.au/full-stack-blog)

- **Backend API:** [https://full-stack-blog-t1n4.onrender.com](https://full-stack-blog-t1n4.onrender.com)

- **Database:**[Neon](https://neon.tech/)

> **Hosting notice:** The backend is hosted on Render's free instance, which may spin down after periods of inactivity. The first request after inactivity can take 50 seconds or longer to complete.

---

## Table of Contents

- [Overview](#overview)

- [Features](#features)

- [Technology Stack](#technology-stack)

- [Architecture](#architecture)

- [Project Structure](#project-structure)

- [Getting Started](#getting-started)

- [Environment Variables](#environment-variables)

- [Database Setup](#database-setup)

- [Running the Server](#running-the-server)

- [API Documentation](#api-documentation)

- [Authentication and Authorization](#authentication-and-authorization)

- [Database Schema](#database-schema)

- [Deployment](#deployment)

- [Error Handling](#error-handling)

- [Author](#author)

---

## Overview

The backend is built with Express.js and provides a RESTful API consumed by two frontend clients:

- **Blog Reader:** Retrieves published blog posts and allows users to manage comments.

- **Blog Writer:** Provides authenticated writers with functionality to create, edit, publish, and manage blog posts.

The API uses PostgreSQL for persistent data storage and Prisma ORM for database queries and relational data management.

The application implements JWT-based authentication to identify authenticated users and role-based access control to restrict writer operations to authorised users.

### Main Responsibilities

- Handle user registration and login.

- Authenticate users using JSON Web Tokens.

- Verify JWTs on protected endpoints.

- Enforce writer permissions.

- Retrieve and manage blog posts.

- Create, retrieve, update, and delete comments.

- Manage relational data using Prisma ORM.

- Return JSON responses to frontend clients.

---

## Features

### User Authentication

- User registration.

- User login.

- Password hashing using `bcryptjs`.

- JWT generation and verification.

- Token expiration.

- Protected API endpoints.

### Role-Based Access Control

The application distinguishes between readers and writers.

- Readers can access published content and manage comments.

- Writers can manage blog posts and publication status.

- Writer endpoints require a valid JWT and author privileges.

### Blog Post Management

- Retrieve all published blog posts.

- Retrieve individual blog posts.

- Create new blog posts.

- Save and update drafts.

- Retrieve draft posts.

- Delete blog posts.

- Publish and unpublish blog posts.

### Comment Management

- Retrieve comments associated with a blog post.

- Create comments.

- Update comments.

- Delete comments.

---

## Technology Stack

| Technology     | Purpose                                |
| -------------- | -------------------------------------- |
| Node.js        | JavaScript runtime                     |
| Express.js     | HTTP server and REST API framework     |
| PostgreSQL     | Relational database                    |
| Prisma ORM     | Database access and data modelling     |
| JSON Web Token | Authentication and token verification  |
| bcryptjs       | Password hashing and comparison        |
| Passport       | Authentication middleware dependency   |
| passport-jwt   | JWT authentication strategy dependency |
| CORS           | Cross-origin resource sharing          |
| dotenv         | Environment variable configuration     |
| Postman        | API testing                            |

### Main Dependencies

| Package          | Purpose                          |
| ---------------- | -------------------------------- |
| `express`        | HTTP server and routing          |
| `@prisma/client` | Prisma database client           |
| `prisma`         | Prisma CLI and schema management |
| `bcryptjs`       | Password hashing                 |
| `jsonwebtoken`   | JWT creation and verification    |
| `cors`           | CORS configuration               |
| `dotenv`         | Environment configuration        |

---

## Architecture

The backend follows a client-server architecture. Frontend applications communicate with the Express API through HTTP requests, while Prisma ORM handles database operations against PostgreSQL.

```
                  ┌──────────────────────┐
                  │    Frontend Clients  │
                  │                      │
                  │    Blog Reader       │
                  │    Blog Writer       │
                  └──────────┬───────────┘
                             │
                         HTTP / JSON
                             │
                  ┌──────────▼───────────┐
                  │      Express.js     │
                  │       API Server     │
                  └──────────┬───────────┘
                             │
                  ┌──────────▼───────────┐
                  │      API Routers     │
                  │                      │
                  │   Main Router        │
                  │   Reader Router      │
                  │   Writer Router      │
                  └──────────┬───────────┘
                             │
                  ┌──────────▼───────────┐
                  │   Controllers        │
                  │                      │
                  │   Authentication     │
                  │   Blog Posts         │
                  │   Comments           │
                  └──────────┬───────────┘
                             │
                  ┌──────────▼───────────┐
                  │ Authentication       │
                  │ Middleware           │
                  │                      │
                  │ JWT Verification     │
                  │ Author Permissions   │
                  └──────────┬───────────┘
                             │
                  ┌──────────▼───────────┐
                  │      Prisma ORM      │
                  └──────────┬───────────┘
                             │
                  ┌──────────▼───────────┐
                  │     PostgreSQL       │
                  └──────────────────────┘
```

### Request Lifecycle

1.  A frontend client sends an HTTP request to an API endpoint.

2.  Express routes the request to the appropriate controller.

3.  Protected routes execute authentication middleware.

4.  The JWT is verified and the authenticated user's information is attached to the request.

5.  Writer routes additionally verify author permissions.

6.  Controllers interact with the database through Prisma queries.

7.  The API returns a JSON response to the client.

---

## Project Structure

```
backend/
│
├── src/
│   ├── controllers/
│   │   ├── blogMainControllerMain.js
│   │   ├── blogReadController.js
│   │   └── blogWriteController.js
│   │
│   ├── middleware/
│   │   └── authenticator.js
│   │
│   ├── prisma/
│   │   ├── schema.prisma
│   │   ├── prismaQueries.js
│   │   └── seedSampleData.js
│   │
│   ├── routes/
│   │   ├── blogMainRouter.js
│   │   ├── blogReaderRouter.js
│   │   └── blogWriterRouter.js
│   │
│   └── index.js
│
├── .env
├── package.json
└── package-lock.json
```

### Directory Responsibilities

| Directory / File   | Responsibility                                       |
| ------------------ | ---------------------------------------------------- |
| `src/controllers/` | Handles incoming requests and application operations |
| `src/middleware/`  | JWT authentication and authorisation middleware      |
| `src/prisma/`      | Prisma schema, database queries, and seed data       |
| `src/routes/`      | Express route definitions                            |
| `src/index.js`     | Express application configuration and server startup |
| `package.json`     | Dependencies and npm scripts                         |

---

## Getting Started

### Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/)

- npm

- [PostgreSQL](https://www.postgresql.org/) or a hosted PostgreSQL database

- [Git](https://git-scm.com/)

### 1\. Clone the Repository

```
git clone https://github.com/amalk-au/full-stack-blog.git
```

Navigate into the backend directory:

```
cd full-stack-blog/backend
```

### 2\. Install Dependencies

```
pnpm install
```

### 3\. Configure Environment Variables

Create a `.env` file in the backend directory:

```
CORS_URL=http://localhost:5173
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=public"
PORT=3000
JWT_SECRET_KEY=your_jwt_secret_key
```

Replace the database connection details and JWT secret with your own values.

See [Environment Variables](#environment-variables) for details.

---

## Environment Variables

The backend requires the following environment variables:

| Variable         | Description                                           |
| ---------------- | ----------------------------------------------------- |
| `CORS_URL`       | Frontend origin allowed to make cross-origin requests |
| `DATABASE_URL`   | PostgreSQL database connection string                 |
| `PORT`           | Port used by the Express server                       |
| `JWT_SECRET_KEY` | Secret key used to sign and verify JWTs               |

### Local Development Example

```
CORS_URL=http://localhost:5173
DATABASE_URL="postgresql://postgres:password@localhost:5432/full_stack_blog?schema=public"
PORT=3000
JWT_SECRET_KEY=replace_with_a_secure_secret
```

### Production Example

```
CORS_URL=https://www.amalk.au
DATABASE_URL=your_neon_database_connection_string
PORT=3000
JWT_SECRET_KEY=your_production_jwt_secret
```

**Security considerations:**

- Never commit `.env` files to source control.

- Do not expose database credentials or JWT secrets.

- Use a strong, unique JWT secret in production.

- Configure environment variables through your hosting provider.

- Use HTTPS for production API communication.

---

## Database Setup

The application uses PostgreSQL with Prisma ORM.

The Prisma schema is located at:

```
src/prisma/schema.prisma
```

### 1\. Generate Prisma Client

From the backend directory, run:

```
npx prisma generate --schema=src/prisma/schema.prisma
```

This generates Prisma Client based on the database schema.

### 2\. Synchronise the Database Schema

```
npx prisma db push --schema=src/prisma/schema.prisma
```

This synchronises the Prisma schema with the configured PostgreSQL database.

### 3\. Seed the Database

```
pnpm run seed
```

The seed script creates sample users, blog posts, and comments.

### 4\. Open Prisma Studio

To inspect database records through Prisma Studio:

```
pnpm run studio
```

Prisma Studio provides a browser-based interface for viewing and managing database records.

> **Note:** The seed script contains predefined sample data. Review the seed implementation before running it against a production database.

---

## Running the Server

The backend uses native Node.js ES modules.

The available npm scripts are:

| Command           | Description                                |
| ----------------- | ------------------------------------------ |
| `pnpm run dev`    | Starts the server using Node.js watch mode |
| `pnpm start`      | Starts the server                          |
| `pnpm run seed`   | Executes the database seed script          |
| `pnpm run studio` | Opens Prisma Studio                        |

### Development Mode

```
pnpm run dev
```

The development server restarts automatically when watched files change.

### Production Mode

```
pnpm start
```

The server uses the configured `PORT` environment variable. If `PORT` is not provided, the application defaults to port `4000`.

The API will be available at:

```
http://localhost:3000
```

When using the default port without setting `PORT`:

```
http://localhost:4000
```

---

## API Documentation

The backend exposes RESTful endpoints for authentication, blog posts, and comments.

All API responses use JSON.

### Base URLs

**Local development:**

```
http://localhost:3000
```

**Production:**

```
https://full-stack-blog-t1n4.onrender.com
```

Append the relevant endpoint to the base URL when making requests.

### 1\. Main / Authentication Routes

| Method | Endpoint    | Description                                          | Authentication |
| ------ | ----------- | ---------------------------------------------------- | -------------- |
| `GET`  | `/`         | Returns API welcome information and available routes | No             |
| `POST` | `/register` | Registers a new user                                 | No             |
| `POST` | `/login`    | Authenticates a user and returns a JWT               | No             |
| `POST` | `/logout`   | Returns logout route response                        | No             |

#### Register

```
POST /register
```

Example request body:

```
{
  "user_email": "user@example.com",
  "user_name": "exampleuser",
  "password": "your_password"
}
```

Newly registered users are assigned reader privileges by default.

#### Login

```
POST /login
```

Example request body:

```
{
  "user_email": "user@example.com",
  "user_name": "exampleuser",
  "password": "your_password"
}
```

Successful authentication returns a JWT.

Example response structure:

```
{
  "Login": "Login Successful",
  "token": "YOUR_JWT_TOKEN"
}
```

### 2\. Reader Routes

Reader routes provide access to published blog posts and comment functionality.

| Method   | Endpoint                               | Description                      | Authentication |
| -------- | -------------------------------------- | -------------------------------- | -------------- |
| `GET`    | `/reader`                              | Returns reader route information | No             |
| `GET`    | `/reader/posts`                        | Retrieves published blog posts   | No             |
| `GET`    | `/reader/posts/:id`                    | Retrieves an individual post     | No             |
| `GET`    | `/reader/posts/:id/comment`            | Retrieves comments for a post    | No             |
| `POST`   | `/reader/posts/:id/comment/create`     | Creates a comment                | Yes            |
| `PUT`    | `/reader/posts/:id/comment/:id/update` | Updates a comment                | Yes            |
| `DELETE` | `/reader/posts/:id/comment/:id/delete` | Deletes a comment                | Yes            |

### 3\. Writer Routes

Writer routes provide blog management functionality.

All writer management operations require:

- A valid JWT.

- Author privileges.

| Method   | Endpoint                    | Description                      | Authentication |
| -------- | --------------------------- | -------------------------------- | -------------- |
| `GET`    | `/writer`                   | Returns writer route information | No             |
| `POST`   | `/writer/posts/create`      | Creates a new blog post          | JWT + Author   |
| `GET`    | `/writer/posts/drafts`      | Retrieves all drafts             | JWT + Author   |
| `GET`    | `/writer/posts/:id/drafts`  | Retrieves a draft by ID          | JWT + Author   |
| `PUT`    | `/writer/posts/:id/drafts`  | Updates a draft                  | JWT + Author   |
| `DELETE` | `/writer/posts/:id/delete`  | Deletes a blog post              | JWT + Author   |
| `PUT`    | `/writer/posts/:id/publish` | Toggles publication status       | JWT + Author   |

### API Authentication Header

Protected endpoints require the JWT to be sent in the HTTP authorization header.

```
Authorization: Bearer YOUR_JWT_TOKEN
```

Example:

```
GET /writer/posts/drafts
Authorization: Bearer YOUR_JWT_TOKEN
```

### Example Blog Post Response

An example response containing published blog posts:

```
{
  "data": [
    {
      "id": 1,
      "blog_post_title": "Example Blog Post",
      "blog_post_content": "This is an example blog post.",
      "blog_post_publish_status": true,
      "blog_post_publish_timestamp": "2025-01-01T10:00:00.000Z",
      "blog_post_author_id": 1
    }
  ]
}
```

### Testing API Endpoints

Use [Postman](https://www.postman.com/) to test the API.

Recommended testing workflow:

1.  Register a user using `POST /register`.

2.  Log in using `POST /login`.

3.  Obtain the JWT from the login response.

4.  Include the JWT in the `Authorization` header.

5.  Test protected reader and writer endpoints.

6.  Verify the returned JSON responses and HTTP status codes.

---

## Authentication and Authorization

The backend uses JSON Web Tokens (JWT) to authenticate users and restrict access to protected resources.

### JWT Generation

When a user successfully logs in, the backend generates a signed JWT containing user-related information.

The token payload includes:

- `userName`

- `status`

- `author`

- `UserID`

The token is signed using `JWT_SECRET_KEY` and configured with an expiration time of 1,800 seconds (30 minutes).

### Authentication Middleware

The `authenticateJWT` middleware:

1.  Extracts the JWT from the `Authorization` header.

2.  Verifies the token using `JWT_SECRET_KEY`.

3.  Rejects requests without a token.

4.  Rejects invalid or expired tokens.

5.  Attaches decoded authentication information to `req.authData`.

6.  Passes valid requests to the next middleware or controller.

### Authorisation Middleware

The `checkAuthorStatus` middleware checks the authenticated user's `author` property.

If `author` is `true`, the request proceeds.

Otherwise, the request is rejected.

### Access Control Overview

| Operation                 | Reader        | Writer        |
| ------------------------- | ------------- | ------------- |
| View published posts      | Yes           | Yes           |
| View post details         | Yes           | Yes           |
| Retrieve comments         | Yes           | Yes           |
| Create comments           | Authenticated | Authenticated |
| Update comments           | Authenticated | Authenticated |
| Delete comments           | Authenticated | Authenticated |
| Create blog posts         | No            | Yes           |
| Manage drafts             | No            | Yes           |
| Delete blog posts         | No            | Yes           |
| Publish / unpublish posts | No            | Yes           |

### Logout

The logout endpoint is available at:

```
POST /logout
```

The frontend removes the JWT from local storage when the user logs out.

The current backend logout route returns a response but does not implement server-side token revocation. The JWT remains valid until it expires.

---

## Database Schema

The application uses PostgreSQL with Prisma ORM.

The Prisma schema defines three primary models:

- `BlogUsers`

- `BlogContent`

- `BlogComments`

### BlogUsers

Stores registered user information.

| Field        | Type    | Description                                      |
| ------------ | ------- | ------------------------------------------------ |
| `id`         | Int     | Primary key                                      |
| `user_email` | String  | Unique email address                             |
| `user_name`  | String  | Unique username                                  |
| `password`   | String  | Hashed password                                  |
| `author`     | Boolean | Indicates whether the user has writer privileges |

### BlogContent

Stores blog post information.

| Field                         | Type     | Description                        |
| ----------------------------- | -------- | ---------------------------------- |
| `id`                          | Int      | Primary key                        |
| `blog_post_title`             | String   | Blog post title                    |
| `blog_post_content`           | String   | Blog post content                  |
| `blog_post_publish_status`    | Boolean  | Publication status                 |
| `blog_post_publish_timestamp` | DateTime | Publication timestamp              |
| `blog_post_author_id`         | Int      | Foreign key referencing the author |

### BlogComments

Stores comments associated with blog posts and users.

| Field               | Type     | Description                                |
| ------------------- | -------- | ------------------------------------------ |
| `id`                | Int      | Primary key                                |
| `comment_text`      | String   | Comment content                            |
| `comment_timestamp` | DateTime | Comment timestamp                          |
| `blog_post_id`      | Int      | Foreign key referencing a blog post        |
| `comment_author_id` | Int      | Foreign key referencing the comment author |

### Entity Relationships

```
BlogUsers
   │
   ├───────────────< BlogContent
   │                      │
   │                      │
   │                      └────────< BlogComments
   │
   └───────────────────────────────< BlogComments
```

Relationship overview:

- A user can create multiple blog posts.

- A user can create multiple comments.

- A blog post can have multiple comments.

- Deleting a related user or blog post cascades to associated records according to the Prisma schema.

---

## Deployment

The backend is deployed using [Render](https://render.com/), with PostgreSQL hosted on [Neon](https://neon.tech/).

### Render Configuration

| Setting        | Value                      |
| -------------- | -------------------------- |
| Repository     | `amalk-au/full-stack-blog` |
| Branch         | `main`                     |
| Root Directory | `backend`                  |
| Build Command  | `npm install`              |
| Start Command  | `npm start`                |

The root directory should be `backend` because this is where the backend `package.json` is located.

### Production Environment Variables

Configure the following environment variables in the Render dashboard:

```
CORS_URL=https://www.amalk.au
DATABASE_URL=your_neon_database_connection_string
PORT=3000
JWT_SECRET_KEY=your_production_jwt_secret
```

### Database Hosting

The production PostgreSQL database is hosted on Neon.

1.  Create a PostgreSQL database through Neon.

2.  Obtain the database connection string.

3.  Configure the connection string as `DATABASE_URL` in Render.

4.  Ensure the Prisma schema is synchronised with the production database.

---

## Error Handling

The Express application includes a global error-handling middleware.

Unhandled errors are logged on the server and return a JSON response.

Example response:

```
{
  "message": "Something Went Wrong !",
  "error": "Error details"
}
```

Authentication middleware also returns responses for missing, invalid, or expired JWTs.

| HTTP Status | Description                                                    |
| ----------- | -------------------------------------------------------------- |
| `401`       | Authentication token missing or insufficient author privileges |
| `403`       | Invalid or expired JWT                                         |
| `500`       | Internal server error                                          |

---

## Author : Amal K.

- Portfolio: [amalk.au](https://www.amalk.au)

- GitHub: [amalk-au](https://github.com/amalk-au)

- Main Project: [Full Stack Blog](https://github.com/amalk-au/full-stack-blog)

---

**Developed by Amal Kariyawasam (2025)**

[amalk.au](https://amalk.au)
