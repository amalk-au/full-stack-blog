# Full Stack Blog — Frontend

The frontend application for [Full Stack Blog](https://github.com/amalk-au/full-stack-blog), built with React, JavaScript, and Vite.

The application provides two separate client interfaces: **Blog Reader** and **Blog Writer**. Both communicate with a centralised REST API built with Node.js and Express.js.

The frontend implements client-side routing, JWT-based authentication, protected routes, and role-based access to application functionality.

## Live Application

**Website:**[https://amalk.au](https://amalk.au)

**Full Stack Blog:**[https://amalk.au/full-stack-blog](https://amalk.au/full-stack-blog)

### Application Navigation

| Page        | Description                                  | Link                                                   |
| ----------- | -------------------------------------------- | ------------------------------------------------------ |
| Home        | Application homepage                         | [Home](https://amalk.au/full-stack-blog)               |
| Blog Reader | Browse published posts and manage comments   | [Blog Reader](https://amalk.au/full-stack-blog/reader) |
| Blog Writer | Create, edit, publish, and manage blog posts | [Blog Writer](https://amalk.au/full-stack-blog/writer) |
| Login       | Authenticate as a writer                     | [Login](https://amalk.au/full-stack-blog/login)        |
| Logout      | Log out and return to the homepage           | [Logout](https://amalk.au/full-stack-blog)             |

**Backend API:**[https://full-stack-blog-t1n4.onrender.com](https://full-stack-blog-t1n4.onrender.com)

> **Authentication notice:** If you see `No JWT Found in Local Storage`, the application cannot find an authentication token in the browser's local storage. Log in to access protected writer functionality.

---

## Table of Contents

- [Overview](#overview)

- [Features](#features)

- [Technology Stack](#technology-stack)

- [Application Architecture](#application-architecture)

- [Project Structure](#project-structure)

- [Getting Started](#getting-started)

- [Package Management](#package-management)

- [Running the Application](#running-the-application)

- [Available Scripts](#available-scripts)

- [Application Routing](#application-routing)

- [Authentication and Authorization](#authentication-and-authorization)

- [Backend Integration](#backend-integration)

- [Building for Production](#building-for-production)

- [Deployment](#deployment)

- [GitHub Pages Routing Considerations](#github-pages-routing-considerations)

- [Troubleshooting](#troubleshooting)

- [Future Improvements](#future-improvements)

- [Source Code](#source-code)

- [Author](#author)

---

## Overview

The frontend is a React single-page application (SPA) that provides the user interface for the Full Stack Blog platform.

It communicates with the backend REST API to retrieve and manage application data, including users, blog posts, and comments.

The application is divided into two primary client experiences:

### Blog Reader

The Blog Reader provides a content-reading interface.

Users can:

- Browse published blog posts.

- View individual blog posts.

- Retrieve comments associated with blog posts.

- Create comments.

- Edit existing comments.

- Delete comments.

### Blog Writer

The Blog Writer provides content management functionality for authenticated writers.

Writers can:

- Create blog posts.

- Edit existing blog posts.

- Save posts as drafts.

- View draft posts.

- Publish blog posts.

- Manage publication status.

- Edit comments.

- Delete comments.

---

## Features

### User Interface

- React component-based architecture.

- Client-side navigation using React Router.

- Separate reader and writer interfaces.

- Reusable UI components.

- Responsive application layout.

### Blog Reader

- Retrieve published blog posts from the backend API.

- Display individual blog post content.

- Retrieve associated comments.

- Create, edit, and delete comments.

### Blog Writer

- Create and edit blog posts.

- Manage draft content.

- Publish and unpublish blog posts.

- Retrieve existing drafts.

- Manage comments.

### Authentication

- User registration.

- User login.

- JWT storage in browser local storage.

- Authentication state management.

- Protected application routes.

- Logout functionality.

### API Integration

- HTTP communication with the Express backend.

- JSON request and response handling.

- JWT authentication headers for protected requests.

- Dynamic retrieval and management of application resources.

---

## Technology Stack

### Core Technologies

| Technology         | Purpose                              |
| ------------------ | ------------------------------------ |
| JavaScript         | Application programming language     |
| React 19           | Component-based UI development       |
| React DOM          | Rendering React components           |
| React Router DOM 7 | Client-side routing                  |
| Vite 6             | Development server and build tooling |
| HTML5              | Application structure                |
| CSS3               | Application styling                  |

### Development Tools

| Technology   | Purpose                    |
| ------------ | -------------------------- |
| pnpm         | Package management         |
| ESLint       | JavaScript code linting    |
| Git          | Version control            |
| GitHub Pages | Frontend hosting           |
| gh-pages     | Deployment to GitHub Pages |

### Backend Integration

| Technology | Purpose                          |
| ---------- | -------------------------------- |
| Node.js    | Backend runtime                  |
| Express.js | REST API                         |
| PostgreSQL | Relational database              |
| Prisma ORM | Database access                  |
| JWT        | Authentication and authorisation |

---

## Application Architecture

The frontend follows a component-based architecture using React.

React Router manages client-side navigation, while the frontend communicates with the backend through HTTP requests.

```
                  ┌────────────────────────┐
                  │         Users          │
                  └────────────┬───────────┘
                               │
                  ┌────────────▼───────────┐
                  │      React App         │
                  │                        │
                  │   React Components     │
                  │   React Router         │
                  └────────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
        ┌────────▼────────┐         ┌────────▼────────┐
        │   Blog Reader   │         │   Blog Writer   │
        │                 │         │                 │
        │ Published Posts │         │ Post Management │
        │ Comments        │         │ Drafts           │
        └────────┬────────┘         └────────┬────────┘
                 │                           │
                 └─────────────┬─────────────┘
                               │
                         HTTP / JSON
                               │
                  ┌────────────▼───────────┐
                  │     Express REST API   │
                  │                        │
                  │ Authentication         │
                  │ Authorisation          │
                  │ Posts                  │
                  │ Comments               │
                  └────────────────────────┘
```

### Main Responsibilities

**React components**

Responsible for rendering the application's user interface and managing individual interface elements.

**React Router**

Handles client-side navigation between application pages.

**Authentication**

Manages the frontend authentication state using JWTs stored in browser local storage.

**Backend communication**

Sends HTTP requests to the Express API and processes the returned JSON responses.

---

## Project Structure

The frontend is located in the `frontend` directory of the main repository.

```
frontend/
│
├── public/
│
├── src/
│   ├── assets/
│   │
│   ├── components/
│   │   └── main.jsx
│   │
│   └── ...
│
├── index.html
├── package.json
├── pnpm-lock.yaml
├── vite.config.js
└── eslint.config.js
```

### Main Files and Directories

| File / Directory          | Responsibility                               |
| ------------------------- | -------------------------------------------- |
| `public/`                 | Static assets                                |
| `src/assets/`             | Application assets                           |
| `src/components/`         | React components and application entry point |
| `src/components/main.jsx` | React application entry point                |
| `index.html`              | HTML document loaded by Vite                 |
| `package.json`            | Dependencies and npm-compatible scripts      |
| `pnpm-lock.yaml`          | Locked dependency versions managed by pnpm   |
| `vite.config.js`          | Vite configuration                           |
| `eslint.config.js`        | ESLint configuration                         |

---

## Getting Started

Follow these instructions to run the frontend locally.

### Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/)

- [pnpm](https://pnpm.io/)

- [Git](https://git-scm.com/)

### 1\. Install pnpm

If pnpm is not already installed, enable it using Corepack:

```
corepack enable
corepack prepare pnpm@latest --activate
```

Verify the installation:

```
pnpm --version
```

### 2\. Clone the Repository

```
git clone https://github.com/amalk-au/full-stack-blog.git
```

Navigate into the frontend directory:

```
cd full-stack-blog/frontend
```

### 3\. Install Dependencies

Install the dependencies using pnpm:

```
pnpm install
```

This installs the packages defined in `package.json` and uses `pnpm-lock.yaml` to maintain consistent dependency versions.

---

## Package Management

This project uses **pnpm** for frontend dependency management.

Use pnpm when installing, updating, or executing project dependencies.

### Install Dependencies

```
pnpm install
```

### Add a Production Dependency

```
pnpm add package-name
```

### Add a Development Dependency

```
pnpm add -D package-name
```

### Remove a Dependency

```
pnpm remove package-name
```

### Update Dependencies

```
pnpm update
```

### Run a Package Script

```
pnpm run script-name
```

**Important:** Use `pnpm-lock.yaml` as the dependency lockfile. Avoid mixing npm or Yarn installation commands with pnpm in this project.

---

## Running the Application

### Development Server

Start the Vite development server:

```
pnpm run dev
```

Vite starts the frontend development server.

The default local development address is:

```
http://localhost:5173
```

Open the address in your browser to access the application.

### Development Workflow

A typical development workflow:

1.  Navigate to the frontend directory.

2.  Install dependencies using `pnpm install`.

3.  Start the development server using `pnpm run dev`.

4.  Make changes to React components and application styles.

5.  Vite provides development updates as files change.

---

## Available Scripts

The frontend defines the following scripts in `package.json`.

| Command            | Description                                     |
| ------------------ | ----------------------------------------------- |
| `pnpm run dev`     | Starts the Vite development server              |
| `pnpm run build`   | Creates an optimised production build           |
| `pnpm run preview` | Previews the production build locally           |
| `pnpm run lint`    | Runs ESLint against the frontend source         |
| `pnpm run deploy`  | Builds and deploys the frontend to GitHub Pages |

### Linting

Run ESLint to identify potential JavaScript issues:

```
pnpm run lint
```

### Production Build

Generate the production build:

```
pnpm run build
```

Vite generates the production-ready frontend files in:

```
dist/
```

### Preview Production Build

To preview the production build locally:

```
pnpm run preview
```

---

## Application Routing

The application uses React Router DOM to manage client-side navigation.

The frontend provides separate routes for reader and writer functionality.

### Main Application Routes

| Route                     | Description          |
| ------------------------- | -------------------- |
| `/full-stack-blog/`       | Application homepage |
| `/full-stack-blog/reader` | Blog Reader          |
| `/full-stack-blog/writer` | Blog Writer          |
| `/full-stack-blog/login`  | Login page           |

The application also includes routes for managing blog posts, drafts, and comments.

### Client-Side Routing

React Router handles navigation without requiring a full browser page reload for every route transition.

This provides a single-page application experience while keeping reader and writer functionality logically separated.

---

## Authentication and Authorization

The frontend integrates with the backend's JWT-based authentication system.

### Authentication Flow

1.  A user submits their login credentials.

2.  The frontend sends the credentials to the backend login endpoint.

3.  The backend validates the credentials.

4.  The backend generates and returns a JWT.

5.  The frontend stores the JWT in browser local storage.

6.  Protected frontend functionality checks for an available authentication token.

7.  Protected API requests include the JWT in the authorization header.

8.  The backend verifies the token before processing protected operations.

### JWT Storage

The frontend stores the authentication token in browser local storage.

The token is used to identify the authenticated user when communicating with protected backend endpoints.

### Protected Routes

Protected application functionality requires an authenticated user.

If no JWT is found in local storage, the frontend displays:

```
No JWT Found in Local Storage
```

The user must log in before accessing the relevant protected functionality.

### Logout

When a user logs out, the frontend removes the JWT from local storage and returns the user to the application homepage.

**Note:** Removing the JWT from browser local storage clears the client-side authentication state. The backend token remains valid until it expires because the current backend implementation does not provide server-side token revocation.

---

## Backend Integration

The frontend communicates with the backend through its REST API.

**Production API:**

```
https://full-stack-blog-t1n4.onrender.com
```

**Local development API:**

```
http://localhost:3000
```

### Main API Resources

The frontend interacts with three primary backend resources:

| Resource   | Functionality                                        |
| ---------- | ---------------------------------------------------- |
| Users      | Registration and authentication                      |
| Blog Posts | Retrieving, creating, editing, and publishing posts  |
| Comments   | Retrieving, creating, editing, and deleting comments |

### HTTP Methods

The frontend uses standard HTTP methods to communicate with the backend:

| Method   | Purpose                                               |
| -------- | ----------------------------------------------------- |
| `GET`    | Retrieve application resources                        |
| `POST`   | Create resources or submit authentication credentials |
| `PUT`    | Update existing resources                             |
| `DELETE` | Remove resources                                      |

### JWT Authorization Header

Protected API requests include the JWT in the HTTP authorization header:

```
Authorization: Bearer YOUR_JWT_TOKEN
```

### Backend Repository

For backend architecture, API endpoint definitions, authentication middleware, database configuration, and Prisma schema documentation, see:

[Full Stack Blog — Backend](https://github.com/amalk-au/full-stack-blog/tree/main/backend)

---

## Building for Production

The frontend uses Vite to generate an optimised production build.

Run:

```
pnpm run build
```

Vite creates the production files in the `dist/` directory.

The generated build contains the static assets required to serve the React application.

### Vite Base Configuration

The application is deployed under the `/full-stack-blog/` GitHub Pages path.

The Vite configuration uses:

```
export default defineConfig({
  plugins: [react()],
  base: '/full-stack-blog/'
})
```

The `base` configuration ensures that production asset paths resolve correctly when the application is hosted under a subdirectory.

---

## Deployment

The frontend is deployed to GitHub Pages using the `gh-pages` package.

### Deployment Configuration

| Setting              | Value                      |
| -------------------- | -------------------------- |
| Repository           | `amalk-au/full-stack-blog` |
| Branch               | `main`                     |
| Hosting              | GitHub Pages               |
| Build Tool           | Vite                       |
| Deployment Package   | gh-pages                   |
| Production Base Path | `/full-stack-blog/`        |

### Deploying with pnpm

Navigate into the frontend directory:

```
cd frontend
```

Run the deployment command:

```
pnpm run deploy
```

The deployment process:

1.  Runs the configured pre-deployment script.

2.  Builds the React application using Vite.

3.  Generates the production files in `dist/`.

4.  Publishes the contents of `dist/` to GitHub Pages using `gh-pages`.

### Deployment Script Configuration

The frontend currently defines these scripts:

```
{
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist",
  "build": "vite build"
}
```

To keep the deployment workflow consistently using pnpm, the `predeploy` script can be configured as:

```
{
  "predeploy": "pnpm run build",
  "deploy": "gh-pages -d dist",
  "build": "vite build"
}
```

Once updated, running:

```
pnpm run deploy
```

will execute the production build and deployment using pnpm.

### Production URL

The deployed application is available at:

[https://amalk.au/full-stack-blog](https://amalk.au/full-stack-blog)

---

## GitHub Pages Routing Considerations

The application uses React Router for client-side routing.

GitHub Pages primarily serves static files and does not automatically resolve all client-side routes.

Consequently, refreshing a nested route or opening a nested URL directly may result in a 404 response.

For example:

```
https://amalk.au/full-stack-blog/reader
```

If this occurs, navigate to the application homepage:

[https://amalk.au/full-stack-blog](https://amalk.au/full-stack-blog)

Then use the application's internal navigation.

This is a hosting limitation associated with client-side routing on GitHub Pages rather than a problem with React Router itself.

---

## Troubleshooting

### `pnpm: command not found`

This indicates that pnpm is not installed or is not available in the system PATH.

**Solution:**

Enable Corepack and activate pnpm:

```
corepack enable
corepack prepare pnpm@latest --activate
```

Verify:

```
pnpm --version
```

### Dependency Installation Errors

If dependency installation fails, make sure you are running the command from the frontend directory.

```
cd frontend
pnpm install
```

If dependencies become inconsistent, remove `node_modules` and reinstall:

```
rm -rf node_modules
pnpm install
```

### Frontend Routes Return 404

GitHub Pages does not automatically support all client-side routes.

**Solution:**

Return to the application homepage and navigate using the application's internal navigation links.

### Backend Requests Take a Long Time

The Render free instance may spin down after inactivity.

**Solution:**

Allow additional time for the first request. Subsequent requests may respond faster once the backend is running.

### `No JWT Found in Local Storage`

This notice indicates that the application cannot find an authentication token in browser local storage.

**Solution:**

Log in through the application's login page before accessing protected functionality.

### CORS Errors

The frontend and backend run on different origins.

The backend must allow the frontend origin through its CORS configuration.

For local development:

```
http://localhost:5173
```

For production:

```
https://amalk.au
```

---

## Future Improvements

Potential improvements to the frontend include:

- Improve application-wide state management.

- Centralise API request handling.

- Improve loading and error states.

- Add comprehensive frontend testing.

- Improve form validation and user feedback.

- Improve accessibility and keyboard navigation.

- Implement more robust authentication state handling.

- Improve client-side routing and GitHub Pages fallback behaviour.

- Improve responsive layouts across different screen sizes.

---

## Source Code

The frontend source code is maintained in the main Full Stack Blog repository.

| Component       | Repository                                                                 |
| --------------- | -------------------------------------------------------------------------- |
| Main repository | [full-stack-blog](https://github.com/amalk-au/full-stack-blog)             |
| Frontend        | [frontend](https://github.com/amalk-au/full-stack-blog/tree/main/frontend) |
| Backend         | [backend](https://github.com/amalk-au/full-stack-blog/tree/main/backend)   |

---

## Author : Amal K.

Full Stack Software Engineer

- Website: [https://amalk.au](https://amalk.au)

- GitHub: [amalk-au](https://github.com/amalk-au)

- Full Stack Blog: [GitHub Repository](https://github.com/amalk-au/full-stack-blog)

---

**Developed by Amal K. (2025)**

[https://amalk.au](https://amalk.au)
