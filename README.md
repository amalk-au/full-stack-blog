# Full Stack Blog

A full-stack blogging application built with React, Node.js, Express, and PostgreSQL. The application features a RESTful API, JWT-based authentication, protected routes, and role-based access control (RBAC), with separate interfaces for readers and writers.

## Live Demo

**Frontend:** [Blog Frontend](https://amalk.au/full-stack-blog)

**Backend API:** [Blog Backend API](https://full-stack-blog-t1n4.onrender.com/)

> **Authentication notice:** If you see `No JWT Found in Local Storage`, you are not currently authenticated. Log in to access protected writer functionality.

## Screenshots

### Blog Reader

![blog-reader-main](./documentation/screenshots/blog-reader-main.png)
![blog-reader-view-post](./documentation/screenshots/blog-reader-view-post.png)

### Authentication

![sign-in](./documentation/screenshots/sign-in.png)
![register-user](./documentation/screenshots/register-user.png)
![json-web-token](./documentation/screenshots/json-web-token.png)

### Blog Writer

![blog-writer-main](./documentation/screenshots/blog-writer-main.png)
![blog-writer-comments](./documentation/screenshots/blog-writer-comments.png)
![blog-writer-drafts](./documentation/screenshots/blog-writer-drafts.png)
![blog-writer-edit-post](./documentation/screenshots/blog-writer-edit-post.png)

### Online Documentation

![Documentation 1](./documentation/screenshots/doc-1.png)
![Documentation 2](./documentation/screenshots/doc-2.png)
![Documentation 3](./documentation/screenshots/doc-3.png)
![Documentation 4](./documentation/screenshots/doc-4.png)
![Documentation 5](./documentation/screenshots/doc-5.png)
![Documentation 6](./documentation/screenshots/doc-6.png)

### Deployment

The application is deployed using the following services:

| Component | Service                       |
| --------- | ----------------------------- |
| Frontend  | GitHub Pages                  |
| Backend   | [Render](https://render.com/) |
| Database  | [Neon](https://neon.tech/)    |

**Deployment considerations:**

- The backend is hosted on Render's free instance, which may spin down after periods of inactivity.

- The first request after inactivity can take 60 seconds or longer to complete.

- Neon and Render free tiers may have performance limitations, so initial requests can be slower than expected.

### GitHub Pages Routing Notice

The frontend uses client-side routing. GitHub Pages does not automatically handle all client-side routes.

Refreshing a nested route or opening one directly may result in a 404 error. If this happens, navigate to the application homepage and use the application's internal navigation links.

---

## Table of Contents

- [Project Overview](#project-overview)

- [Technical Implementation](#technical-implementation)

- [Features](#features)

- [Technology Stack](#technology-stack)

- [Application Architecture](#application-architecture)

- [Getting Started](#getting-started)

- [Environment Variables](#environment-variables)

- [Database Setup](#database-setup)

- [Running the Application](#running-the-application)

- [API Documentation](#api-documentation)

- [Authentication and Authorization](#authentication-and-authorization)

- [Deployment](#deployment)

- [Troubleshooting](#troubleshooting)

- [Future Improvements](#future-improvements)

- [Source Code](#source-code)

- [Author](#author)

---

## Project Overview

Full Stack Blog is a full-stack blogging application that provides a content management experience through two separate frontend clients: Blog Reader and Blog Writer.

The application follows a client-server architecture, with the frontend applications communicating with a centralised backend through a RESTful API.

The backend manages users, blog posts, comments, authentication, and authorisation. PostgreSQL provides relational data storage, while Prisma ORM handles database operations.

The application uses JSON Web Tokens (JWT) for authentication and role-based access control (RBAC) to manage access to protected functionality.

### Application Clients

**Blog Reader**

Provides functionality for users to:

- Browse published blog posts.

- Read individual blog posts.

- View comments associated with posts.

- Create, edit, and delete comments.

**Blog Writer**

Provides content management functionality for authenticated writers to:

- Create blog posts.

- Edit existing blog posts.

- Save posts as drafts.

- View draft posts.

- Publish blog posts.

- Manage publication status.

- Edit and delete comments.

---

## Technical Implementation

The application demonstrates the implementation of a full-stack web application using modern JavaScript technologies and established software development principles.

### RESTful API Design

The backend follows REST principles where applicable:

- **Client-server architecture:** Frontend and backend operate independently and communicate through HTTP requests.

- **Stateless communication:** Each request contains the information required by the server to process it.

- **Resource-based routing:** API endpoints represent resources such as users, posts, and comments.

- **HTTP methods:** Standard methods such as `GET`, `POST`, `PUT`, and `DELETE` represent resource operations.

- **JSON data exchange:** The API uses JSON for request and response payloads.

### Authentication and Authorization

- JWT-based user authentication.

- Token verification for protected endpoints.

- Authentication middleware.

- Role-based access control.

- Restricted access to writer functionality.

### Database Management

- PostgreSQL relational database.

- Prisma ORM for database access.

- Relational data management for users, posts, and comments.

- Prisma schema synchronisation and database seeding.

### Frontend and Backend Integration

- Separate frontend clients for readers and writers.

- Centralised backend API.

- HTTP-based client-server communication.

- JWT-based authentication between frontend and backend.

---

## Features

### Blog Reader

- Browse published blog posts.

- View individual blog posts.

- Retrieve comments associated with posts.

- Create comments.

- Edit existing comments.

- Delete comments.

### Blog Writer

- Create blog posts.

- Edit existing posts.

- Save posts as drafts.

- View draft posts.

- Publish blog posts.

- Manage publication status.

- Edit comments.

- Delete comments.

### Authentication and Authorization

- User registration.

- User login.

- JWT-based authentication.

- Protected routes.

- Role-based access control.

- Client-side JWT storage.

---

## Technology Stack

### Frontend

The frontend is responsible for rendering the user interface and communicating with the backend API.

| Technology | Purpose                                |
| ---------- | -------------------------------------- |
| JavaScript | Application programming language       |
| React      | Component-based UI development         |
| Vite       | Frontend development and build tooling |
| HTML       | Application structure                  |
| CSS        | Application styling                    |

The frontend contains two main client applications:

- **Blog Reader:** Handles reading posts and managing comments.

- **Blog Writer:** Handles post management and comment moderation.

### Backend

The backend provides the REST API and handles application logic, authentication, authorisation, and database operations.

| Technology | Purpose                                      |
| ---------- | -------------------------------------------- |
| Node.js    | JavaScript runtime                           |
| Express.js | Backend web framework                        |
| PostgreSQL | Relational database                          |
| Prisma ORM | Database access and schema management        |
| JWT        | Authentication and token-based authorisation |
| Postman    | API development and testing                  |

### Deployment and Infrastructure

| Service      | Purpose                     |
| ------------ | --------------------------- |
| GitHub Pages | Frontend hosting            |
| Render       | Backend hosting             |
| Neon         | PostgreSQL database hosting |

---

## Application Architecture

The application follows a client-server architecture.

The frontend applications communicate with the backend through HTTP requests. The backend processes requests, interacts with the PostgreSQL database through Prisma ORM, and returns JSON responses.

```
                  ┌──────────────────────┐
                  │        Users         │
                  └──────────┬───────────┘
                             │
                ┌────────────┴────────────┐
                │                         │
       ┌────────▼────────┐       ┌────────▼────────┐
       │   Blog Reader   │       │   Blog Writer   │
       │   React Client  │       │   React Client  │
       └────────┬────────┘       └────────┬────────┘
                │                         │
                └────────────┬────────────┘
                             │
                        HTTP / JSON
                             │
                   ┌─────────▼─────────┐
                   │   Express API     │
                   │   Node.js         │
                   └─────────┬─────────┘
                             │
                  ┌──────────▼──────────┐
                  │ Authentication and  │
                  │ Authorization (JWT) │
                  └──────────┬──────────┘
                             │
                       Prisma ORM
                             │
                   ┌─────────▼─────────┐
                   │    PostgreSQL     │
                   │    Database       │
                   └───────────────────┘
```

### Main Application Resources

The backend manages three primary resources:

- **Users:** Registration, login, and user information.

- **Posts:** Blog post creation, editing, drafts, and publication.

- **Comments:** Creating, editing, and deleting comments associated with posts.

---

## Getting Started

Follow these instructions to run the application locally.

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

Navigate into the project directory:

```
cd full-stack-blog
```

### 2\. Install Frontend Dependencies

```
cd frontend
pnpm install
```

### 3\. Install Backend Dependencies

Open another terminal or return to the project root:

```
cd backend
pnpm install
```

### 4\. Configure Environment Variables

Create a `.env` file in the backend directory.

Add the required environment variables:

```
CORS_URL=http://localhost:5173
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=public"
PORT=3000
JWT_SECRET_KEY=your_jwt_secret_key
```

Replace the database connection details with your PostgreSQL credentials.

See [Environment Variables](#environment-variables) for more information.

---

## Environment Variables

The backend requires the following environment variables.

| Variable         | Description                                             |
| ---------------- | ------------------------------------------------------- |
| `CORS_URL`       | Frontend origin permitted to make cross-origin requests |
| `DATABASE_URL`   | PostgreSQL connection string                            |
| `PORT`           | Port on which the backend server runs                   |
| `JWT_SECRET_KEY` | Secret key used to sign and verify JWTs                 |

### Example

```
CORS_URL=http://localhost:5173
DATABASE_URL="postgresql://postgres:password@localhost:5432/full_stack_blog?schema=public"
PORT=3000
JWT_SECRET_KEY=replace_with_a_secure_secret
```

**Important:**

- Never commit your `.env` file.

- Do not expose your JWT secret.

- Use a strong, unique secret in production.

- Configure production environment variables through your hosting provider.

---

## Database Setup

The application uses PostgreSQL with Prisma ORM.

After configuring the database connection, navigate to the backend directory:

```
cd backend
```

### 1\. Generate Prisma Client

```
npx prisma generate
```

This generates the Prisma Client based on your Prisma schema.

### 2\. Synchronise the Database Schema

```
npx prisma db push
```

This synchronises the database schema with the Prisma schema.

### 3\. Seed the Database

```
npm run seed
```

This runs the project's seed script to populate the database with initial data.

> Make sure your database is running and your `DATABASE_URL` is correct before executing these commands.

---

## Running the Application

The frontend and backend run independently.

### Start the Backend

From the backend directory:

```
pnpm start
```

The backend should be available at:

```
http://localhost:3000
```

### Start the Frontend

From the frontend directory:

```
pnpm run dev
```

Vite will display the local development URL in your terminal. By default, this is commonly:

```
http://localhost:5173
```

Open the frontend URL in your browser.

---

## API Documentation

The backend exposes endpoints for authentication, blog posts, and comments.

The API uses JSON for request and response payloads.

### API Base URLs

**Local development:**

```
http://localhost:3000
```

**Production:**

```
https://full-stack-blog-t1n4.onrender.com
```

Append the relevant endpoint to the base URL when making requests.

For example:

```
http://localhost:3000/writer/posts/create
```

### Authentication Endpoints

| Method | Endpoint    | Description         |
| ------ | ----------- | ------------------- |
| `POST` | `/register` | Register a user     |
| `POST` | `/login`    | Authenticate a user |

Logout is handled on the frontend by removing the JWT from local storage.

### Reader Endpoints

| Method   | Endpoint                               | Description                  |
| -------- | -------------------------------------- | ---------------------------- |
| `GET`    | `/reader`                              | Access the reader interface  |
| `GET`    | `/reader/posts`                        | Retrieve published posts     |
| `GET`    | `/reader/posts/:id`                    | Retrieve an individual post  |
| `GET`    | `/reader/posts/:id/comment`            | Retrieve comments for a post |
| `POST`   | `/reader/posts/:id/comment/create`     | Create a comment             |
| `PUT`    | `/reader/posts/:id/comment/:id/update` | Update a comment             |
| `DELETE` | `/reader/posts/:id/comment/:id/delete` | Delete a comment             |

### Writer Endpoints

| Method   | Endpoint                    | Description                        |
| -------- | --------------------------- | ---------------------------------- |
| `GET`    | `/writer`                   | Access the writer interface        |
| `GET`    | `/writer/posts/create`      | Access the post creation route     |
| `GET`    | `/writer/posts/drafts`      | Retrieve draft posts               |
| `POST`   | `/writer/posts/:id/drafts`  | Create or save a draft             |
| `PUT`    | `/writer/posts/:id/drafts`  | Update a draft                     |
| `DELETE` | `/writer/posts/:id/delete`  | Delete a post                      |
| `PUT`    | `/writer/posts/:id/publish` | Update a post's publication status |

### Example API Response

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

The response contains a `data` array with the published posts and their associated properties.

### Testing API Endpoints

You can use [Postman](https://www.postman.com/) to test the backend endpoints.

When testing protected endpoints:

1.  Register or log in through the authentication endpoints.

2.  Obtain the JWT returned by the login process.

3.  Include the token in the request's authorization header if required by the backend.

4.  Send the request with the appropriate HTTP method and JSON payload.

5.  Inspect the response and status code.

A typical JWT authorization header looks like this:

```
Authorization: Bearer YOUR_JWT_TOKEN
```

---

## Authentication and Authorization

The application uses JSON Web Tokens (JWT) to authenticate users and protect restricted functionality.

### Authentication Flow

1.  A user submits their login credentials.

2.  The backend validates the credentials.

3.  The backend generates a JWT.

4.  The frontend stores the JWT in local storage.

5.  Subsequent protected requests include the token.

6.  The backend verifies the token before allowing access to protected functionality.

### Role-Based Access Control

The application separates reader and writer functionality.

| Role   | Permissions                                         |
| ------ | --------------------------------------------------- |
| Reader | Browse published posts and manage comments          |
| Writer | Manage blog posts, publication status, and comments |

The backend should enforce authorisation independently of frontend navigation. Hiding a frontend route or button is not sufficient protection for a restricted API endpoint.

### Logout

The frontend handles logout by removing the JWT from local storage.

After logout, protected frontend functionality should no longer be accessible without authenticating again.

---

## Deployment

The application is deployed using three services:

- GitHub Pages for the frontend.

- Render for the backend.

- Neon for the PostgreSQL database.

### Frontend Deployment

The frontend is hosted using GitHub Pages.

To deploy the frontend, navigate to the frontend directory:

```
cd frontend
```

Run:

```
pnpm run deploy
```

This executes the project's configured deployment script.

### Backend Deployment

The backend is hosted on Render.

General deployment configuration:

| Setting        | Value                      |
| -------------- | -------------------------- |
| Repository     | `amalk-au/full-stack-blog` |
| Branch         | `main`                     |
| Root Directory | `backend`                  |
| Build Command  | `pnpm install`             |
| Start Command  | `pnpm start`               |

Configure the production environment variables in the Render dashboard.

For example:

```
CORS_URL=https://www.amalk.au
DATABASE_URL=your_neon_database_connection_string
PORT=3000
JWT_SECRET_KEY=your_production_jwt_secret
```

### Database Deployment

The production PostgreSQL database is hosted on [Neon](https://neon.tech/).

Create a database and use its connection string as the production `DATABASE_URL`.

Make sure the deployed backend can connect to the database and that the Prisma schema has been synchronised.

---

## Troubleshooting

### `No JWT Found in Local Storage`

This notice indicates that the frontend cannot find an authentication token in local storage.

**Solution:** Log in through the application's login page before accessing protected functionality.

### Frontend Routes Return 404 on Refresh

GitHub Pages does not automatically support all client-side routes.

**Solution:** Return to the application homepage and navigate using the application's internal links.

### Backend Requests Take a Long Time

The Render free instance may spin down after inactivity.

**Solution:** Allow additional time for the first request. Subsequent requests may respond faster once the backend is running.

### Database Connection Errors

Check the following:

- The PostgreSQL database is running.

- `DATABASE_URL` contains the correct connection details.

- The database credentials are valid.

- The database schema has been synchronised.

- The production backend has the correct database environment variable.

### CORS Errors

Check that `CORS_URL` matches the frontend origin.

**Local development:**

```
CORS_URL=http://localhost:5173
```

**Production:**

```
CORS_URL=https://amalk.au
```

---

## Future Improvements

Potential improvements to the application include:

- Add comprehensive backend API documentation.

- Improve request validation and error handling.

- Add automated unit and integration tests.

- Improve API response consistency.

- Implement pagination for blog posts and comments.

- Improve frontend loading and error states.

- Add more granular role and permission management.

- Improve deployment automation and CI/CD workflows.

---

## Source Code

The source code is organised into separate frontend and backend directories.

| Component       | Repository                                                                 |
| --------------- | -------------------------------------------------------------------------- |
| Main repository | [full-stack-blog](https://github.com/amalk-au/full-stack-blog)             |
| Frontend        | [frontend](https://github.com/amalk-au/full-stack-blog/tree/main/frontend) |
| Backend         | [backend](https://github.com/amalk-au/full-stack-blog/tree/main/backend)   |

---

## Author : Amal K.

- Portfolio: [amalk.au](https://amalk.au)

- GitHub: [amalk-au](https://github.com/amalk-au)

---

**Developed by Amal K. (2025)**

[amalk.au](https://www.amalk.au)
