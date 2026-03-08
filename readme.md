# NestJS: The Complete Developer's Guide 2025

**Platform:** Udemy  
**Technology:** NestJS  
**Version:** NestJS 7.6.17

---

## Course Overview

This course teaches NestJS from the ground up, starting with building a project from scratch to understand the internal workings of NestJS. The approach focuses on understanding the framework's internals first, making everything else easier and more straightforward as the course progresses.

---

## Section 2: The Basics of Nest

<br>

### 🎬 Lecture 2.1 – Project Setup

---

#### What This Lecture Covers

This lecture covers the initial setup of a NestJS project from scratch, without using the Nest CLI. The purpose is to understand the underlying structure and dependencies that make up a NestJS application.

#### Prerequisites

- Basic knowledge of TypeScript
- General understanding of Node.js fundamentals

#### Project Creation Steps

1. Create a new project directory called `scratch`
2. Generate a `package.json` file using `npm init -y`
3. Install required dependencies

#### Dependencies Installation

```bash
npm install @nestjs/common@7.6.17 @nestjs/core@7.6.17 @nestjs/platform-express@7.6.17 reflect-metadata@0.1.13 typescript@4.3.2
```

#### Understanding the Dependencies

| Dependency                 | Purpose                                                                                      |
| -------------------------- | -------------------------------------------------------------------------------------------- |
| `@nestjs/common`           | Contains the majority of functions, classes, and utilities used to build NestJS applications |
| `@nestjs/core`             | Core NestJS functionality                                                                    |
| `@nestjs/platform-express` | Adapter between Express.js and NestJS for handling HTTP requests                             |
| `reflect-metadata`         | Library tied to decorators functionality                                                     |
| `typescript`               | TypeScript compiler for transpiling code                                                     |

#### Why This Matters

Understanding the dependencies helps clarify that NestJS itself does not handle incoming HTTP requests directly. Instead, it relies on an external HTTP server implementation (Express.js or Fastify) to handle requests and responses.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=600&lines=🎬+Lecture+2.2+–+TypeScript+Configuration" alt="Lecture 2.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to configure TypeScript for a NestJS project by creating a `tsconfig.json` file with the necessary compiler options.

#### TypeScript Configuration File

Create a `tsconfig.json` file in the project root:

```json
{
  "compilerOptions": {
    "module": "CommonJS",
    "target": "ES2017",
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

#### Configuration Options Explained

| Option                   | Value      | Purpose                                   |
| ------------------------ | ---------- | ----------------------------------------- |
| `module`                 | `CommonJS` | Specifies the module system for output    |
| `target`                 | `ES2017`   | JavaScript version target for compilation |
| `experimentalDecorators` | `true`     | Enables decorator syntax support          |
| `emitDecoratorMetadata`  | `true`     | Emits design-type metadata for decorators |

#### Why This Matters

The `experimentalDecorators` and `emitDecoratorMetadata` settings are at the absolute core of what makes NestJS work. Decorators are used extensively throughout NestJS to define controllers, modules, routes, and more.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+2.3+–+Creating+a+Controller" alt="Lecture 2.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces the request-response cycle in HTTP servers and explains the core tools NestJS provides to handle each step of processing incoming requests.

#### The Request-Response Cycle

Every HTTP server follows a similar pattern:

1. Receive a request
2. Validate data in the request
3. Authenticate/authorize the user
4. Route the request to a specific handler
5. Execute business logic
6. Access/store data in a database
7. Formulate and send a response

#### NestJS Tools for Request Handling

| Tool             | Purpose                                   |
| ---------------- | ----------------------------------------- |
| **Pipes**        | Validate data on incoming requests        |
| **Guards**       | Handle authentication and authorization   |
| **Controllers**  | Contain routing logic                     |
| **Services**     | Contain business logic                    |
| **Repositories** | Handle database access                    |
| **Interceptors** | Modify requests/responses                 |
| **Filters**      | Handle exceptions                         |
| **Modules**      | Group and organize application components |

#### Minimum Requirements for a NestJS Application

Every NestJS application requires at least:

- One **Module**
- One **Controller**

#### Creating the Main File

Create `src/main.ts`:

```typescript
import { Controller, Module, Get } from "@nestjs/common";

@Controller()
class AppController {
  @Get()
  getRootRoute() {
    return "Hi there!";
  }
}
```

#### Key Concepts

**Decorator**: A special syntax (using `@` symbol) that tells NestJS about the purpose of a class or method. The `@Controller()` decorator marks a class as a controller that handles and routes incoming requests.

**Route Handler**: A method inside a controller that handles a specific type of incoming request. The `@Get()` decorator creates a route handler that responds to HTTP GET requests.

#### Why This Matters

Controllers are the entry point for all incoming HTTP requests. Understanding how decorators work is essential because NestJS uses them extensively to define application structure and behavior.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=600&lines=🎬+Lecture+2.4+–+Starting+Up+a+Nest+App" alt="Lecture 2.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to create a NestJS module, wire it to a controller, and bootstrap the application to start listening for incoming traffic.

#### Creating a Module

Add the module to `src/main.ts`:

```typescript
import { Controller, Module, Get } from "@nestjs/common";
import { NestFactory } from "@nestjs/core";

@Controller()
class AppController {
  @Get()
  getRootRoute() {
    return "Hi there!";
  }
}

@Module({
  controllers: [AppController],
})
class AppModule {}

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}

bootstrap();
```

#### Key Concepts

**Module**: A class decorated with `@Module()` that wraps up controllers and other providers. The `controllers` property lists all controllers that belong to this module.

**NestFactory**: A class from `@nestjs/core` that creates an instance of a NestJS application.

**Bootstrap Function**: The entry point function that creates the application instance and starts listening for traffic on a specified port.

#### Import Sources

| Import                        | Source           | Usage Frequency     |
| ----------------------------- | ---------------- | ------------------- |
| `Controller`, `Module`, `Get` | `@nestjs/common` | ~95% of imports     |
| `NestFactory`                 | `@nestjs/core`   | Mainly in `main.ts` |

#### How NestJS Starts Up

1. `bootstrap()` function is called
2. `NestFactory.create()` receives the `AppModule`
3. NestJS looks at the module's `controllers` array
4. NestJS creates instances of all listed controllers
5. NestJS examines decorators to set up route handlers
6. Application starts listening on the specified port

#### Running the Application

```bash
npx ts-node-dev src/main.ts
```

#### Testing the Application

Navigate to `http://localhost:3000` in a browser to see "Hi there!" displayed.

#### Why This Matters

Understanding the bootstrap process and how modules connect to controllers is fundamental to building any NestJS application. The module system is how NestJS organizes and structures applications.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=600&lines=🎬+Lecture+2.5+–+File+Naming+Conventions" alt="Lecture 2.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains the file naming conventions used in NestJS projects and demonstrates how to properly organize code by extracting classes into separate files.

#### NestJS File Naming Convention

The naming pattern follows: `<name>.<type>.ts`

| Class Name      | File Name           |
| --------------- | ------------------- |
| `AppController` | `app.controller.ts` |
| `AppModule`     | `app.module.ts`     |
| `UsersService`  | `users.service.ts`  |
| `AuthGuard`     | `auth.guard.ts`     |

#### Why This Convention Matters

- Immediately understand a file's purpose by its name
- Quickly identify the type of class contained in a file
- Maintain consistency across the entire codebase
- One class per file is the standard practice

#### Extracting the Controller

Create `src/app.controller.ts`:

```typescript
import { Controller, Get } from "@nestjs/common";

@Controller()
export class AppController {
  @Get()
  getRootRoute() {
    return "Hi there!";
  }
}
```

#### Extracting the Module

Create `src/app.module.ts`:

```typescript
import { Module } from "@nestjs/common";
import { AppController } from "./app.controller";

@Module({
  controllers: [AppController],
})
export class AppModule {}
```

#### Updating the Main File

Update `src/main.ts`:

```typescript
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}

bootstrap();
```

#### Important Reminders

- Always use the `export` keyword when defining classes that need to be imported elsewhere
- Import classes from their respective files using relative paths

#### Why This Matters

Proper file organization is essential for maintainable and scalable NestJS applications. Following conventions makes it easier for teams to collaborate and for new developers to understand the codebase.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=DC3545&center=true&vCenter=true&width=600&lines=🎬+Lecture+2.6+–+Routing+Decorators" alt="Lecture 2.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to use the `@Controller()` and `@Get()` decorators to define routing rules and create multiple route handlers.

#### Route Configuration with Decorators

Both `@Controller()` and `@Get()` decorators accept optional string arguments to define routes.

#### Controller-Level Routing

The route passed to `@Controller()` applies to all route handlers within that controller:

```typescript
@Controller("/app")
export class AppController {
  // All routes in this controller start with /app
}
```

#### Method-Level Routing

The route passed to `@Get()` defines the specific path for that route handler:

```typescript
@Controller("/app")
export class AppController {
  @Get("/hello")
  getHello() {
    return "Hello!";
  }

  @Get("/bye")
  getBye() {
    return "Bye there!";
  }
}
```

#### Route Resolution

Routes are combined from controller and method decorators:

| Controller Route | Method Route | Full Path    |
| ---------------- | ------------ | ------------ |
| `/app`           | `/hello`     | `/app/hello` |
| `/app`           | `/bye`       | `/app/bye`   |
| (empty)          | (empty)      | `/` (root)   |

#### Example: Multiple Route Handlers

```typescript
import { Controller, Get } from "@nestjs/common";

@Controller("/app")
export class AppController {
  @Get("/asdf")
  getRootRoute() {
    return "Hi there!";
  }

  @Get("/bye")
  getByeThere() {
    return "Bye there!";
  }
}
```

#### Testing Routes

- `GET /app/asdf` → Returns "Hi there!"
- `GET /app/bye` → Returns "Bye there!"
- `GET /` → Returns 404 Not Found (no handler defined)

#### Why This Matters

Understanding routing is fundamental to building REST APIs with NestJS. The decorator-based routing system provides a clean and declarative way to define API endpoints, making the code self-documenting and easy to maintain.

<br>

---

## Section 3: Generating Projects with the Nest CLI

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=500&lines=🎬+Lecture+3.1+–+App+Setup" alt="Lecture 3.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture transitions from the manual project setup to using the Nest CLI for project generation. It introduces the Messages application that will be built throughout this section.

#### Why Start with a Manual Project First?

When using the CLI to generate a project, it creates many files and folders automatically which can be confusing. Starting with a simple manual project helps understand how little code it takes to get Nest up and running.

#### Installing the Nest CLI

```bash
npm install -g @nestjs/cli
```

> **Note:** If you get a permission error, try prepending `sudo` on Mac/Linux or run as Administrator on Windows.

#### Generating a New Project

```bash
nest new messages
```

When prompted, select your preferred package manager (npm is recommended for this course).

#### The Messages Application

The goal is to build a simple application that stores and retrieves messages from a plain JSON file.

#### Application Routes

| Method | Route           | Description                 |
| ------ | --------------- | --------------------------- |
| GET    | `/messages`     | List all messages           |
| GET    | `/messages/:id` | Retrieve a specific message |
| POST   | `/messages`     | Create a new message        |

#### Planning the Architecture

For each route, we need to think about what classes to create:

**GET /messages (List all messages)**

- ❌ Pipe - No incoming data to validate
- ❌ Guard - No authentication required
- ✅ Controller - Route the request
- ✅ Service - Business logic to get messages
- ✅ Repository - Access the JSON file

**POST /messages (Create a message)**

- ✅ Pipe - Validate the incoming body (content property)
- ❌ Guard - No authentication required
- ✅ Controller - Route the request
- ✅ Service - Business logic to create message
- ✅ Repository - Store in the JSON file

**GET /messages/:id (Get specific message)**

- ❌ Pipe - ID comes from URL, minimal validation
- ❌ Guard - No authentication required
- ✅ Controller - Route the request
- ✅ Service - Business logic to find message
- ✅ Repository - Read from the JSON file

#### Important Clarification

We're only creating **one** controller, **one** service, and **one** repository to handle all three requests - not separate ones for each route.

#### Why This Matters

Planning the architecture before writing code helps understand what components are needed and how they interact. This planning process should be done for any NestJS application.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=650&lines=🎬+Lecture+3.2+–+Using+the+Nest+CLI+to+Generate+Files" alt="Lecture 3.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explores the generated project structure, how to start the development server, and how to use the CLI to generate modules.

#### Project Structure Overview

When you generate a project with Nest CLI, you get many more files and folders compared to a manual setup:

```
messages/
├── src/
│   ├── app.controller.ts
│   ├── app.controller.spec.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── main.ts
├── test/
├── node_modules/
├── package.json
├── tsconfig.json
├── eslint.config.mjs
└── ...
```

#### Important Scripts in package.json

| Script        | Command                      | Purpose                                     |
| ------------- | ---------------------------- | ------------------------------------------- |
| `start:dev`   | `nest start --watch`         | Start in development mode with auto-restart |
| `start`       | `nest start`                 | Start in production mode                    |
| `start:debug` | `nest start --debug --watch` | Start with debugging enabled                |
| `build`       | `nest build`                 | Compile TypeScript to JavaScript            |

#### Starting the Development Server

```bash
pnpm run start:dev
```

This starts the server with hot-reload - any code changes will automatically restart the server.

#### Disabling ESLint (Optional)

The instructor prefers to disable ESLint since TypeScript already catches many errors. To disable:

1. Open `eslint.config.mjs`
2. Comment out the entire contents of the configuration object

```javascript
// Comment out all contents if you want to disable ESLint
```

> **Note:** This is a personal preference. You can keep ESLint enabled if you prefer.

#### Cleaning Up Default Files

For this project, we'll create our own module and controller from scratch. Delete these default files:

- `app.controller.ts`
- `app.controller.spec.ts`
- `app.module.ts`
- `app.service.ts`

#### Generating a Module with CLI

```bash
nest generate module messages
```

This creates:

- A `messages` directory
- A `messages.module.ts` file inside it

#### Generated Module Code

```typescript
import { Module } from "@nestjs/common";

@Module({})
export class MessagesModule {}
```

> **Important:** Don't include the word "module" in the name when running the command. The CLI automatically appends it.

#### Updating main.ts

After generating the module, update `main.ts` to use the new module:

```typescript
import { NestFactory } from "@nestjs/core";
import { MessagesModule } from "./messages/messages.module";

async function bootstrap() {
  const app = await NestFactory.create(MessagesModule);
  await app.listen(3000);
}
bootstrap();
```

#### Why This Matters

The Nest CLI significantly speeds up development by generating boilerplate code and maintaining consistent file structure. Understanding how to use it effectively is essential for productive NestJS development.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+3.3+–+More+on+Generating+Files" alt="Lecture 3.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to generate a controller using the Nest CLI and explains the command options in detail.

#### Generating a Controller

```bash
nest generate controller messages/messages --flat
```

#### Understanding the Command

| Part                       | Purpose                                                   |
| -------------------------- | --------------------------------------------------------- |
| `nest generate controller` | Tell CLI to generate a controller                         |
| `messages/messages`        | First `messages` = folder, Second `messages` = class name |
| `--flat`                   | Don't create an additional `controllers` subfolder        |

#### What Gets Created

The command creates two files:

- `messages.controller.ts` - The controller class
- `messages.controller.spec.ts` - Test file for the controller

#### Auto-Wiring to Module

The CLI automatically updates `messages.module.ts`:

```typescript
import { Module } from "@nestjs/common";
import { MessagesController } from "./messages.controller";

@Module({
  controllers: [MessagesController],
})
export class MessagesModule {}
```

> **Key Benefit:** The CLI not only creates files but also wires them together automatically!

#### Generated Controller Code

```typescript
import { Controller } from "@nestjs/common";

@Controller("messages")
export class MessagesController {}
```

Notice that the route `'messages'` is automatically added to the `@Controller()` decorator.

#### The --flat Option Explained

**Without `--flat`:**

```
messages/
├── controllers/
│   ├── messages.controller.ts
│   └── messages.controller.spec.ts
└── messages.module.ts
```

**With `--flat`:**

```
messages/
├── messages.controller.ts
├── messages.controller.spec.ts
└── messages.module.ts
```

Use `--flat` when you don't want additional subdirectory organization. For smaller projects, `--flat` keeps things simpler.

#### Naming Convention Reminder

If you run:

```bash
nest generate controller messages/messages-controller  # Wrong!
```

You'll end up with `MessagesControllerController` - the CLI already appends "Controller" to the class name.

#### Why This Matters

Using the CLI's generate commands saves significant time and ensures consistent structure. The automatic wiring of generated classes to modules reduces boilerplate and potential errors.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=600&lines=🎬+Lecture+3.4+–+Adding+Routing+Logic" alt="Lecture 3.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to set up route handlers inside a controller using decorators, and the two different approaches for organizing routes.

#### Route Decorators

NestJS provides decorators for each HTTP method:

| Decorator   | HTTP Method |
| ----------- | ----------- |
| `@Get()`    | GET         |
| `@Post()`   | POST        |
| `@Put()`    | PUT         |
| `@Delete()` | DELETE      |
| `@Patch()`  | PATCH       |

#### Two Options for Route Configuration

**Option 1: Full paths in method decorators**

```typescript
@Controller()
export class MessagesController {
  @Get("/messages")
  listMessages() {}

  @Post("/messages")
  createMessage() {}

  @Get("/messages/:id")
  getMessage() {}
}
```

**Option 2: Extract common prefix to controller (Recommended)**

```typescript
@Controller("messages")
export class MessagesController {
  @Get()
  listMessages() {}

  @Post()
  createMessage() {}

  @Get("/:id")
  getMessage() {}
}
```

#### Route Resolution

Routes are constructed by combining the controller prefix with the method route:

| Controller | Method  | Final Route     |
| ---------- | ------- | --------------- |
| `messages` | (empty) | `/messages`     |
| `messages` | (empty) | `/messages`     |
| `messages` | `/:id`  | `/messages/:id` |

#### Implementing the Messages Controller

```typescript
import { Controller, Get, Post } from "@nestjs/common";

@Controller("messages")
export class MessagesController {
  @Get()
  listMessages() {}

  @Post()
  createMessage() {}

  @Get("/:id")
  getMessage() {}
}
```

#### Route Parameters

The `:id` syntax in `@Get('/:id')` creates a route parameter. When a request comes to `/messages/123`, the `123` becomes available as the `id` parameter.

#### Why This Matters

Extracting common route prefixes to the controller level:

- Reduces code duplication
- Makes routes easier to read and maintain
- Follows DRY (Don't Repeat Yourself) principle

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=600&lines=🎬+Lecture+3.5+–+[Optional]+Postman+Setup" alt="Lecture 3.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to set up Postman as an API client for testing NestJS applications.

#### Why Use an API Client?

- GET requests can be tested in a browser
- POST, PUT, DELETE requests require writing JavaScript in browser console
- API clients provide a better interface for testing all HTTP methods

#### Installing Postman

1. Navigate to [postman.com](https://postman.com)
2. Create an account (required)
3. Download the desktop application
4. Install and launch

> **Note:** You can skip login in the desktop app by clicking "I will sign in later" at the bottom left.

#### Making a GET Request

1. Click the `+` button to create a new request
2. Select `GET` from the dropdown
3. Enter the URL: `http://localhost:3000/messages`
4. Click `Send`
5. View the response at the bottom (Status: 200 OK)

#### Making a POST Request

1. Change method to `POST`
2. Go to the `Body` tab
3. Select `raw`
4. Change dropdown to `JSON`
5. Enter the JSON body:

```json
{
  "content": "Hi there"
}
```

6. Click `Send`

#### Important Notes for POST Requests

- The body must be valid JSON (not JavaScript)
- Use double quotes for both keys and values
- The `Content-Type` header is automatically set to `application/json`

#### Why This Matters

Having a proper API client is essential for testing REST APIs during development. Postman provides features like:

- Request history
- Collections for organizing requests
- Environment variables
- Automated testing

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=DC3545&center=true&vCenter=true&width=700&lines=🎬+Lecture+3.6+–+[Optional]+VS+Code+REST+Client+Extension" alt="Lecture 3.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces the VS Code REST Client extension as an alternative to Postman for testing APIs directly within VS Code.

#### Why Use REST Client?

- Requests are stored as files in your project
- Can be version controlled with your code
- Acts as documentation for your API
- No need to leave your code editor

#### Installing REST Client

1. Open VS Code
2. Go to View → Extensions (or `Ctrl+Shift+X`)
3. Search for "REST Client"
4. Install the extension by Huachao Mao

#### Creating a Request File

Create a file named `requests.http` in your project root:

```http
### List all messages
GET http://localhost:3000/messages

### Create a new message
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": "Hi there"
}

### Get a particular message
GET http://localhost:3000/messages/123
```

#### Request File Syntax

| Element       | Purpose                                    |
| ------------- | ------------------------------------------ |
| `###`         | Comment/separator between requests         |
| `GET`, `POST` | HTTP method                                |
| URL           | Full URL for the request                   |
| Headers       | Listed on lines immediately after the URL  |
| Empty line    | Separates headers from body                |
| Body          | JSON or other content after the empty line |

#### Making Requests

- A "Send Request" link appears above each request
- Click it to execute the request
- Response appears in a new panel on the right

#### Important Formatting Rules

For POST requests with a body:

1. Headers go directly after the URL (no empty line)
2. **One empty line** must separate headers from body
3. Body content follows the empty line

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": "Hi there"
}
```

#### Benefits Over Postman

| Feature               | REST Client           | Postman            |
| --------------------- | --------------------- | ------------------ |
| Version Control       | ✅ Built into project | ❌ Separate system |
| IDE Integration       | ✅ In VS Code         | ❌ Separate app    |
| Documentation         | ✅ Self-documenting   | ⚠️ Requires export |
| Account Required      | ❌ No                 | ✅ Yes             |
| Works without VS Code | ❌ No                 | ✅ Yes             |

#### Why This Matters

The REST Client extension provides a lightweight, integrated way to test APIs that becomes part of your project's documentation. The request file can be shared with the team and kept in version control.

<br>

---

## Section 3 Summary

This section covered:

1. **Nest CLI Installation** - Installing and using `@nestjs/cli` globally
2. **Project Generation** - Using `nest new` to scaffold projects
3. **Module Generation** - Using `nest generate module` to create modules
4. **Controller Generation** - Using `nest generate controller` with options
5. **Route Configuration** - Setting up routes with `@Get()`, `@Post()` decorators
6. **API Testing Tools** - Setting up Postman or VS Code REST Client

#### Key CLI Commands Learned

| Command                                         | Purpose                   |
| ----------------------------------------------- | ------------------------- |
| `npm install -g @nestjs/cli`                    | Install Nest CLI globally |
| `nest new <project-name>`                       | Create a new project      |
| `nest generate module <name>`                   | Generate a module         |
| `nest generate controller <path>/<name> --flat` | Generate a controller     |

These tools and techniques form the foundation for efficient NestJS development workflows.
<br>

---

## Section 4: Validating Request Data with Pipes

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=700&lines=🎬+Lecture+4.1+–+Accessing+Request+Data+with+Decorators" alt="Lecture 4.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to extract information from incoming HTTP requests using parameter decorators in NestJS.

#### HTTP Request Structure

An HTTP request consists of several parts:

```
GET /messages/5?validate=true HTTP/1.1     ← Start Line (method, route, protocol)
Host: localhost:3000                        ← Headers
Content-Type: application/json              ← Headers

{ "content": "Hello" }                      ← Body (for POST/PUT/PATCH)
```

#### Request Data Extraction Decorators

NestJS provides decorators to extract different parts of a request:

| Decorator    | Purpose                            | Example Usage        |
| ------------ | ---------------------------------- | -------------------- |
| `@Param()`   | Extract URL parameters (wildcards) | `/messages/:id` → id |
| `@Query()`   | Extract query string parameters    | `?validate=true`     |
| `@Body()`    | Extract request body               | JSON payload         |
| `@Headers()` | Extract request headers            | `Content-Type`, etc. |

#### Types of Decorators

| Decorator Type     | Applied To      | Example               |
| ------------------ | --------------- | --------------------- |
| Class Decorator    | Entire class    | `@Controller()`       |
| Method Decorator   | Method          | `@Get()`, `@Post()`   |
| Argument Decorator | Method argument | `@Body()`, `@Param()` |

#### Using @Body() Decorator

Extract the body from a POST request:

```typescript
import { Controller, Post, Body } from "@nestjs/common";

@Controller("messages")
export class MessagesController {
  @Post()
  createMessage(@Body() body: any) {
    console.log(body);
  }
}
```

#### Using @Param() Decorator

Extract URL parameters:

```typescript
import { Controller, Get, Param } from "@nestjs/common";

@Controller("messages")
export class MessagesController {
  @Get("/:id")
  getMessage(@Param("id") id: string) {
    console.log(id);
  }
}
```

> **Note:** The string passed to `@Param('id')` must match the route parameter name (`:id`).

#### Complete Controller Example

```typescript
import { Controller, Get, Post, Body, Param } from "@nestjs/common";

@Controller("messages")
export class MessagesController {
  @Get()
  listMessages() {}

  @Post()
  createMessage(@Body() body: any) {
    console.log(body);
  }

  @Get("/:id")
  getMessage(@Param("id") id: string) {
    console.log(id);
  }
}
```

#### Testing the Decorators

**POST Request Test:**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": "Hi there"
}
```

Console output: `{ content: 'Hi there' }`

**GET Request with Parameter:**

```http
GET http://localhost:3000/messages/anything
```

Console output: `anything`

#### Why This Matters

Parameter decorators are fundamental to working with HTTP requests in NestJS. They provide a clean, declarative way to access request data without manually parsing the request object.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=600&lines=🎬+Lecture+4.3+–+Using+Pipes+for+Validation" alt="Lecture 4.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces the ValidationPipe for automatic request validation in NestJS applications.

#### Why Use Pipes for Validation?

For a POST request handler that expects:

```json
{
  "content": "some string"
}
```

We need to validate:

- The `content` property exists
- The `content` value is a string (not a number, null, etc.)

If validation fails, the request should be rejected **before** reaching the route handler.

#### The ValidationPipe

NestJS provides a built-in `ValidationPipe` that handles validation automatically:

- Built into NestJS
- Used on almost every project
- Validates incoming request data
- Returns detailed error messages

#### Setting Up Global Validation

Update `main.ts` to use the ValidationPipe globally:

```typescript
import { NestFactory } from "@nestjs/core";
import { ValidationPipe } from "@nestjs/common";
import { MessagesModule } from "./messages/messages.module";

async function bootstrap() {
  const app = await NestFactory.create(MessagesModule);
  app.useGlobalPipes(new ValidationPipe());
  await app.listen(3000);
}
bootstrap();
```

#### What useGlobalPipes() Does

| Aspect      | Description                                         |
| ----------- | --------------------------------------------------- |
| Scope       | Applies to **all** incoming requests                |
| Opt-in      | Only validates routes with validation rules defined |
| Intelligent | Skips routes without validation rules               |

#### Key Points

- `useGlobalPipes()` applies the pipe to every route
- The ValidationPipe only runs validation when rules are defined
- Routes without validation rules are not affected

#### Why This Matters

Setting up global validation once means you don't have to wire up validation for each individual route. The ValidationPipe intelligently determines which routes need validation based on the presence of DTOs and validation decorators.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+4.4+–+Adding+Validation+Rules" alt="Lecture 4.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains the complete process of setting up validation rules using DTOs (Data Transfer Objects) and the class-validator library.

#### Validation Setup Steps

| Step | Action                                        | Frequency    |
| ---- | --------------------------------------------- | ------------ |
| 1    | Set up global ValidationPipe in `main.ts`     | Once per app |
| 2    | Create a DTO class describing expected data   | Per route    |
| 3    | Add validation decorators to DTO properties   | Per route    |
| 4    | Apply DTO as type annotation in route handler | Per route    |

#### What is a DTO?

**DTO** = **D**ata **T**ransfer **O**bject

A class that describes all the properties expected in an incoming request. DTOs:

- Define the shape of request data
- Hold validation rules via decorators
- Are used as type annotations in route handlers

#### Step 2: Create the DTO Class

Create the directory and file structure:

```
messages/
├── dtos/
│   └── create-message.dto.ts
├── messages.controller.ts
└── messages.module.ts
```

Create `create-message.dto.ts`:

```typescript
export class CreateMessageDto {
  content: string;
}
```

#### Step 3: Install and Apply Validation Decorators

Install required packages:

```bash
npm install class-validator class-transformer
```

| Package             | Purpose                                     |
| ------------------- | ------------------------------------------- |
| `class-validator`   | Provides validation decorators              |
| `class-transformer` | Transforms plain objects to class instances |

Add validation decorators to the DTO:

```typescript
import { IsString } from "class-validator";

export class CreateMessageDto {
  @IsString()
  content: string;
}
```

#### Common Validation Decorators

| Decorator       | Validates                 |
| --------------- | ------------------------- |
| `@IsString()`   | Value is a string         |
| `@IsNumber()`   | Value is a number         |
| `@IsEmail()`    | Value is a valid email    |
| `@IsNotEmpty()` | Value is not empty        |
| `@MinLength(n)` | String has minimum length |
| `@MaxLength(n)` | String has maximum length |
| `@IsOptional()` | Property is optional      |

#### Step 4: Apply DTO to Route Handler

Update the controller to use the DTO:

```typescript
import { Controller, Post, Body } from "@nestjs/common";
import { CreateMessageDto } from "./dtos/create-message.dto";

@Controller("messages")
export class MessagesController {
  @Post()
  createMessage(@Body() body: CreateMessageDto) {
    console.log(body);
  }
}
```

> **Important:** The DTO is applied as a **type annotation**. This might seem strange since TypeScript types are usually removed at runtime, but NestJS handles this specially.

#### Testing Validation

**Valid Request:**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": "Hi there"
}
```

Result: ✅ Status 200/201

**Invalid Request (number instead of string):**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": 123
}
```

Result: ❌ Error: "content must be a string"

**Invalid Request (missing property):**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{}
```

Result: ❌ Error: "content must be a string"

**Invalid Request (misspelled property):**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "contnet": "Hi there"
}
```

Result: ❌ Error: "content must be a string"

#### Why This Matters

Automatic validation ensures that route handlers only receive properly formatted data. This:

- Reduces defensive coding in handlers
- Provides consistent error messages
- Catches errors early in the request lifecycle

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=650&lines=🎬+Lecture+4.6+–+How+Type+Info+is+Preserved" alt="Lecture 4.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This optional lecture explains how TypeScript type information is preserved at runtime, allowing the ValidationPipe to work.

#### The TypeScript Paradox

When learning TypeScript, you're told:

> "All type information is stripped out when TypeScript compiles to JavaScript"

So how does NestJS know about our DTO type annotation at runtime?

#### The Answer: emitDecoratorMetadata

In `tsconfig.json`:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

The `emitDecoratorMetadata` option allows a **small amount** of type information to persist into JavaScript.

#### How It Works

When TypeScript compiles:

```typescript
@Post()
createMessage(@Body() body: CreateMessageDto) {
  // ...
}
```

It generates JavaScript with metadata:

```javascript
__decorate(
  [
    common_1.Post(),
    __param(0, common_1.Body()),
    __metadata("design:paramtypes", [create_message_dto_1.CreateMessageDto]),
  ],
  MessagesController.prototype,
  "createMessage",
  null
);
```

#### The Key Line

```javascript
__metadata("design:paramtypes", [CreateMessageDto]);
```

This metadata tells the ValidationPipe:

- The `createMessage` method expects one parameter
- That parameter should be of type `CreateMessageDto`

#### Viewing Compiled Code

You can see the compiled JavaScript in the `dist/` folder:

```
dist/
├── messages/
│   ├── messages.controller.js    ← Compiled JavaScript
│   └── dtos/
│       └── create-message.dto.js
└── main.js
```

> **Warning:** Don't save any changes to files in `dist/` - they are auto-generated!

#### The Validation Flow

1. Request arrives at POST `/messages`
2. ValidationPipe intercepts the request
3. Pipe reads `design:paramtypes` metadata
4. Discovers parameter type is `CreateMessageDto`
5. Finds the DTO class and its validation decorators
6. Validates incoming body against the rules
7. Passes validated data to handler (or returns error)

#### Why This Matters

Understanding this mechanism explains:

- Why `emitDecoratorMetadata` must be `true`
- Why DTOs must be classes (not interfaces)
- Why validation "magically" works with just a type annotation
- This pattern is used throughout NestJS (not just validation)

<br>

---

## Section 4 Summary

This section covered:

1. **Request Data Extraction** - Using `@Body()`, `@Param()`, `@Query()`, `@Headers()` decorators
2. **Decorator Types** - Class, method, and argument decorators
3. **ValidationPipe Setup** - Global validation configuration
4. **DTOs** - Data Transfer Objects for describing request structure
5. **class-validator** - Adding validation rules with decorators
6. **Type Metadata** - How TypeScript type info persists to runtime

#### Complete Validation Setup Checklist

```typescript
// 1. main.ts - Global pipe setup
import { ValidationPipe } from '@nestjs/common';
app.useGlobalPipes(new ValidationPipe());

// 2. create-message.dto.ts - DTO with validation
import { IsString } from 'class-validator';
export class CreateMessageDto {
  @IsString()
  content: string;
}

// 3. controller - Apply DTO as type
createMessage(@Body() body: CreateMessageDto) { }
```

#### Required Packages

```bash
npm install class-validator class-transformer
```

---

---

## Section 5: Nest Architecture - Services and Repositories

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.1+–+Services+and+Repositories" alt="Lecture 5.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces the concepts of Services and Repositories, two critical architectural patterns in NestJS for organizing business logic and data access.

#### Understanding Services vs Repositories

Both are classes, but serve different purposes:

| Aspect         | Service                          | Repository                   |
| -------------- | -------------------------------- | ---------------------------- |
| Purpose        | Business logic & data management | Storage-related logic only   |
| Interaction    | Works with repositories          | Directly accesses storage    |
| Responsibility | Orchestration                    | CRUD operations on storage   |
| Example        | Finding & filtering messages     | Reading/writing to JSON file |

#### When to Use Each

**Use a Service when you need to:**

- Execute business logic
- Fetch data from a repository
- Manipulate or transform data
- Coordinate multiple operations

**Use a Repository when you need to:**

- Directly interact with a database
- Write information to a file
- Manage file I/O operations
- Handle storage layer details

#### Common Methods Pattern

Services and repositories typically have similar method names:

```typescript
// Repository
class MessagesRepository {
  findOne(id: string) {} // Find by ID
  findAll() {} // Find all records
  create(content: string) {} // Add new record
}

// Service (calls repository methods)
class MessagesService {
  findOne(id: string) {} // Delegates to repo
  findAll() {} // Delegates to repo
  create(content: string) {} // Delegates to repo
}
```

#### Controller → Service → Repository Flow

```
Incoming Request
      ↓
   Controller
      ↓
   Service (business logic)
      ↓
   Repository (data access)
      ↓
   Storage (file, database, etc.)
```

#### Why This Architecture?

1. **Separation of Concerns** - Each layer has one responsibility
2. **Testability** - Easy to mock repositories for testing services
3. **Reusability** - Services can use multiple repositories
4. **Maintainability** - Changes to storage don't affect business logic

#### Note on Repository Wrappers

In real applications, repositories usually wrap external storage libraries:

- **TypeORM** - Database ORM with built-in repositories
- **Mongoose** - MongoDB object modeling with schemas
- **Prisma** - Modern database client

For this course, we'll build a repository from scratch to understand the pattern.

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.2+–+Implementing+a+Repository" alt="Lecture 5.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### Creating Repository and Service Files

In this lecture, we build the repository and service from scratch without using NestJS CLI generators initially.

#### File Structure Setup

```bash
messages/
  src/
    messages.repository.ts    # New: Handles file I/O
    messages.service.ts       # New: Business logic layer
    messages.controller.ts
    app.module.ts
```

#### MessagesRepository Class Structure

The repository will have three core methods:

```typescript
export class MessagesRepository {
  async findOne(id: string) {}
  async findAll() {}
  async create(content: string) {}
}
```

#### Understanding Each Method

| Method  | Purpose                            | Returns              |
| ------- | ---------------------------------- | -------------------- |
| findOne | Find message by ID from storage    | Message or undefined |
| findAll | Retrieve all messages from storage | All messages object  |
| create  | Add new message to storage         | void/confirmation    |

#### Required Dependencies

```bash
npm install class-validator class-transformer
```

These packages handle data validation and transformation for DTOs.

#### Key Implementation Details

1. **Messages Repository** - Manages file I/O operations
   - Reads/writes to `messages.json` file
   - Uses Node.js `fs/promises` module
   - Parses and stringifies JSON data

2. **Messages Service** - Business logic layer
   - Receives repository instance
   - Delegates to repository methods
   - Handles business logic (filtering, validation, etc.)

3. **Storage Format** - JSON file structure

```json
{
  "1": { "id": "1", "content": "Hello" },
  "2": { "id": "2", "content": "World" }
}
```

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.3+–+Reading+and+Writing+to+a+Storage+File" alt="Lecture 5.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### Implementing File I/O Operations

This lecture covers the actual implementation of reading and writing messages to a JSON file.

#### MessagesRepository Implementation

```typescript
import { readFile, writeFile } from "fs/promises";

export class MessagesRepository {
  async findOne(id: string) {
    const contents = await readFile("messages.json", "utf8");
    const messages = JSON.parse(contents);
    return messages[id];
  }

  async findAll() {
    const contents = await readFile("messages.json", "utf8");
    const messages = JSON.parse(contents);
    return messages;
  }

  async create(content: string) {
    const contents = await readFile("messages.json", "utf8");
    const messages = JSON.parse(contents);

    // Generate random ID
    const id = Math.floor(Math.random() * 999);

    // Add new message
    messages[id] = { id, content };

    // Write back to file
    await writeFile("messages.json", JSON.stringify(messages));
  }
}
```

#### File Operations Breakdown

| Operation | Method                                                 | Purpose                  |
| --------- | ------------------------------------------------------ | ------------------------ |
| Read      | `readFile('messages.json', 'utf8')`                    | Load file contents       |
| Parse     | `JSON.parse(contents)`                                 | Convert string to object |
| Modify    | `messages[id] = { id, content }`                       | Update object            |
| Write     | `writeFile('messages.json', JSON.stringify(messages))` | Save to file             |

#### Initial messages.json Setup

```json
{}
```

Start with an empty object to avoid parsing errors on application startup.

#### Important Notes

- File must exist beforehand (we don't auto-generate it)
- All operations are asynchronous
- IDs are randomly generated integers
- Each message stores both `id` and `content`

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.4+–+Implementing+a+Service" alt="Lecture 5.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### Creating the MessagesService

The service acts as an intermediary between the controller and repository, providing business logic capabilities.

#### MessagesService Implementation

```typescript
import { MessagesRepository } from "./messages.repository";

export class MessagesService {
  messagesRepo = new MessagesRepository(); // Temporary: Will use DI later

  findOne(id: string) {
    return this.messagesRepo.findOne(id);
  }

  findAll() {
    return this.messagesRepo.findAll();
  }

  create(content: string) {
    return this.messagesRepo.create(content);
  }
}
```

#### Why Service Seems Redundant

At this stage, the service appears to simply delegate to the repository:

- **Service method**: `findOne(id)` → **Repository method**: `findOne(id)`
- **Service method**: `findAll()` → **Repository method**: `findAll()`
- **Service method**: `create(content)` → **Repository method**: `create(content)`

**This pattern becomes clear when you add business logic later:**

```typescript
export class MessagesService {
  // Future: Add filtering, validation, caching, etc.
  findAll() {
    const messages = this.messagesRepo.findAll();
    // Filter active messages
    // Add timestamps
    // Cache results
    return processedMessages;
  }
}
```

#### Service vs Repository Distinction

| Aspect       | Service                | Repository            |
| ------------ | ---------------------- | --------------------- |
| Focus        | Business logic         | Data access           |
| Dependencies | Uses repositories      | No dependencies       |
| Reusability  | Can use multiple repos | Single responsibility |
| Testing      | Easy to mock           | Tests file I/O        |

#### Note on Dependency Management

```typescript
// ⚠️ NOT RECOMMENDED - Service creates its own dependency
messagesRepo = new MessagesRepository();

// We'll fix this with Dependency Injection in later lectures
```

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.5+–+Manual+Testing+of+the+Controller" alt="Lecture 5.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### Connecting Service to Controller

Now we wire up the service to the controller and test all three endpoints.

#### MessagesController with Service

```typescript
import { Controller, Get, Post, Body, Param } from "@nestjs/common";
import { MessagesService } from "./messages.service";
import { CreateMessageDto } from "./dto/create-message.dto";

@Controller("messages")
export class MessagesController {
  messagesService = new MessagesService(); // Temporary: Will use DI

  @Get()
  listMessages() {
    return this.messagesService.findAll();
  }

  @Post()
  createMessage(@Body() body: CreateMessageDto) {
    return this.messagesService.create(body.content);
  }

  @Get(":id")
  getMessage(@Param("id") id: string) {
    return this.messagesService.findOne(id);
  }
}
```

#### Testing with Postman/REST Client

**1. Get All Messages**

```http
GET http://localhost:3000/messages
```

Expected Response (empty start):

```json
{}
```

**2. Create a Message**

```http
POST http://localhost:3000/messages
Content-Type: application/json

{
  "content": "Hello NestJS!"
}
```

Expected Response:

```json
{
  "123": {
    "id": 123,
    "content": "Hello NestJS!"
  }
}
```

**3. Get Specific Message**

```http
GET http://localhost:3000/messages/123
```

Expected Response:

```json
{
  "id": 123,
  "content": "Hello NestJS!"
}
```

#### Required Setup

Ensure `messages.json` exists in project root:

```json
{}
```

**If file doesn't exist:** You'll see a 500 error with "ENOENT: no such file or directory"

#### Application Flow

```
Client Request
     ↓
Controller (Route Handler)
     ↓
Service (Business Logic)
     ↓
Repository (File I/O)
     ↓
messages.json (Storage)
```

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.6+–+Reporting+Errors+with+Exceptions" alt="Lecture 5.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### Handling Errors with NestJS Exceptions

This lecture covers proper error handling using NestJS built-in HTTP exceptions.

#### The Problem: Invalid Message ID

Without error handling, requesting a non-existent message returns `200 OK` with `null`.

#### Solution: NotNotFoundException

```typescript
import { Controller, Get, Param, NotFoundException } from "@nestjs/common";
import { MessagesService } from "./messages.service";

@Controller("messages")
export class MessagesController {
  @Get(":id")
  async getMessage(@Param("id") id: string) {
    const message = await this.messagesService.findOne(id);

    if (!message) {
      throw new NotFoundException("Message not found");
    }

    return message;
  }
}
```

#### NestJS Built-in Exceptions

| Exception                    | Status Code | Use Case                   |
| ---------------------------- | ----------- | -------------------------- |
| NotFoundException            | 404         | Resource doesn't exist     |
| BadRequestException          | 400         | Invalid request parameters |
| UnauthorizedException        | 401         | Authentication failed      |
| ForbiddenException           | 403         | Access denied              |
| UnprocessableEntityException | 422         | Validation failed          |
| GatewayTimeoutException      | 504         | Request timeout            |

#### Automatic Error Handling

When you throw an exception, NestJS automatically:

1. **Catches** the exception
2. **Extracts** status code and message
3. **Returns** formatted JSON response
4. **Sets** appropriate HTTP status

#### Example Error Response

**Request:**

```http
GET http://localhost:3000/messages/999
```

**Response (404):**

```json
{
  "statusCode": 404,
  "message": "Message not found",
  "error": "Not Found"
}
```

#### Complete Controller with Error Handling

```typescript
@Controller("messages")
export class MessagesController {
  constructor(private messagesService: MessagesService) {}

  @Get()
  listMessages() {
    return this.messagesService.findAll();
  }

  @Post()
  createMessage(@Body() body: CreateMessageDto) {
    return this.messagesService.create(body.content);
  }

  @Get(":id")
  async getMessage(@Param("id") id: string) {
    const message = await this.messagesService.findOne(id);

    if (!message) {
      throw new NotFoundException("Message not found");
    }

    return message;
  }
}
```

#### Key Points

- Always validate data before returning
- Use appropriate HTTP status codes
- Provide clear error messages
- NestJS exceptions are self-documenting
- Exceptions follow HTTP standards

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.7+–+Understanding+Inversion+of+Control" alt="Lecture 5.7" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### The Inversion of Control Principle

This lecture introduces the foundational concept behind Dependency Injection.

#### The Problem: Classes Creating Their Own Dependencies

**Current (Bad) Approach:**

```typescript
export class MessagesService {
  // Service creates its own dependency ❌
  messagesRepo = new MessagesRepository();

  findOne(id: string) {
    return this.messagesRepo.findOne(id);
  }
}
```

**Issues:**

- Service is tightly coupled to MessagesRepository
- Hard to test (can't mock the repository)
- Can't reuse service with different repositories
- Not following the Inversion of Control principle

#### Solution: Constructor Injection

**Better Approach:**

```typescript
export class MessagesService {
  // Dependency is passed in ✅
  constructor(private messagesRepo: MessagesRepository) {}

  findOne(id: string) {
    return this.messagesRepo.findOne(id);
  }
}

// Usage:
const repo = new MessagesRepository();
const service = new MessagesService(repo);
```

**Benefits:**

- Service doesn't create dependencies
- Easy to test with mock repository
- More flexible and reusable
- Follows Inversion of Control

#### Best Approach: Interface-Based Injection

```typescript
// Define interface
interface IRepository {
  findOne(id: string): Promise<Message>;
  findAll(): Promise<Messages>;
  create(content: string): Promise<void>;
}

// Service depends on interface, not implementation
export class MessagesService {
  constructor(private repo: IRepository) {}
}

// Can use any implementation
const messagesRepo = new MessagesRepository();
const mockRepo = new MockRepository();
const service = new MessagesService(messagesRepo); // or mockRepo
```

#### Dependency Hierarchy

```
Controller
    ↓ depends on
  Service
    ↓ depends on
  Repository
    ↓ uses
  Storage
```

#### Three Levels of Code Quality

| Level  | Pattern                               | Testability    | Flexibility    |
| ------ | ------------------------------------- | -------------- | -------------- |
| Bad    | `new MessagesRepository()` in Service | ❌ Low         | ❌ Low         |
| Better | Constructor injection                 | ✅ Good        | ✅ Good        |
| Best   | Interface-based injection             | ✅✅ Excellent | ✅✅ Excellent |

#### Why This Matters

1. **Testability** - Mock dependencies easily
2. **Flexibility** - Swap implementations without changing code
3. **Maintainability** - Clear dependency relationships
4. **Reusability** - Use service with different repositories

#### The Downside: Boilerplate Code

Creating instances with constructor injection requires more setup:

```typescript
// Without IoC (simple but inflexible)
const service = new MessagesService();

// With IoC (flexible but verbose)
const repo = new MessagesRepository();
const service = new MessagesService(repo);
const controller = new MessagesController(service);

// In complex apps: Even more boilerplate!
```

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+5.8+–+Introduction+to+Dependency+Injection" alt="Lecture 5.8" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What is Dependency Injection?

Dependency Injection (DI) solves the boilerplate problem of Inversion of Control by using a **Container** to automatically manage dependencies.

#### The Boilerplate Problem

With manual constructor injection, creating instances becomes verbose:

```typescript
// For a simple 3-layer app
const repo = new MessagesRepository();
const service = new MessagesService(repo);
const controller = new MessagesController(service);

// For complex apps with many dependencies:
const repo1 = new Repository1();
const repo2 = new Repository2();
const service1 = new Service1(repo1, repo2);
const service2 = new Service2(repo1);
const controller = new Controller(service1, service2);
// ... and this grows exponentially!
```

#### The DI Container Solution

A **Container** (also called an **Injector**) automatically:

1. **Registers** all classes and their dependencies
2. **Resolves** dependency graphs
3. **Creates** instances when needed
4. **Injects** dependencies automatically

#### How NestJS Container Works

**Step 1: Registration**

```
Container scans application for decorated classes:
├── @Injectable() MessagesRepository
├── @Injectable() MessagesService (depends on MessagesRepository)
└── @Controller() MessagesController (depends on MessagesService)

Container builds dependency map:
- MessagesRepository → no dependencies
- MessagesService → needs MessagesRepository
- MessagesController → needs MessagesService
```

**Step 2: Instantiation**

```
When controller is requested:
1. Container sees it needs MessagesService
2. Container sees service needs MessagesRepository
3. Container creates MessagesRepository first
4. Container creates MessagesService with repo
5. Container creates Controller with service
6. Returns fully constructed Controller
```

#### Benefits of Dependency Injection Container

| Problem          | Manual IoC | DI Container |
| ---------------- | ---------- | ------------ |
| Boilerplate Code | 🔴 Lots    | 🟢 None      |
| Testing          | 🟢 Easy    | 🟢 Easy      |
| Flexibility      | 🟢 High    | 🟢 High      |
| Scalability      | 🔴 Poor    | 🟢 Excellent |

#### NestJS Dependency Injection Implementation

Next lectures will cover:

1. **@Injectable()** decorator - Mark classes for injection
2. **@Inject()** decorator - Specify dependencies
3. **Module Configuration** - Register providers
4. **Testing** - Provide mock dependencies

#### Quick Preview

```typescript
import { Injectable } from "@nestjs/common";

@Injectable()
export class MessagesRepository {
  async findOne(id: string) {}
  async findAll() {}
  async create(content: string) {}
}

@Injectable()
export class MessagesService {
  // NestJS automatically injects MessagesRepository!
  constructor(private messagesRepo: MessagesRepository) {}

  findOne(id: string) {
    return this.messagesRepo.findOne(id);
  }
}

@Controller("messages")
export class MessagesController {
  // NestJS automatically injects MessagesService!
  constructor(private service: MessagesService) {}

  @Get(":id")
  getMessage(@Param("id") id: string) {
    return this.service.findOne(id);
  }
}
```

#### The DI Container Automatically Handles

✅ Creating instances in correct order  
✅ Resolving dependency chains  
✅ Singleton pattern (one instance per class)  
✅ Managing lifecycle  
✅ Injecting into constructors

#### Key Takeaway

**Dependency Injection is Inversion of Control without the boilerplate.**

The container handles all the manual wiring, letting you focus on business logic instead of plumbing code.

## <br>

## Section 6: Nest Architecture - Organizing Code with Modules

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.1+–+Project+Overview" alt="Lecture 6.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces a new project focused on understanding modules and dependency injection in NestJS through a practical computer simulation example.

#### The Computer Project

We're building a simplified computer model that demonstrates how different modules interact and share dependencies.

#### Project Architecture

The application will model a computer with these components:

| Component    | Purpose                                  | Dependencies |
| ------------ | ---------------------------------------- | ------------ |
| Power Supply | Supplies electricity to other components | None         |
| CPU          | Processes data                           | Power Supply |
| Disk         | Stores data                              | Power Supply |
| Computer     | Orchestrates CPU and Disk                | CPU, Disk    |

#### Module Hierarchy

```
Computer Module (top-level)
├── CPU Module
│   └── Power Module
└── Disk Module
    └── Power Module
```

#### Key Learning Objectives

1. Understand how modules work in NestJS
2. Learn how to share services between modules
3. Understand the relationship between modules and dependency injection
4. Master the scoping and accessibility of services

#### Why This Matters

This hierarchical structure demonstrates:

- **Encapsulation** - Each module manages its own concerns
- **Dependency injection** - Services are injected where needed
- **Code reusability** - Services can be shared across modules
- **Scalability** - Easy to add new modules and components

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.2+–+Generating+a+Few+Files" alt="Lecture 6.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to generate modules and services using the Nest CLI to create our project structure.

#### Project Setup

Generate a new NestJS project:

```bash
nest new di
cd di
npm start:dev
```

#### Cleaning Up Generated Files

Delete all default files except `main.ts`:

```bash
# Delete from src/:
- app.controller.ts
- app.controller.spec.ts
- app.module.ts
- app.service.ts

# Keep:
- main.ts
```

#### Generating Modules

Create all four required modules:

```bash
nest g module computer
nest g module cpu
nest g module disk
nest g module power
```

#### Generating Services

Create services for each module:

```bash
nest g service cpu
nest g service power
nest g service disk
```

#### Generating Controller

Create the controller for the computer module:

```bash
nest g controller computer
```

#### Updating Main.ts

Replace the AppModule import with ComputerModule:

```typescript
import { NestFactory } from "@nestjs/core";
import { ComputerModule } from "./computer/computer.module";

async function bootstrap() {
  const app = await NestFactory.create(ComputerModule);
  await app.listen(3000);
}
bootstrap();
```

#### File Structure After Generation

```
src/
├── computer/
│   ├── computer.controller.ts
│   └── computer.module.ts
├── cpu/
│   ├── cpu.service.ts
│   └── cpu.module.ts
├── disk/
│   ├── disk.service.ts
│   └── disk.module.ts
├── power/
│   ├── power.service.ts
│   └── power.module.ts
└── main.ts
```

#### Key Points

- Use CLI to generate consistent structure
- Bottom-up approach: start with foundational modules
- Keep one responsibility per module
- Use descriptive naming conventions

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.3+–+Implementing+Power+Service" alt="Lecture 6.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture focuses on implementing the base Power Service that other services will depend on.

#### Power Service Implementation

Create the power service that supplies power to other components:

```typescript
import { Injectable } from "@nestjs/common";

@Injectable()
export class PowerService {
  supplyPower(watts: number) {
    console.log(`Supplying ${watts} watts of power`);
  }
}
```

#### Power Service Purpose

| Aspect    | Description                  |
| --------- | ---------------------------- |
| Method    | `supplyPower(watts: number)` |
| Parameter | Number of watts to supply    |
| Returns   | void (logs supply action)    |
| Used By   | CPU Service, Disk Service    |

#### Power Module Setup

Update the power module to export the service:

```typescript
import { Module } from "@nestjs/common";
import { PowerService } from "./power.service";

@Module({
  providers: [PowerService],
  exports: [PowerService],
})
export class PowerModule {}
```

#### Why Exports Matter

| Without Exports              | With Exports                       |
| ---------------------------- | ---------------------------------- |
| Service is private to module | Service available to other modules |
| Can't be imported elsewhere  | Can be shared across the app       |
| Limited reusability          | Promotes code reuse                |

#### Key Concepts

- **Providers** - Classes that can be injected
- **Exports** - Services/classes available to other modules
- **Dependency** - When one service needs another

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.4+–+More+on+DI+Between+Modules" alt="Lecture 6.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to share services from one module to another using dependency injection.

#### Connecting CPU Service to Power Service

**Step 1: Ensure Power Service is Exported**

Power Module (already done):

```typescript
@Module({
  providers: [PowerService],
  exports: [PowerService],
})
export class PowerModule {}
```

**Step 2: Import Power Module into CPU Module**

```typescript
import { Module } from "@nestjs/common";
import { CpuService } from "./cpu.service";
import { PowerModule } from "../power/power.module";

@Module({
  imports: [PowerModule],
  providers: [CpuService],
})
export class CpuModule {}
```

**Step 3: Inject Power Service into CPU Service**

```typescript
import { Injectable } from "@nestjs/common";
import { PowerService } from "../power/power.service";

@Injectable()
export class CpuService {
  constructor(private powerService: PowerService) {}

  compute(a: number, b: number): number {
    console.log("Drawing 10 watts of power from power service");
    this.powerService.supplyPower(10);
    return a + b;
  }
}
```

#### Three-Step Pattern for Sharing Services

| Step | Action                           | Module                      |
| ---- | -------------------------------- | --------------------------- |
| 1    | Add service to `exports`         | Provider Module             |
| 2    | Add provider module to `imports` | Consumer Module             |
| 3    | Inject service in constructor    | Consumer Service/Controller |

#### Repeating the Pattern for Disk Service

Same three steps for DiskModule and DiskService:

```typescript
// disk.module.ts
@Module({
  imports: [PowerModule],
  providers: [DiskService],
})
export class DiskModule {}

// disk.service.ts
@Injectable()
export class DiskService {
  constructor(private powerService: PowerService) {}

  getData(): string {
    console.log("Drawing 20 watts of power from power service");
    this.powerService.supplyPower(20);
    return "Data from disk";
  }
}
```

#### Service Hierarchy

```
PowerService (no dependencies)
    ↑
    ├── CpuService (depends on PowerService)
    └── DiskService (depends on PowerService)
```

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.5+–+Consuming+Multiple+Modules" alt="Lecture 6.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture shows how to use multiple services in a single module/controller through dependency injection.

#### Connecting Computer Module to CPU and Disk Modules

**Step 1: Export Services from CPU and Disk Modules**

CPU Module:

```typescript
@Module({
  imports: [PowerModule],
  providers: [CpuService],
  exports: [CpuService],
})
export class CpuModule {}
```

Disk Module:

```typescript
@Module({
  imports: [PowerModule],
  providers: [DiskService],
  exports: [DiskService],
})
export class DiskModule {}
```

**Step 2: Import Both Modules into Computer Module**

```typescript
import { Module } from "@nestjs/common";
import { ComputerController } from "./computer.controller";
import { CpuModule } from "../cpu/cpu.module";
import { DiskModule } from "../disk/disk.module";

@Module({
  imports: [CpuModule, DiskModule],
  controllers: [ComputerController],
})
export class ComputerModule {}
```

**Step 3: Inject Both Services into Controller**

```typescript
import { Controller, Get } from "@nestjs/common";
import { CpuService } from "../cpu/cpu.service";
import { DiskService } from "../disk/disk.service";

@Controller("computer")
export class ComputerController {
  constructor(
    private cpuService: CpuService,
    private diskService: DiskService
  ) {}

  @Get()
  run() {
    return [this.cpuService.compute(1, 2), this.diskService.getData()];
  }
}
```

#### Testing the Integration

**Route Handler: GET /computer**

```bash
curl http://localhost:3000/computer
```

**Expected Response:**

```json
[3, "Data from disk"]
```

**Console Output:**

```
Drawing 10 watts of power from power service
Supplying 10 watts of power
Drawing 20 watts of power from power service
Supplying 20 watts of power
```

#### Complete Dependency Flow

```
HTTP Request (GET /computer)
    ↓
ComputerController
    ├→ CpuService.compute(1, 2)
    │    ↓
    │    PowerService.supplyPower(10)
    │
    └→ DiskService.getData()
         ↓
         PowerService.supplyPower(20)
```

#### Key Takeaways

- Multiple services can be injected into a single class
- Services are instantiated once and reused
- Dependency resolution happens automatically
- Clean separation of concerns across modules

---

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+6.6+–+Modules+Wrapup" alt="Lecture 6.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture wraps up modules by explaining the relationship between modules, dependency injection, and scoping.

#### Module Architecture Diagram

**Power Module Container:**

```
Power Module
├── Providers:
│   └── PowerService
├── Exports:
│   └── PowerService
```

**CPU Module Container:**

```
CPU Module
├── Imports:
│   └── PowerModule
├── Providers:
│   └── CpuService
└── (CpuService can access PowerService from exports)
```

#### Scoping and Visibility

| Concept      | Meaning                                         |
| ------------ | ----------------------------------------------- |
| **Private**  | Service only available within its module        |
| **Exported** | Service available to modules that import        |
| **Imported** | Access to exported services from another module |
| **Scoped**   | Services are limited in what they can access    |

#### Single Container Model

**Behind the Scenes:**

Although modules appear as separate containers, NestJS actually:

1. Creates a **single application container**
2. **Scopes** access based on module imports
3. Allows **service sharing** through exports
4. Maintains **encapsulation** boundaries

```
Single Container (Logical View)
├── PowerService (available to all that import)
├── CpuService (available to Computer via CpuModule)
├── DiskService (available to Computer via DiskModule)
└── ComputerController (orchestrates CPU and Disk)
```

#### The Three-Step Pattern (Summary)

**Always follow this pattern to share code between modules:**

1. **Export** - Add service to `exports` in provider module
2. **Import** - Add provider module to `imports` in consumer module
3. **Inject** - Add service to constructor in consumer class

#### Hierarchical Module Structure

```
RootModule (Computer)
├── imports: [CpuModule, DiskModule]
│
├── CpuModule
│   └── imports: [PowerModule]
│       └── providers: [CpuService]
│
├── DiskModule
│   └── imports: [PowerModule]
│       └── providers: [DiskService]
│
└── PowerModule
    └── providers: [PowerService]
```

#### Benefits of Module Organization

| Benefit             | Example                                    |
| ------------------- | ------------------------------------------ |
| **Maintainability** | Each module has single responsibility      |
| **Reusability**     | Services exported for use elsewhere        |
| **Testability**     | Easy to mock dependencies                  |
| **Scalability**     | Add new modules without affecting existing |
| **Organization**    | Clear structure and hierarchy              |

#### Key Takeaways

1. Modules organize related code together
2. Dependency injection handles service instantiation
3. Exports control what's available to other modules
4. Imports make services from other modules available
5. Constructors inject dependencies needed
6. Single container with scoped visibility behind the scenes

#### Moving Forward

This module system is foundational for building:

- Large applications with multiple features
- Shared utility modules (auth, database, etc.)
- Feature modules that can be independently developed
- Testable, maintainable code architecture

## Section 7: Big Project Time!

This section introduces a larger, more complex application - a **Used Car Pricing API**. The focus shifts from basic concepts to real-world application architecture, including authentication, authorization, database integration, and data validation.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=500&lines=🎬+Lecture+7.1+–+App+Overview" alt="Lecture 7.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces the next major project: a **Used Car Pricing API** that helps users estimate the value of their vehicles and crowdsources real market data through user-submitted sales reports.

#### Application Overview

The Used Car Pricing API solves a common problem: determining how much a used car is worth. The application combines user authentication, data estimation algorithms, and administrative oversight to create a reliable pricing tool.

#### Core Features

1. **User Authentication**
   - Users sign up with email and password
   - Secure authentication required for all features
   - Session management for logged-in users

2. **Vehicle Value Estimation**
   - Users request price estimates for their vehicles
   - Estimates based on:
     - Make (manufacturer)
     - Model (vehicle name)
     - Year (manufacture year)
     - Mileage (total distance driven)
     - Location (latitude and longitude)

3. **Sales Report Submission**
   - After selling their vehicle, users can report the actual sale price
   - This data enriches the pricing database
   - Creates a feedback loop for more accurate future estimates

4. **Administrative Oversight**
   - Administrators review all submitted sales reports
   - Prevents fraudulent or inaccurate data (e.g., $0 sales or $5 million sales)
   - Approve or reject reports before adding them to the dataset

#### Application Flow

```
User Registration/Login
         ↓
Request Vehicle Estimate
         ↓
Sell Vehicle (external)
         ↓
Submit Sale Report
         ↓
Admin Reviews Report → [Approved/Rejected]
         ↓
Data Added to Dataset (if approved)
         ↓
Improved Future Estimates
```

#### Why This Project Matters

**Real-World Complexity**: Unlike the simple messages application, this project includes:

- User authentication and authorization
- Database relationships between entities
- Data validation and business rules
- Role-based access control (regular users vs administrators)
- Complex query logic for price estimation

**Industry Standard Practices**: This application demonstrates:

- Proper separation of concerns
- Service-oriented architecture
- Data integrity through administrative review
- Secure user management

#### What You'll Learn

- Building authentication systems in NestJS
- Implementing role-based authorization
- Designing relational database schemas
- Creating complex business logic
- Handling data validation and transformation
- Building RESTful APIs with proper HTTP methods
- Managing application state and user sessions

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=500&lines=🎬+Lecture+7.2+–+API+Design" alt="Lecture 7.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture focuses on designing the API routes and endpoints needed to support all application features. Route design is a critical first step in building any API.

#### Complete API Route Design

| Method | Route        | Body/Query String Data                                           | Description                                       |
| ------ | ------------ | ---------------------------------------------------------------- | ------------------------------------------------- |
| POST   | /auth/signup | Body: { email, password }                                        | Create new user account and sign in               |
| POST   | /auth/signin | Body: { email, password }                                        | Sign in existing user                             |
| GET    | /reports     | Query: ?make&model&year&mileage&longitude&latitude               | Get estimated vehicle value                       |
| POST   | /reports     | Body: { make, model, year, mileage, longitude, latitude, price } | Submit a vehicle sale report                      |
| PATCH  | /reports/:id | Body: { approved }                                               | Approve or reject a submitted report (Admin only) |

#### Route Details and Rationale

**Authentication Routes**

**POST /auth/signup**

- **Purpose**: Register new users
- **Request Body**:
  ```json
  {
    "email": "user@example.com",
    "password": "securePassword123"
  }
  ```
- **Response**: User object with authentication token/session
- **Why POST**: Creating a new resource (user account)

**POST /auth/signin**

- **Purpose**: Authenticate existing users
- **Request Body**:
  ```json
  {
    "email": "user@example.com",
    "password": "securePassword123"
  }
  ```
- **Response**: User object with authentication token/session
- **Why POST**: While not creating a resource, login is not idempotent and may create sessions

**Report Routes**

**GET /reports (Estimate)**

- **Purpose**: Get estimated value for a vehicle
- **Query String Example**:
  ```
  /reports?make=honda&model=civic&year=2015&mileage=50000&longitude=-122.4194&latitude=37.7749
  ```
- **Response**: Simple price estimate
  ```json
  {
    "estimatedValue": 12500
  }
  ```
- **Why GET**: Reading data, no modifications
- **Why Query String**: Filtering criteria, not creating a resource

**POST /reports (Submit Sale)**

- **Purpose**: Submit actual sale data to improve estimates
- **Request Body**:
  ```json
  {
    "make": "honda",
    "model": "civic",
    "year": 2015,
    "mileage": 50000,
    "longitude": -122.4194,
    "latitude": 37.7749,
    "price": 12000
  }
  ```
- **Response**: Created report object
- **Why POST**: Creating a new resource (sale report)
- **Authentication Required**: Yes

**PATCH /reports/:id (Admin Approval)**

- **Purpose**: Approve or reject submitted reports
- **URL Parameter**: Report ID (e.g., `/reports/123`)
- **Request Body**:
  ```json
  {
    "approved": true
  }
  ```
- **Response**: Updated report object
- **Why PATCH**: Partial update of existing resource
- **Authorization Required**: Admin role only

#### Design Considerations

**Query String vs Request Body**

- **Query Strings**: Used for filtering, searching, or reading data (GET requests)
- **Request Body**: Used for creating or updating data (POST, PATCH, PUT requests)

**Resource Naming**

- Use plural nouns (`/reports`, not `/report`)
- Keep URLs simple and predictable
- Use path parameters for specific resources (`/reports/:id`)

**HTTP Method Selection**

- **GET**: Retrieve data (safe, idempotent)
- **POST**: Create new resources (not idempotent)
- **PATCH**: Partially update resources (idempotent)
- **PUT**: Replace entire resources (idempotent)
- **DELETE**: Remove resources (idempotent)

#### Potential Future Routes

As mentioned in the lecture, this initial design will likely evolve. Possible additions:

- `GET /auth/whoami` - Get current user information
- `GET /users/:id` - Get specific user details
- `PATCH /users/:id` - Update user information
- `GET /reports/:id` - Get specific report details
- `DELETE /reports/:id` - Delete a report (Admin)

#### Why This Matters

**Proper API design is crucial because**:

- URLs are contracts with clients - changing them breaks applications
- Good design makes APIs intuitive and easy to use
- RESTful conventions create predictability
- Clear separation of concerns improves maintainability
- Proper HTTP method usage enables caching and optimization

**Planning before coding**:

- Reduces refactoring later
- Identifies missing features early
- Helps estimate development time
- Creates documentation naturally

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=550&lines=🎬+Lecture+7.3+–+Module+Design" alt="Lecture 7.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to organize NestJS applications using modules and demonstrates the standard pattern for structuring controllers, services, and repositories around application resources.

#### Identifying Application Resources

By analyzing the API routes, we can identify two primary resources:

1. **Users** - Handles authentication and user management
2. **Reports** - Handles vehicle sale reports and price estimates

#### Standard Module Structure Pattern

For each resource, create:

- **One Controller** - Handles routing and HTTP requests
- **One Service** - Contains business logic
- **One Repository** - Manages database operations
- **One Module** - Wraps and organizes these components

#### Application Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        App Module                            │
│  (Root module that imports all feature modules)              │
└─────────────────────────────────────────────────────────────┘
                           │
           ┌───────────────┴───────────────┐
           │                               │
           ▼                               ▼
┌──────────────────────┐        ┌──────────────────────┐
│   Users Module       │        │  Reports Module      │
├──────────────────────┤        ├──────────────────────┤
│ • UsersController    │        │ • ReportsController  │
│ • UsersService       │        │ • ReportsService     │
│ • UsersRepository    │        │ • ReportsRepository  │
└──────────────────────┘        └──────────────────────┘
```

#### Users Module Components

**UsersController**

- Handles: `/auth/signup`, `/auth/signin`
- Validates incoming request data
- Returns HTTP responses
- Delegates business logic to UsersService

**UsersService**

- Implements authentication logic
- Password hashing and verification
- Session management
- User creation and retrieval
- Uses UsersRepository for data access

**UsersRepository**

- Database CRUD operations for users
- Queries and filtering
- Abstracts database implementation details

#### Reports Module Components

**ReportsController**

- Handles: `GET /reports`, `POST /reports`, `PATCH /reports/:id`
- Request validation
- Response formatting
- Delegates to ReportsService

**ReportsService**

- Price estimation algorithm
- Report creation logic
- Report approval workflow
- Business rules (e.g., reasonable price ranges)
- Uses ReportsRepository for data access

**ReportsRepository**

- Database CRUD for reports
- Complex queries for price estimation
- Filtering and aggregation
- Data persistence

#### Why Use Modules?

**Separation of Concerns**

- Each module focuses on a single resource or feature
- Clear boundaries between different parts of the application
- Easier to understand and maintain

**Reusability**

- Modules can be easily shared between projects
- Encapsulated functionality is portable
- Can be published as npm packages

**Team Collaboration**

- Different teams can work on different modules
- Reduced merge conflicts
- Clear ownership of code

**Dependency Management**

- Modules explicitly declare their dependencies
- NestJS manages dependency injection between modules
- Easy to see what each module needs

**Testing**

- Modules can be tested in isolation
- Mock dependencies easily
- Unit and integration testing simplified

#### Module Design Best Practices

1. **One Resource Per Module**: Keep related functionality together
2. **Single Responsibility**: Each module should have one clear purpose
3. **Explicit Dependencies**: Always declare what you need in the module decorator
4. **Minimal Exports**: Only export what other modules need to use
5. **Logical Grouping**: Group by feature/domain, not by technical type

#### Common Mistake to Avoid

❌ **Don't organize by technical type**:

```
controllers/
  - users.controller.ts
  - reports.controller.ts
services/
  - users.service.ts
  - reports.service.ts
```

✅ **Do organize by feature/domain**:

```
users/
  - users.controller.ts
  - users.service.ts
  - users.repository.ts
  - users.module.ts
reports/
  - reports.controller.ts
  - reports.service.ts
  - reports.repository.ts
  - reports.module.ts
```

#### Module Evolution

As mentioned in the lecture, this initial design will evolve as we build the application. We might need to:

- Add more modules (e.g., AuthModule separate from UsersModule)
- Create shared modules for common utilities
- Add DTOs (Data Transfer Objects) for validation
- Include middleware, guards, and interceptors

#### Why This Matters

Starting with a clear module structure:

- Provides a solid foundation for growth
- Makes the codebase easier to navigate
- Improves long-term maintainability
- Follows NestJS best practices and conventions
- Scales well as features are added

Even though we'll need to adjust the structure later, having a clear starting point based on identified resources is crucial for organized development.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=800&lines=🎬+Lecture+7.4+–+Generating+Modules,+Controllers,+and+Services" alt="Lecture 7.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to use the Nest CLI to quickly generate all necessary modules, controllers, and services. It also explains why repositories are created manually rather than generated automatically.

#### Project Initialization

**Create the NestJS Project**

```bash
nest new mycv
```

**Select Package Manager**

- Choose NPM or Yarn when prompted
- Project name: `mycv` (short for "My Car Value")

#### Using the Nest CLI Generator

The Nest CLI provides the `generate` (or `g`) command to create various NestJS components automatically.

**Basic Syntax**

```bash
nest generate <schematic> <name>
# or shorthand
nest g <schematic> <name>
```

#### Generating All Components

**Step 1: Create Modules**

```bash
nest g module users
nest g module reports
```

**What This Creates**:

- `src/users/users.module.ts`
- `src/reports/reports.module.ts`
- Automatically imports modules into `app.module.ts`

**Step 2: Create Controllers**

```bash
nest g controller users
nest g controller reports
```

**What This Creates**:

- `src/users/users.controller.ts`
- `src/users/users.controller.spec.ts` (test file)
- `src/reports/reports.controller.ts`
- `src/reports/reports.controller.spec.ts` (test file)
- Automatically adds controllers to their respective module files

**Step 3: Create Services**

```bash
nest g service users
nest g service reports
```

**What This Creates**:

- `src/users/users.service.ts`
- `src/users/users.service.spec.ts` (test file)
- `src/reports/reports.service.ts`
- `src/reports/reports.service.spec.ts` (test file)
- Automatically adds services to the providers array in their modules

#### Complete CLI Command Sequence

```bash
# Navigate to project directory
cd mycv

# Generate modules
nest g module users
nest g module reports

# Generate controllers
nest g controller users
nest g controller reports

# Generate services
nest g service users
nest g service reports
```

#### Generated File Structure

```
mycv/
└── src/
    ├── app.module.ts           (updated with new modules)
    ├── main.ts
    ├── users/
    │   ├── users.controller.ts
    │   ├── users.controller.spec.ts
    │   ├── users.service.ts
    │   ├── users.service.spec.ts
    │   └── users.module.ts
    └── reports/
        ├── reports.controller.ts
        ├── reports.controller.spec.ts
        ├── reports.service.ts
        ├── reports.service.spec.ts
        └── reports.module.ts
```

#### Automatic Module Updates

**app.module.ts** (automatically updated)

```typescript
import { Module } from "@nestjs/common";
import { UsersModule } from "./users/users.module";
import { ReportsModule } from "./reports/reports.module";

@Module({
  imports: [UsersModule, ReportsModule],
})
export class AppModule {}
```

**users.module.ts** (automatically populated)

```typescript
import { Module } from "@nestjs/common";
import { UsersController } from "./users.controller";
import { UsersService } from "./users.service";

@Module({
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule {}
```

**reports.module.ts** (automatically populated)

```typescript
import { Module } from "@nestjs/common";
import { ReportsController } from "./reports.controller";
import { ReportsService } from "./reports.service";

@Module({
  controllers: [ReportsController],
  providers: [ReportsService],
})
export class ReportsModule {}
```

#### Why Not Generate Repositories?

**Repositories are NOT generated by the CLI because**:

1. **Implementation Varies**: Repositories depend heavily on the chosen database solution
   - TypeORM repositories work differently than Mongoose schemas
   - Prisma has its own client
   - Raw SQL requires different approaches

2. **No Standard Pattern**: Unlike controllers and services, there's no universal repository pattern in NestJS
   - Some use TypeORM's Repository class
   - Others use Mongoose models
   - Some prefer custom repository implementations

3. **Manual Control Needed**:
   - Repository implementation should match your database choice
   - Custom methods vary by application needs
   - Data access patterns are application-specific

4. **Future Flexibility**: Creating repositories manually keeps options open for:
   - Switching databases
   - Adding caching layers
   - Implementing custom query optimization

#### Next Steps

After generating these files:

1. **Choose a database** (e.g., SQLite, PostgreSQL, MongoDB)
2. **Install ORM/ODM** (e.g., TypeORM, Prisma, Mongoose)
3. **Create entities** (database schemas/models)
4. **Manually create repositories** based on chosen database solution
5. **Implement business logic** in services
6. **Define routes** in controllers

#### CLI Generator Options

**Useful Nest CLI Flags**

```bash
# Skip test file generation
nest g service users --no-spec

# Generate in a specific directory
nest g controller users/auth

# Dry run (preview without creating files)
nest g module users --dry-run

# Flat structure (don't create folder)
nest g service users --flat
```

**Available Schematics**

- `module` - Generate a module
- `controller` - Generate a controller
- `service` - Generate a service
- `guard` - Generate a guard
- `interceptor` - Generate an interceptor
- `filter` - Generate an exception filter
- `pipe` - Generate a pipe
- `middleware` - Generate middleware
- `decorator` - Generate a custom decorator
- `gateway` - Generate a WebSocket gateway
- `resolver` - Generate a GraphQL resolver

#### Why This Matters

**Using the Nest CLI**:

- ✅ Saves time - no manual file creation
- ✅ Ensures consistency - follows naming conventions
- ✅ Automatic wiring - updates module imports
- ✅ Includes boilerplate - basic structure included
- ✅ Creates tests - spec files for unit testing
- ✅ Prevents typos - reduces human error

**Benefits for Team Development**:

- Everyone uses the same structure
- Onboarding is easier
- Code reviews focus on logic, not structure
- Refactoring is simpler
- Project organization is predictable

#### Common Mistakes to Avoid

❌ **Don't manually create files that can be generated**

- Wastes time
- May miss important boilerplate
- Won't automatically update modules

❌ **Don't forget to navigate to the project directory**

- CLI commands must run from project root
- Otherwise, files are created in wrong location

❌ **Don't skip planning before generating**

- Think about module structure first
- Avoid generating unnecessary components
- Consider feature organization

✅ **Do use the CLI for all standard components**
✅ **Do review generated files** to understand the structure
✅ **Do customize generated code** to fit your needs

---

## Key Takeaways from Section 7

**Planning is Essential**

- Design API routes before writing code
- Identify resources and their relationships
- Plan module structure based on features

**Use the Right Tools**

- Nest CLI automates repetitive tasks
- Follow NestJS conventions and patterns
- Leverage built-in generators

**Think About Architecture**

- Organize by feature/resource, not technical type
- Use modules to create clear boundaries
- Keep separation of concerns

**Real-World Applications Require**

- Authentication and authorization
- Database integration
- Data validation
- Administrative oversight
- Proper error handling

**Start Simple, Iterate**

- Initial designs will evolve
- Build foundation first
- Refactor as requirements become clear

---

## What's Next

In the following lectures, you will:

1. Set up a database (SQLite with TypeORM)
2. Create entity definitions (User and Report)
3. Build repositories for data access
4. Implement authentication logic
5. Add validation with DTOs
6. Create guards for authorization
7. Implement the price estimation algorithm
8. Add admin approval workflow

This project will demonstrate how all NestJS concepts work together in a real application.

## Section 8: Persisting Data with TypeORM

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.1+–+Persistent+Data+with+Nest" alt="Lecture 8.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture introduces database integration with NestJS using TypeORM. Instead of storing data in plain files, this application will use a real database solution with SQLite initially, then transition to PostgreSQL later.

#### Database Options with NestJS

NestJS works with virtually any database, but two solutions integrate particularly well out of the box:

| Library      | Database Support                                  | Course Focus |
| ------------ | ------------------------------------------------- | ------------ |
| **TypeORM**  | SQL databases (MySQL, PostgreSQL, etc.) + MongoDB | ✅ Primary   |
| **Mongoose** | MongoDB only                                      | ❌           |

#### Why TypeORM + NestJS?

TypeORM and NestJS are a "match made in heaven" - they cooperate fantastically and support each other. NestJS provides tools that make TypeORM a pleasure to use, compensating for areas where TypeORM can be deficient or hard to use standalone.

#### Database Choice Strategy

**Initial Setup:**

- **Database:** SQLite
- **Reason:** Easy to use and get started with
- **Purpose:** Development and learning

**Production Setup:**

- **Database:** PostgreSQL
- **Reason:** More robust, production-ready solution
- **Purpose:** Final application deployment

#### Required Dependencies Installation

```bash
npm install @nestjs/typeorm typeorm sqlite3
```

#### Dependencies Breakdown

| Dependency        | Purpose                                                     |
| ----------------- | ----------------------------------------------------------- |
| `@nestjs/typeorm` | Integration layer making TypeORM and NestJS work together   |
| `typeorm`         | The TypeORM library itself                                  |
| `sqlite3`         | SQLite database client (temporary, will add Postgres later) |

#### Why This Matters

Understanding the separation between NestJS, TypeORM, and the actual database client helps clarify the architecture. TypeORM acts as an abstraction layer that can work with multiple databases, while the specific database client (sqlite3, pg for Postgres) handles the actual connection.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.2+–+Setting+Up+Database+Connection" alt="Lecture 8.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to integrate TypeORM into a NestJS project by setting up a database connection in the App Module. The connection will automatically be shared across all modules in the application.

#### Database Connection Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        App Module                           │
│  ┌──────────────────────────────────────────────────────┐   │
│  │    TypeORM Connection to SQLite Database             │   │
│  └──────────────────────────────────────────────────────┘   │
│                 ↓                          ↓                 │
│     ┌───────────────────────┐  ┌───────────────────────┐   │
│     │    Users Module       │  │   Reports Module      │   │
│     │  ┌─────────────────┐  │  │  ┌─────────────────┐  │   │
│     │  │  User Entity    │  │  │  │  Report Entity  │  │   │
│     │  └─────────────────┘  │  │  └─────────────────┘  │   │
│     │         ↓              │  │         ↓              │   │
│     │  [Auto-generated]      │  │  [Auto-generated]      │   │
│     │  Users Repository      │  │  Reports Repository    │   │
│     └───────────────────────┘  └───────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

#### Three-Step Process

1. **App Module**: Create connection to SQLite database (automatically shared to all modules)
2. **Feature Modules**: Create entity files defining resource structure
3. **Auto-Generation**: NestJS + TypeORM automatically create repositories

#### Configuring App Module

**File:** `src/app.module.ts`

```typescript
import { Module } from "@nestjs/common";
import { TypeOrmModule } from "@nestjs/typeorm";
import { UsersModule } from "./users/users.module";
import { ReportsModule } from "./reports/reports.module";
import { User } from "./users/user.entity";
import { Report } from "./reports/report.entity";

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: "sqlite",
      database: "db.sqlite",
      entities: [User, Report],
      synchronize: true,
    }),
    UsersModule,
    ReportsModule,
  ],
})
export class AppModule {}
```

#### TypeORM Configuration Options

| Option        | Value         | Purpose                                               |
| ------------- | ------------- | ----------------------------------------------------- |
| `type`        | `'sqlite'`    | Specifies the database type (supports many databases) |
| `database`    | `'db.sqlite'` | Name/path of the SQLite database file                 |
| `entities`    | `[...]`       | Array of entity classes to register                   |
| `synchronize` | `true`        | Auto-sync database schema with entities (dev only!)   |

#### ⚠️ Important: The `forRoot()` Method

The `forRoot()` method creates a connection that is automatically shared with all child modules (Users, Reports). This is why nested modules can access the database without additional configuration.

#### Why This Matters

Setting up the connection at the App Module level follows the dependency injection pattern. Child modules receive the connection automatically, promoting code reuse and reducing configuration overhead.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FF6B6B&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.3+–+Creating+Entity+and+Repository" alt="Lecture 8.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to create entity files that define resource structure and how TypeORM automatically generates repositories from these entities.

#### Understanding Entities vs Repositories

**Entity**: A class that defines the structure of a resource (like a model)

- Lists all properties a resource should have
- Example: User has id, email, password

**Repository**: Auto-generated class for database operations

- Created automatically by TypeORM + NestJS
- Provides methods like create, save, find, remove
- No manual file creation needed!

#### Three Steps to Create an Entity

1. **Create entity file** with a class listing properties
2. **Connect entity to parent module**
3. **Connect entity to root connection** in App Module

#### Step 1: Create User Entity File

**File:** `src/users/user.entity.ts`

```typescript
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Column()
  password: string;
}
```

#### TypeORM Decorators Explained

| Decorator                   | Purpose                              |
| --------------------------- | ------------------------------------ |
| `@Entity()`                 | Marks class as a database table      |
| `@PrimaryGeneratedColumn()` | Auto-incrementing primary key column |
| `@Column()`                 | Regular column to store data         |

#### Naming Convention Note

**Exception to the Rule**: Entity classes are named without the "Entity" suffix by community convention.

- ✅ Correct: `export class User`
- ❌ Not typical: `export class UserEntity`

You can use `UserEntity` if you prefer, but `User` is the standard convention.

#### Step 2: Connect Entity to Users Module

**File:** `src/users/users.module.ts`

```typescript
import { Module } from "@nestjs/common";
import { TypeOrmModule } from "@nestjs/typeorm";
import { UsersController } from "./users.controller";
import { UsersService } from "./users.service";
import { User } from "./user.entity";

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule {}
```

#### Step 3: Connect Entity to Root Connection

**Already completed in App Module** - we added the User entity to the `entities` array in the TypeORM configuration.

#### The Result: Auto-Generated Repository

After these three steps, TypeORM automatically creates a **UsersRepository** class with methods for database operations. You don't see a file, but the class exists and can be injected into services.

#### Why This Matters

The entity-driven approach means you define your data structure once, and TypeORM handles the database schema creation and provides a complete API for data operations automatically.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFD93D&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.4+–+Viewing+Database+Contents" alt="Lecture 8.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates creating a Report entity for practice and introduces tools for viewing SQLite database contents in VS Code.

#### Creating the Report Entity (Practice)

Following the same three-step process for the Reports module.

**Step 1: Create Report Entity File**

**File:** `src/reports/report.entity.ts`

```typescript
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity()
export class Report {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  price: number;
}
```

**Step 2: Connect to Reports Module**

**File:** `src/reports/reports.module.ts`

```typescript
import { Module } from "@nestjs/common";
import { TypeOrmModule } from "@nestjs/typeorm";
import { ReportsController } from "./reports.controller";
import { ReportsService } from "./reports.service";
import { Report } from "./report.entity";

@Module({
  imports: [TypeOrmModule.forFeature([Report])],
  controllers: [ReportsController],
  providers: [ReportsService],
})
export class ReportsModule {}
```

**Step 3: Connect to Root Connection**

**File:** `src/app.module.ts`

```typescript
import { Report } from "./reports/report.entity";

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: "sqlite",
      database: "db.sqlite",
      entities: [User, Report], // Add Report here
      synchronize: true,
    }),
    // ...
  ],
})
export class AppModule {}
```

#### Understanding the Database File

- SQLite stores data in a plain file: `db.sqlite`
- This file is automatically created in the project root
- The file contains binary data and cannot be viewed as plain text

#### Viewing SQLite Database in VS Code

**Recommended Extension:**

- **Name:** SQLite Viewer (or similar)
- **Purpose:** View and browse SQLite database contents
- **Access:** Extensions → Search "SQLite" → Install

**Using the Extension:**

1. Click on `db.sqlite` file in the file explorer
2. The extension automatically displays database contents
3. View tables, columns, and data in a user-friendly interface

#### What You Should See

After starting the application with entities configured:

```
📁 db.sqlite
  ├── 📊 Table: user
  │   ├── id (INTEGER PRIMARY KEY)
  │   ├── email (VARCHAR)
  │   └── password (VARCHAR)
  │
  └── 📊 Table: report
      ├── id (INTEGER PRIMARY KEY)
      └── price (INTEGER)
```

#### Why This Matters

Viewing the database contents helps verify that TypeORM's `synchronize: true` setting is working correctly - it automatically created tables matching your entity definitions without manual SQL or migrations.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=A78BFA&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.5+–+Understanding+TypeORM+Decorators" alt="Lecture 8.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture provides an in-depth explanation of TypeORM decorators and the crucial `synchronize` option that automatically manages database schema.

#### The Critical `synchronize` Setting

**File:** `src/app.module.ts`

```typescript
TypeOrmModule.forRoot({
  type: "sqlite",
  database: "db.sqlite",
  entities: [User, Report],
  synchronize: true, // ⚠️ DEVELOPMENT ONLY!
});
```

#### Understanding Synchronize: True

**What it does:**

- Automatically reads entity structure
- Updates database schema to match entities
- Creates/removes tables and columns
- Changes column data types

**⚠️ Critical Warning:**

- **USE ONLY IN DEVELOPMENT**
- Never use in production
- Can cause data loss
- Replaces traditional migration workflow

#### Traditional Database Workflow (Production)

```
┌─────────────────────────────────────────────────────────────┐
│  Database: users table                                      │
│  ┌──────┬───────────────┬──────────────┐                   │
│  │  id  │     email     │   password   │                   │
│  └──────┴───────────────┴──────────────┘                   │
└─────────────────────────────────────────────────────────────┘
                         ↓
         Want to add a new column (username)
                         ↓
┌─────────────────────────────────────────────────────────────┐
│  Write a Migration                                          │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ALTER TABLE users ADD COLUMN username VARCHAR;     │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│  Database: users table                                      │
│  ┌──────┬───────────┬──────────┬──────────────┐            │
│  │  id  │   email   │ password │   username   │            │
│  └──────┴───────────┴──────────┴──────────────┘            │
└─────────────────────────────────────────────────────────────┘
```

#### Synchronize Workflow (Development)

```
┌─────────────────────────────────────────────────────────────┐
│  Entity: User                                               │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  id: number                                         │   │
│  │  email: string                                      │   │
│  │  password: string                                   │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                         ↓
              TypeORM reads entity
                         ↓
┌─────────────────────────────────────────────────────────────┐
│  Database automatically created/updated                     │
│  ┌──────┬───────────────┬──────────────┐                   │
│  │  id  │     email     │   password   │                   │
│  └──────┴───────────────┴──────────────┘                   │
└─────────────────────────────────────────────────────────────┘
```

#### TypeORM Decorator Deep Dive

**File:** `src/users/user.entity.ts`

```typescript
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity() // Creates a "user" table (class name lowercase & pluralized)
export class User {
  @PrimaryGeneratedColumn() // Auto-incrementing primary key
  id: number;

  @Column() // Creates a VARCHAR column
  email: string;

  @Column() // Creates a VARCHAR column
  password: string;
}
```

#### Decorator Mapping to Database

| Decorator                   | Database Result                             |
| --------------------------- | ------------------------------------------- |
| `@Entity()`                 | Creates table named "user"                  |
| `@PrimaryGeneratedColumn()` | INTEGER PRIMARY KEY AUTO_INCREMENT column   |
| `@Column()`                 | VARCHAR/TEXT column (type inferred from TS) |

#### Type Inference

TypeORM uses TypeScript type information to determine database column types:

| TypeScript Type | Database Type (SQLite) |
| --------------- | ---------------------- |
| `number`        | INTEGER                |
| `string`        | VARCHAR/TEXT           |
| `boolean`       | BOOLEAN                |
| `Date`          | DATETIME               |

#### Advanced Column Options (Preview)

```typescript
@Column({ type: 'varchar', length: 255 })
email: string;

@Column({ unique: true })
email: string;

@Column({ nullable: true })
middleName: string;

@Column({ default: false })
isActive: boolean;
```

#### Why This Matters

Understanding `synchronize: true` is critical because:

1. It's incredibly convenient for development
2. It's dangerous in production (can destroy data)
3. It demonstrates TypeORM's tight integration with TypeScript's type system
4. It eliminates the need for manual schema management during development

**Best Practice:** Use `synchronize: true` in development, switch to migrations for production.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=F59E0B&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.6+–+Quick+Note+on+Repositories" alt="Lecture 8.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture clarifies the difference between entities and repositories, explains repository methods, and addresses TypeORM's multiple-ways-to-do-things problem.

#### Entity vs Repository: Clear Distinction

| Concept        | What It Is                        | Purpose                                    |
| -------------- | --------------------------------- | ------------------------------------------ |
| **Entity**     | Class defining data structure     | Lists properties of a resource             |
| **Repository** | Auto-generated class with methods | Provides database operations for an entity |

**Key Point:** When using TypeORM with NestJS, you **DO NOT** manually create repository files. They are auto-generated behind the scenes.

#### Repository API Overview

**Official Docs:** [TypeORM Repository API](https://typeorm.io/repository-api)

#### Common Repository Methods

| Method      | Purpose                                     |
| ----------- | ------------------------------------------- |
| `create()`  | Creates a new instance (doesn't save to DB) |
| `save()`    | Saves one or more entities to database      |
| `find()`    | Finds multiple entities matching criteria   |
| `findOne()` | Finds a single entity by ID or criteria     |
| `remove()`  | Removes one or more entities from database  |

#### Example Usage (Preview)

```typescript
// In a service
const user = this.repo.create({ email: "test@test.com", password: "password" });
await this.repo.save(user);

const users = await this.repo.find({ email: "test@test.com" });
const user = await this.repo.findOne({ where: { id: 1 } });

await this.repo.remove(user);
```

#### ⚠️ TypeORM's Multiple Ways Problem

TypeORM often provides **multiple methods that seem to do the same thing**. This can be confusing.

**Examples:**

| Similar Methods                      | Purpose      | Key Difference                                                |
| ------------------------------------ | ------------ | ------------------------------------------------------------- |
| `save()` vs `insert()` vs `update()` | Persist data | `save()` can insert OR update, others are specific            |
| `remove()` vs `delete()`             | Delete data  | `remove()` requires entity instance, `delete()` uses criteria |
| `find()` vs `createQueryBuilder()`   | Query data   | Different levels of control and complexity                    |

#### Understanding the Differences

**`save()` vs `insert()`:**

- `save()`: Checks if entity exists (by ID), inserts or updates accordingly
- `insert()`: Always performs INSERT, fails if entity exists
- `update()`: Always performs UPDATE, requires entity to exist

**`remove()` vs `delete()`:**

- `remove()`: Requires entity instance, triggers lifecycle hooks
- `delete()`: Deletes by criteria, faster, no hooks

#### Why Multiple Approaches Exist

The differences come down to fine-grained database behavior:

- Performance optimization
- Transaction handling
- Lifecycle hooks
- Cascade operations

#### Learning Approach

You don't need to memorize all methods. The course will:

1. Use the most common, practical methods
2. Explain when and why to use specific approaches
3. Help you understand the underlying SQL behavior

#### Why This Matters

Understanding that repositories are auto-generated helps distinguish between:

- **What you write:** Entity definitions
- **What TypeORM provides:** Repository classes with database methods

This is a fundamental concept in TypeORM's architecture and one of its biggest advantages - you define structure, it provides functionality.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=10B981&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.7+–+A+Few+Extra+Routes" alt="Lecture 8.7" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture outlines the approach for building initial route handlers to learn TypeORM, before implementing the final authentication system.

#### Learning Strategy: Temporary Routes

Before building the final authentication system (signup/signin), we'll create several basic CRUD routes to understand TypeORM better.

#### Temporary Routes (For Learning)

| Route             | Method | Purpose                         |
| ----------------- | ------ | ------------------------------- |
| `/auth/signup`    | POST   | Create a new user               |
| `/auth/:id`       | GET    | Find user with specific ID      |
| `/auth?email=...` | GET    | Find all users with given email |
| `/auth/:id`       | PATCH  | Update user with specific ID    |
| `/auth/:id`       | DELETE | Delete user with specific ID    |

**Note:** These routes are **temporary** - some will be removed or modified for the final application.

#### Route Handler Mapping

**Controller Methods:**

```typescript
// users.controller.ts
class UsersController {
  createUser(); // POST /auth/signup
  findUser(); // GET /auth/:id
  findAllUsers(); // GET /auth?email=...
  updateUser(); // PATCH /auth/:id
  removeUser(); // DELETE /auth/:id
}
```

#### Service Methods

**Matching service methods:**

```typescript
// users.service.ts
class UsersService {
  create(); // Called by createUser()
  findOne(); // Called by findUser()
  find(); // Called by findAllUsers()
  update(); // Called by updateUser()
  remove(); // Called by removeUser()
}
```

#### Request Flow Example

```
HTTP Request: POST /auth/signup
                ↓
    UsersController.createUser()
                ↓
       UsersService.create()
                ↓
       UsersRepository.create()
       UsersRepository.save()
                ↓
          SQLite Database
```

#### Why Multiple Layers?

This layered architecture might seem redundant, but it provides:

1. **Separation of Concerns**
   - Controller: HTTP handling
   - Service: Business logic
   - Repository: Database operations

2. **Flexibility**
   - Easy to add authentication logic
   - Simple to add validation
   - Can reuse service methods

3. **Testability**
   - Each layer can be tested independently
   - Mock dependencies easily

#### Password Security Note

**For Now:** Passwords will be stored as plain text
**Later:** We'll implement proper encryption/hashing

This is a learning progression - we'll add security features after understanding the fundamentals.

#### Why This Matters

Creating these temporary routes provides hands-on experience with:

- TypeORM repository methods
- Request/response handling
- Data validation
- The controller → service → repository pattern

Once comfortable with TypeORM, we'll refactor into a proper authentication system.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=EC4899&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.8+–+Setting+Up+Body+Validation" alt="Lecture 8.8" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates setting up request body validation using DTOs (Data Transfer Objects) with class-validator decorators to ensure incoming data meets requirements.

#### Creating the DTO

**File:** `src/users/dtos/create-user.dto.ts`

```typescript
import { IsEmail, IsString } from "class-validator";

export class CreateUserDto {
  @IsEmail()
  email: string;

  @IsString()
  password: string;
}
```

#### Common Validation Decorators

| Decorator      | Purpose                   |
| -------------- | ------------------------- |
| `@IsEmail()`   | Validates email format    |
| `@IsString()`  | Ensures value is a string |
| `@IsNumber()`  | Ensures value is a number |
| `@MinLength()` | Minimum string length     |
| `@MaxLength()` | Maximum string length     |
| `@Min()`       | Minimum numeric value     |
| `@Max()`       | Maximum numeric value     |

#### Applying DTO to Controller

**File:** `src/users/users.controller.ts`

```typescript
import { Body, Controller, Post } from "@nestjs/common";
import { CreateUserDto } from "./dtos/create-user.dto";

@Controller("auth")
export class UsersController {
  @Post("/signup")
  createUser(@Body() body: CreateUserDto) {
    console.log(body);
  }
}
```

#### Enabling Global Validation

**File:** `src/main.ts`

```typescript
import { ValidationPipe } from "@nestjs/common";
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true, // Strip properties not in DTO
    })
  );

  await app.listen(3000);
}
bootstrap();
```

#### ValidationPipe Options

| Option      | Value  | Purpose                                  |
| ----------- | ------ | ---------------------------------------- |
| `whitelist` | `true` | Strips properties that aren't in the DTO |

#### Security: The `whitelist` Option

**Without whitelist:**

```json
// Request body
{
  "email": "test@test.com",
  "password": "password",
  "admin": true // ⚠️ Malicious extra property
}

// Controller receives ALL properties including "admin"
```

**With whitelist: true:**

```json
// Request body
{
  "email": "test@test.com",
  "password": "password",
  "admin": true  // This will be stripped
}

// Controller receives ONLY DTO properties
{
  "email": "test@test.com",
  "password": "password"
}
```

#### Why This Matters

**Security:** Prevents users from injecting unexpected properties that could:

- Elevate privileges (e.g., `admin: true`)
- Modify protected fields
- Cause unexpected application behavior

**Data Integrity:** Ensures only expected data reaches your business logic

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3B82F6&center=true&vCenter=true&width=600&lines=🎬+Lecture+8.9+–+Manual+Route+Testing" alt="Lecture 8.9" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates manual API testing using VS Code's REST Client extension to verify the signup route and validation rules work correctly.

#### Testing Tool Options

| Tool               | Platform          | Course Choice |
| ------------------ | ----------------- | ------------- |
| **REST Client**    | VS Code Extension | ✅ Primary    |
| **Postman**        | Standalone app    | Alternative   |
| **Insomnia**       | Standalone app    | Alternative   |
| **Thunder Client** | VS Code Extension | Alternative   |

#### Creating Test File

**File:** `src/users/requests.http`

This file is placed in the `users` directory since it contains user-specific requests. For applications with multiple controllers, organizing by feature is cleaner than a single root-level file.

```http
### Create a new user
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "password123"
}
```

#### VS Code REST Client Syntax

```http
### Comment describing the request
HTTP_METHOD URL
Header-Name: Header-Value

{
  "json": "body"
}
```

#### Running the Request

1. Install **REST Client** extension in VS Code
2. Open `requests.http` file
3. Click **Send Request** link above the request
4. View response in new tab

#### Test Scenarios

**Scenario 1: Valid Request**

```http
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "password123"
}
```

**Expected Result:**

- Status Code: `200 OK` (or `201 Created`)
- Console logs the body
- Body is validated and accepted

---

**Scenario 2: Invalid Email Format**

```http
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "notanemail",
  "password": "password123"
}
```

**Expected Result:**

- Status Code: `400 Bad Request`
- Error message: `"email must be an email"`

---

**Scenario 3: Missing Property**

```http
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "test@test.com"
}
```

**Expected Result:**

- Status Code: `400 Bad Request`
- Error message: `"password must be a string"`

---

**Scenario 4: Extra Property (Whitelist Test)**

```http
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "password123",
  "admin": true
}
```

**Expected Result:**

- Status Code: `200 OK`
- The `admin` property is **stripped** before reaching the controller
- Console logs only: `{ email: "test@test.com", password: "password123" }`

#### Verifying Whitelist Behavior

**In terminal/console:**

```
// Before whitelist: true
{ email: 'test@test.com', password: 'password123', admin: true }

// After whitelist: true
{ email: 'test@test.com', password: 'password123' }
```

The `admin` property is automatically removed, preventing potential security issues.

#### Multiple Requests in One File

```http
### Create a new user
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "user1@test.com",
  "password": "password123"
}

###

### Create another user
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "user2@test.com",
  "password": "differentpass"
}
```

**Note:** Use `###` to separate multiple requests in the same file.

#### Why This Matters

Manual testing with REST Client provides:

1. **Fast feedback** during development
2. **Version control** - test files committed with code
3. **Documentation** - requests serve as usage examples
4. **No external tools** - everything within VS Code
5. **Validation testing** - confirms DTOs and pipes work correctly

This workflow is essential for rapid iteration when building APIs.

---

## Summary of Section 8

This section covered:

✅ Setting up TypeORM with NestJS
✅ Configuring SQLite database connection
✅ Creating entities with decorators
✅ Understanding auto-generated repositories
✅ The `synchronize: true` development feature
✅ Entity vs Repository distinction
✅ Creating DTOs for validation
✅ Using ValidationPipe with whitelist security
✅ Manual API testing workflow

**Next Steps:** Implementing service methods to interact with the repository and handle business logic.

## Section 9: Creating and Saving User Data

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.1+–+Creating+and+Saving+a+User" alt="Lecture 9.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to create a `create` method in the users service that uses the users repository to save user data to the database. The connection between the service and repository is established using dependency injection.

#### Setting Up Repository Injection

To use a TypeORM repository in a service, we need specific imports:

```typescript
import { Repository } from "typeorm";
import { InjectRepository } from "@nestjs/typeorm";
import { User } from "./user.entity";
```

#### Implementing the Users Service Constructor

```typescript
import { Injectable } from "@nestjs/common";
import { Repository } from "typeorm";
import { InjectRepository } from "@nestjs/typeorm";
import { User } from "./user.entity";

@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private repo: Repository<User>) {}
}
```

#### Understanding the Constructor Syntax

| Component                 | Purpose                                                            |
| ------------------------- | ------------------------------------------------------------------ |
| `@InjectRepository(User)` | Tells dependency injection system we need the User repository      |
| `private repo`            | Creates and assigns a private property automatically               |
| `Repository<User>`        | Type annotation indicating a repository that handles User entities |

#### Why @InjectRepository is Needed

The dependency injection system uses type annotations to figure out what to inject. However, `Repository<User>` doesn't provide enough information because generics (the `<User>` part) are not preserved at runtime. The `@InjectRepository(User)` decorator explicitly tells NestJS which repository to inject.

#### Creating the Create Method

```typescript
create(email: string, password: string) {
  const user = this.repo.create({ email, password });
  return this.repo.save(user);
}
```

#### Import Sources

| Import             | Source            | Purpose                            |
| ------------------ | ----------------- | ---------------------------------- |
| `Repository`       | `typeorm`         | Type for the repository instance   |
| `InjectRepository` | `@nestjs/typeorm` | Decorator for repository injection |
| `User`             | `./user.entity`   | The entity class                   |

#### Why This Matters

Understanding how to inject repositories into services is fundamental to using TypeORM with NestJS. The `@InjectRepository` decorator bridges the gap between NestJS's dependency injection system and TypeORM's repository pattern.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.2+–+Quick+Breather+and+Review" alt="Lecture 9.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture provides a comprehensive review of the application architecture and explains the difference between the `create` and `save` methods in TypeORM repositories.

#### Application Flow Overview

```
Incoming Request → Validation Pipe → DTO → Controller → Service → Repository → Database
```

| Component           | Responsibility                                          |
| ------------------- | ------------------------------------------------------- |
| **Validation Pipe** | Validates incoming request data                         |
| **DTO**             | Defines the shape and validation rules for request data |
| **Controller**      | Defines routes and extracts data from requests          |
| **Service**         | Contains business logic                                 |
| **Repository**      | Interface to the database                               |
| **Entity**          | Represents a database table structure                   |

#### Create vs Save Methods

The `create` and `save` methods serve different purposes:

```typescript
// Create: Makes an entity instance (NO database interaction)
const user = this.repo.create({ email, password });

// Save: Actually persists the entity to the database
return this.repo.save(user);
```

#### Visual Flow of Create and Save

```
┌─────────────────────────────────────────────────────────────────┐
│                         Application                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   email: "abc@example.com"    ─────►  repo.create()            │
│   password: "abc123"                       │                    │
│                                            ▼                    │
│                                  ┌─────────────────┐            │
│                                  │  User Entity    │            │
│                                  │  Instance       │            │
│                                  │  email: "abc.." │            │
│                                  │  password: "a.."│            │
│                                  └────────┬────────┘            │
│                                           │                     │
│                                           ▼                     │
│                                    repo.save()                  │
│                                           │                     │
└───────────────────────────────────────────┼─────────────────────┘
                                            │
                                            ▼
                                   ┌─────────────────┐
                                   │    Database     │
                                   └─────────────────┘
```

#### Why Use Create Then Save?

The `save` method can accept either:

- A plain object with properties: `repo.save({ email, password })`
- An entity instance: `repo.save(userEntity)`

**Why not just use plain objects?**

Using `repo.create()` first creates an actual entity instance. This is important because entity instances can have **hooks** (lifecycle methods) defined on them that run during certain operations.

#### Entity Hooks Example

```typescript
@Entity()
export class User {
  @AfterInsert()
  logInsert() {
    console.log("Inserted User with id", this.id);
  }

  @AfterUpdate()
  logUpdate() {
    console.log("Updated User with id", this.id);
  }

  @AfterRemove()
  logRemove() {
    console.log("Removed User with id", this.id);
  }
}
```

#### Key Insight

If you call `repo.save({ email, password })` with a plain object instead of an entity instance, **hooks will NOT be executed**. Always use `repo.create()` first if you want hooks to run.

#### Why This Matters

Understanding the distinction between `create` and `save` is crucial for properly leveraging TypeORM's entity lifecycle hooks. These hooks are valuable for logging, validation, and other side effects during database operations.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.3+–+More+on+Create+vs+Save" alt="Lecture 9.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture provides a deeper dive into why entity instances are important and demonstrates the practical implications of using `create` before `save` versus saving plain objects directly.

#### Entity Hooks Behavior

```typescript
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Column()
  password: string;

  @AfterInsert()
  logInsert() {
    console.log("Inserted User with id", this.id);
  }

  @AfterUpdate()
  logUpdate() {
    console.log("Updated User with id", this.id);
  }

  @AfterRemove()
  logRemove() {
    console.log("Removed User with id", this.id);
  }
}
```

#### Comparison: Entity Instance vs Plain Object

| Approach                       | Hooks Execute? | Code                                          |
| ------------------------------ | -------------- | --------------------------------------------- |
| Using `create()` then `save()` | ✅ Yes         | `repo.save(repo.create({ email, password }))` |
| Saving plain object directly   | ❌ No          | `repo.save({ email, password })`              |

#### Why Hooks Are Important

Hooks allow you to:

- **Log operations** for debugging and auditing
- **Transform data** before or after operations
- **Trigger side effects** like sending notifications
- **Validate data** at the entity level

#### Testing Hook Execution

When you create a user using the proper method:

```typescript
// In the service
create(email: string, password: string) {
  const user = this.repo.create({ email, password });
  return this.repo.save(user);
}
```

Console output when creating a user:

```
Inserted User with id 1
```

If you skip `create()` and pass a plain object:

```typescript
// Hooks will NOT run
return this.repo.save({ email, password });
```

No console output appears.

#### Best Practice

Always use the two-step process when you have entity hooks:

```typescript
// Step 1: Create entity instance
const entity = this.repo.create(data);

// Step 2: Save to database
return this.repo.save(entity);
```

#### Why This Matters

Entity hooks are a powerful feature for implementing cross-cutting concerns. Understanding when they execute (and when they don't) prevents subtle bugs and ensures your application behaves consistently.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=700&lines=🎬+Lecture+9.4+–+Required+Update+for+find+and+findOne+Methods" alt="Lecture 9.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture addresses breaking changes introduced in TypeORM 0.3.0 that affect the `find` and `findOne` methods, and provides the updated syntax required for these operations.

#### TypeORM 0.3.0 Breaking Changes

The TypeORM 0.3.0 release introduced changes that:

- Deprecates `findBy` as a separate method
- Requires different syntax for `find` and `findOne` operations

#### Updated findOne Method

**Old syntax (deprecated):**

```typescript
findOne(id: number) {
  return this.repo.findOne(id);
}
```

**New syntax (required):**

```typescript
findOne(id: number) {
  return this.repo.findOneBy({ id });
}
```

#### Updated find Method

**Old syntax (deprecated):**

```typescript
find(email: string) {
  return this.repo.find({ email });
}
```

**New syntax (required):**

```typescript
find(email: string) {
  return this.repo.find({ where: { email } });
}
```

#### Summary of Changes

| Method    | Old Syntax           | New Syntax                      |
| --------- | -------------------- | ------------------------------- |
| `findOne` | `findOne(id)`        | `findOneBy({ id })`             |
| `find`    | `find({ property })` | `find({ where: { property } })` |

#### Complete Service Method Examples

```typescript
// Find one user by ID
findOne(id: number) {
  return this.repo.findOneBy({ id });
}

// Find all users by email
find(email: string) {
  return this.repo.find({ where: { email } });
}
```

#### Why This Matters

Staying up-to-date with TypeORM version changes ensures your code works correctly and follows current best practices. These breaking changes are common in rapidly evolving libraries.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=DC3545&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.5+–+Querying+for+Data" alt="Lecture 9.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture focuses on implementing the remaining service methods (`findOne`, `find`, `update`, `remove`) before connecting them to controller route handlers. This approach helps understand TypeORM repository interactions more efficiently.

#### Service Method Scaffolding

Start by creating method signatures in the service:

```typescript
@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private repo: Repository<User>) {}

  create(email: string, password: string) {
    const user = this.repo.create({ email, password });
    return this.repo.save(user);
  }

  findOne(id: number) {
    // Find user by ID
  }

  find(email: string) {
    // Find users by email
  }

  update() {
    // Update a user
  }

  remove() {
    // Remove a user
  }
}
```

#### Implementing findOne

The `findOne` method retrieves a single user by their ID:

```typescript
findOne(id: number) {
  return this.repo.findOneBy({ id });
}
```

#### Alternative findOne Usage

`findOneBy` can also accept search criteria objects:

```typescript
// Find by ID
this.repo.findOneBy({ id });

// Find by email
this.repo.findOneBy({ email: "test@example.com" });

// Find by multiple criteria
this.repo.findOneBy({ email: "test@example.com", id: 1 });
```

#### Implementing find

The `find` method retrieves all users matching a given email:

```typescript
find(email: string) {
  return this.repo.find({ where: { email } });
}
```

#### Repository Query Methods Summary

| Method                          | Purpose                             | Returns                 |
| ------------------------------- | ----------------------------------- | ----------------------- |
| `findOneBy({ criteria })`       | Find first record matching criteria | Single entity or `null` |
| `find({ where: { criteria } })` | Find all records matching criteria  | Array of entities       |
| `findBy({ criteria })`          | Shorthand for find with where       | Array of entities       |

#### Why This Matters

Building service methods first allows you to focus on TypeORM interactions without the complexity of HTTP request handling. The service layer should encapsulate all database operations, making it reusable across different controllers or communication protocols.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=17A2B8&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.6+–+Updating+Data" alt="Lecture 9.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to implement an `update` method in the service, including how to design flexible function signatures using TypeScript's `Partial` type.

#### Bad Design: Individual Property Arguments

```typescript
// DON'T do this - inflexible and hard to maintain
update(id: number, email: string, password: string) {
  // What if we only want to update email?
  // What do we pass for password?
}
```

**Problems with this approach:**

- What value to pass for properties you don't want to update?
- Argument list grows with each new property
- Hard to read and maintain

#### Good Design: Using Partial<Entity>

```typescript
update(id: number, attrs: Partial<User>) {
  // Can update any combination of properties
}
```

#### Understanding Partial<T>

`Partial<T>` is a TypeScript utility type that makes all properties of `T` optional:

```typescript
// User entity
class User {
  id: number;
  email: string;
  password: string;
}

// Partial<User> is equivalent to:
interface PartialUser {
  id?: number;
  email?: string;
  password?: string;
}
```

#### Implementing the Update Method

```typescript
async update(id: number, attrs: Partial<User>) {
  const user = await this.findOne(id);
  if (!user) {
    throw new NotFoundException('user not found');
  }
  Object.assign(user, attrs);
  return this.repo.save(user);
}
```

#### Update Method Flow

```
1. Fetch user by ID  ─────►  findOne(id)
                                  │
                                  ▼
2. Check if exists   ─────►  if (!user) throw error
                                  │
                                  ▼
3. Apply changes     ─────►  Object.assign(user, attrs)
                                  │
                                  ▼
4. Save to database  ─────►  repo.save(user)
```

#### Why Object.assign?

`Object.assign(target, source)` copies properties from `source` to `target`:

```typescript
const user = { id: 1, email: "old@test.com", password: "secret" };
const attrs = { email: "new@test.com" };

Object.assign(user, attrs);
// user is now: { id: 1, email: 'new@test.com', password: 'secret' }
```

#### Save vs Update Repository Methods

| Method                   | Requires Entity Instance | Hooks Execute | Database Trips            |
| ------------------------ | ------------------------ | ------------- | ------------------------- |
| `save(entity)`           | Yes                      | ✅ Yes        | 1 (if fetched) + 1 (save) |
| `update(criteria, data)` | No                       | ❌ No         | 1                         |

**Why use save instead of update?**

- `save` with an entity instance executes hooks
- `update` skips hooks entirely

#### Why This Matters

Using `Partial<Entity>` provides flexibility for update operations while maintaining type safety. Understanding the difference between `save` and `update` ensures hooks execute when needed.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E83E8C&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.7+–+Removing+Users" alt="Lecture 9.7" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains how to implement the `remove` method in the service, highlighting the important difference between `remove` and `delete` repository methods.

#### Remove vs Delete Methods

Similar to `save` vs `update`, TypeORM provides two ways to delete records:

| Method             | Input           | Hooks Execute | Database Trips     |
| ------------------ | --------------- | ------------- | ------------------ |
| `remove(entity)`   | Entity instance | ✅ Yes        | 2 (fetch + delete) |
| `delete(criteria)` | ID or criteria  | ❌ No         | 1                  |

#### Implementing the Remove Method

```typescript
async remove(id: number) {
  const user = await this.findOne(id);
  if (!user) {
    throw new NotFoundException('user not found');
  }
  return this.repo.remove(user);
}
```

#### Why Use Remove Instead of Delete?

If you have hooks defined on your entity:

```typescript
@Entity()
export class User {
  @AfterRemove()
  logRemove() {
    console.log("Removed User with id", this.id);
  }
}
```

Using `delete`:

```typescript
// Hook will NOT execute
await this.repo.delete(id);
```

Using `remove`:

```typescript
// Hook WILL execute
const user = await this.findOne(id);
await this.repo.remove(user);
```

#### Trade-off Consideration

```
delete(id)                          remove(entity)
    │                                    │
    ▼                                    ▼
┌─────────┐                      ┌─────────────────┐
│ 1 Query │                      │ Query 1: Fetch  │
└─────────┘                      └────────┬────────┘
                                          │
                                          ▼
                                 ┌─────────────────┐
                                 │ Query 2: Delete │
                                 └─────────────────┘

Faster, but no hooks          Slower, but hooks run
```

#### Error Handling Decision

Whether to throw an error when the user doesn't exist is a design decision:

```typescript
async remove(id: number) {
  const user = await this.findOne(id);
  if (!user) {
    // Option 1: Throw error (recommended)
    throw new NotFoundException('user not found');

    // Option 2: Return silently (user already doesn't exist)
    // return;
  }
  return this.repo.remove(user);
}
```

#### Complete Service Implementation

```typescript
@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private repo: Repository<User>) {}

  create(email: string, password: string) {
    const user = this.repo.create({ email, password });
    return this.repo.save(user);
  }

  findOne(id: number) {
    return this.repo.findOneBy({ id });
  }

  find(email: string) {
    return this.repo.find({ where: { email } });
  }

  async update(id: number, attrs: Partial<User>) {
    const user = await this.findOne(id);
    if (!user) {
      throw new NotFoundException("user not found");
    }
    Object.assign(user, attrs);
    return this.repo.save(user);
  }

  async remove(id: number) {
    const user = await this.findOne(id);
    if (!user) {
      throw new NotFoundException("user not found");
    }
    return this.repo.remove(user);
  }
}
```

#### Why This Matters

Choosing between `remove` and `delete` (or `save` and `update`) is an important architectural decision. If you need hooks to run for logging, auditing, or side effects, use the entity-based methods even though they require additional database queries.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=20C997&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.8+–+Finding+and+Filtering+Records" alt="Lecture 9.8" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to wire up the service methods to controller route handlers, starting with `findOne` and `find` operations.

#### Required Imports

```typescript
import { Controller, Get, Param, Query } from "@nestjs/common";
```

#### Implementing Find User by ID

Route: `GET /auth/:id`

```typescript
@Get('/:id')
findUser(@Param('id') id: string) {
  return this.usersService.findOne(parseInt(id));
}
```

**Important:** URL parameters are always strings! You must parse them to numbers when your service expects a numeric ID.

#### Implementing Find Users by Email

Route: `GET /auth?email=test@example.com`

```typescript
@Get()
findAllUsers(@Query('email') email: string) {
  return this.usersService.find(email);
}
```

#### Param vs Query Decorators

| Decorator         | Extracts From | Example URL                 | Usage              |
| ----------------- | ------------- | --------------------------- | ------------------ |
| `@Param('id')`    | URL path      | `/auth/5`                   | Get resource by ID |
| `@Query('email')` | Query string  | `/auth?email=test@test.com` | Filter/search      |

#### Controller Implementation So Far

```typescript
@Controller("auth")
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Post("/signup")
  createUser(@Body() body: CreateUserDto) {
    return this.usersService.create(body.email, body.password);
  }

  @Get("/:id")
  findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }

  @Get()
  findAllUsers(@Query("email") email: string) {
    return this.usersService.find(email);
  }
}
```

#### Testing the Routes

**Find by ID:**

```http
GET http://localhost:3000/auth/1

Response:
{
  "id": 1,
  "email": "test@example.com",
  "password": "password123"
}
```

**Find by Email:**

```http
GET http://localhost:3000/auth?email=test@example.com

Response:
[
  {
    "id": 1,
    "email": "test@example.com",
    "password": "password123"
  }
]
```

#### Security Note

The responses currently include the password field. This is a security concern that will be addressed later using serialization/interceptors to filter out sensitive data.

#### Why This Matters

Connecting services to controllers completes the request flow from HTTP to database. Understanding how to extract different types of request data (params, query strings, body) is essential for building REST APIs.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FD7E14&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.9+–+Removing+Records" alt="Lecture 9.9" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements the delete route handler, demonstrating how to handle DELETE requests and discussing error scenarios.

#### Required Imports

```typescript
import {
  Controller,
  Get,
  Post,
  Delete,
  Param,
  Query,
  Body,
} from "@nestjs/common";
```

#### Implementing Remove User

Route: `DELETE /auth/:id`

```typescript
@Delete('/:id')
removeUser(@Param('id') id: string) {
  return this.usersService.remove(parseInt(id));
}
```

#### Testing the Delete Route

**Delete a user:**

```http
DELETE http://localhost:3000/auth/1

Response:
{
  "email": "test@example.com",
  "password": "password123"
}
```

**Note:** The response shows the deleted user data (without the ID, as it's been removed).

#### Verifying Deletion

After deletion, querying for users with that email should return an empty array:

```http
GET http://localhost:3000/auth?email=test@example.com

Response:
[]
```

#### Error Handling Consideration

If you try to delete a user that doesn't exist:

```http
DELETE http://localhost:3000/auth/999

Response:
{
  "statusCode": 500,
  "message": "Internal server error"
}
```

This error occurs because our service throws a `NotFoundException`, but we haven't set up proper error handling yet. This will be addressed in upcoming lectures.

#### Controller Update

```typescript
@Controller("auth")
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Post("/signup")
  createUser(@Body() body: CreateUserDto) {
    return this.usersService.create(body.email, body.password);
  }

  @Get("/:id")
  findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }

  @Get()
  findAllUsers(@Query("email") email: string) {
    return this.usersService.find(email);
  }

  @Delete("/:id")
  removeUser(@Param("id") id: string) {
    return this.usersService.remove(parseInt(id));
  }
}
```

#### Why This Matters

Implementing DELETE routes follows the same pattern as GET routes with URL parameters. Understanding error propagation from services to controllers is important for building robust APIs.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6610F2&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.10+–+Updating+Records" alt="Lecture 9.10" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements the update (PATCH) route handler, including creating a new DTO for update validation with optional fields.

#### Creating the Update User DTO

Unlike `CreateUserDto` where both fields are required, `UpdateUserDto` needs optional fields:

```typescript
// src/users/dtos/update-user.dto.ts
import { IsEmail, IsString, IsOptional } from "class-validator";

export class UpdateUserDto {
  @IsEmail()
  @IsOptional()
  email: string;

  @IsString()
  @IsOptional()
  password: string;
}
```

#### Understanding @IsOptional

The `@IsOptional()` decorator from `class-validator`:

- Makes the property optional in validation
- If the property is provided, other validators still apply
- If the property is not provided, validation passes

#### Validation Behavior

| Request Body                                          | Valid? | Reason                         |
| ----------------------------------------------------- | ------ | ------------------------------ |
| `{ "email": "test@test.com" }`                        | ✅     | Valid email, password optional |
| `{ "password": "newpass" }`                           | ✅     | Valid string, email optional   |
| `{ "email": "test@test.com", "password": "newpass" }` | ✅     | Both valid                     |
| `{ }`                                                 | ✅     | Both optional                  |
| `{ "email": "not-an-email" }`                         | ❌     | Invalid email format           |

#### Implementing Update User Route

Route: `PATCH /auth/:id`

```typescript
@Patch('/:id')
updateUser(@Param('id') id: string, @Body() body: UpdateUserDto) {
  return this.usersService.update(parseInt(id), body);
}
```

#### Required Imports

```typescript
import {
  Controller,
  Get,
  Post,
  Patch,
  Delete,
  Param,
  Query,
  Body,
} from "@nestjs/common";
import { CreateUserDto } from "./dtos/create-user.dto";
import { UpdateUserDto } from "./dtos/update-user.dto";
```

#### Complete Controller Implementation

```typescript
@Controller("auth")
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Post("/signup")
  createUser(@Body() body: CreateUserDto) {
    return this.usersService.create(body.email, body.password);
  }

  @Get("/:id")
  findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }

  @Get()
  findAllUsers(@Query("email") email: string) {
    return this.usersService.find(email);
  }

  @Delete("/:id")
  removeUser(@Param("id") id: string) {
    return this.usersService.remove(parseInt(id));
  }

  @Patch("/:id")
  updateUser(@Param("id") id: string, @Body() body: UpdateUserDto) {
    return this.usersService.update(parseInt(id), body);
  }
}
```

#### Testing the Update Route

**Update email only:**

```http
PATCH http://localhost:3000/auth/1
Content-Type: application/json

{
  "email": "newemail@example.com"
}

Response:
{
  "id": 1,
  "email": "newemail@example.com",
  "password": "originalpassword"
}
```

**Update both fields:**

```http
PATCH http://localhost:3000/auth/1
Content-Type: application/json

{
  "email": "newemail@example.com",
  "password": "newpassword"
}
```

#### Why This Matters

The `@IsOptional()` decorator is essential for PATCH operations where clients should be able to update individual fields without providing all data. This follows REST conventions where PATCH performs partial updates.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E83E8C&center=true&vCenter=true&width=600&lines=🎬+Lecture+9.11+–+A+Few+Notes+on+Exceptions" alt="Lecture 9.11" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture discusses an important architectural consideration about throwing HTTP-specific exceptions from services and its implications for reusability across different communication protocols.

#### Current Implementation Issue

In our service, we're throwing `NotFoundException` (an HTTP-specific exception):

```typescript
async update(id: number, attrs: Partial<User>) {
  const user = await this.findOne(id);
  if (!user) {
    throw new NotFoundException('user not found');  // HTTP-specific!
  }
  // ...
}

async remove(id: number) {
  const user = await this.findOne(id);
  if (!user) {
    throw new NotFoundException('user not found');  // HTTP-specific!
  }
  // ...
}
```

#### The Problem: Service Reusability

NestJS supports multiple communication protocols:

```
                         ┌─────────────────────────┐
                         │     Users Service       │
                         │ (throws NotFoundException)│
                         └───────────┬─────────────┘
                                     │
              ┌──────────────────────┼──────────────────────┐
              │                      │                      │
              ▼                      ▼                      ▼
    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ HTTP Controller │    │ WebSocket       │    │ gRPC Controller │
    │ (works! ✅)     │    │ Controller (❌) │    │ (❌)            │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
```

`NotFoundException` is specifically for HTTP 404 responses. If the same service is used by:

- **WebSocket controller** - Cannot properly handle HTTP exceptions
- **gRPC controller** - Has its own error handling mechanism
- **GraphQL resolver** - Uses different error types

#### NestJS Built-in HTTP Exceptions

| Exception                      | HTTP Status Code |
| ------------------------------ | ---------------- |
| `BadRequestException`          | 400              |
| `UnauthorizedException`        | 401              |
| `ForbiddenException`           | 403              |
| `NotFoundException`            | 404              |
| `ConflictException`            | 409              |
| `InternalServerErrorException` | 500              |

All of these are HTTP-specific!

#### Solutions

**Option 1: Accept the Limitation (Current Approach)**
If you know your service will only be used with HTTP controllers, throwing HTTP exceptions is acceptable:

```typescript
throw new NotFoundException("user not found");
```

**Option 2: Throw Generic Errors + Controller Handling**
Throw plain errors from services and handle them in controllers:

```typescript
// Service
async remove(id: number) {
  const user = await this.findOne(id);
  if (!user) {
    throw new Error('user not found');  // Generic error
  }
  return this.repo.remove(user);
}

// Controller
@Delete('/:id')
async removeUser(@Param('id') id: string) {
  try {
    return await this.usersService.remove(parseInt(id));
  } catch (err) {
    throw new NotFoundException(err.message);  // Convert to HTTP
  }
}
```

**Option 3: Custom Exception Filters**
Create exception filters that handle errors differently based on the communication protocol.

#### For This Course

We'll use Option 1 (throwing HTTP exceptions from services) because:

- We're only using HTTP controllers
- It's simpler and more straightforward
- It's a common pattern in many NestJS applications

#### Import for NotFoundException

```typescript
import { Injectable, NotFoundException } from "@nestjs/common";
```

#### Updated Service

```typescript
import { Injectable, NotFoundException } from "@nestjs/common";
import { Repository } from "typeorm";
import { InjectRepository } from "@nestjs/typeorm";
import { User } from "./user.entity";

@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private repo: Repository<User>) {}

  create(email: string, password: string) {
    const user = this.repo.create({ email, password });
    return this.repo.save(user);
  }

  findOne(id: number) {
    return this.repo.findOneBy({ id });
  }

  find(email: string) {
    return this.repo.find({ where: { email } });
  }

  async update(id: number, attrs: Partial<User>) {
    const user = await this.findOne(id);
    if (!user) {
      throw new NotFoundException("user not found");
    }
    Object.assign(user, attrs);
    return this.repo.save(user);
  }

  async remove(id: number) {
    const user = await this.findOne(id);
    if (!user) {
      throw new NotFoundException("user not found");
    }
    return this.repo.remove(user);
  }
}
```

#### Why This Matters

Understanding the implications of exception handling in services is crucial for building reusable, maintainable code. While HTTP exceptions work well for HTTP-only applications, being aware of this limitation helps you make informed architectural decisions for more complex applications.

<br>

---

## Section 9 Summary

This section covered the complete CRUD operations for user data:

| Operation | Route               | Service Method | Key Concepts                           |
| --------- | ------------------- | -------------- | -------------------------------------- |
| Create    | `POST /auth/signup` | `create()`     | `repo.create()` + `repo.save()`, hooks |
| Read One  | `GET /auth/:id`     | `findOne()`    | `findOneBy()`, URL params              |
| Read Many | `GET /auth?email=`  | `find()`       | `find({ where })`, query strings       |
| Update    | `PATCH /auth/:id`   | `update()`     | `Partial<Entity>`, `@IsOptional()`     |
| Delete    | `DELETE /auth/:id`  | `remove()`     | `remove()` vs `delete()`, hooks        |

#### Key Takeaways

1. **Create vs Save**: Use `create()` to make entity instances, `save()` to persist. This ensures hooks execute.

2. **Remove vs Delete**: Use `remove()` with entities for hooks, `delete()` with IDs for performance.

3. **TypeORM 0.3.0 Changes**: Use `findOneBy()` and `find({ where })` syntax.

4. **Partial<Entity>**: Provides type-safe flexible update operations.

5. **@IsOptional()**: Makes DTO properties optional for PATCH operations.

6. **Exception Handling**: HTTP exceptions in services work but limit reusability across protocols.

## Section 10: Custom Data Serialization

This section covers how to control and customize the data sent back in HTTP responses. You'll learn how to hide sensitive information like passwords, create custom interceptors, and build reusable serialization solutions that can format different responses for different route handlers.

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=650&lines=🎬+Lecture+10.1+–+Excluding+Response+Properties" alt="Lecture 10.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture identifies a security concern in our API responses: user passwords are being returned in HTTP responses. We'll explore the NestJS recommended solution using the `@Exclude()` decorator and class serializer interceptor.

#### The Problem: Exposing Sensitive Data

When fetching a user, the response includes the password:

```json
{
  "id": 1,
  "email": "test@test.com",
  "password": "abc123" // ❌ Should NOT be exposed!
}
```

Even after implementing password encryption, we should never send passwords in responses.

#### Understanding the Current Flow

```
Request: GET /auth/2
         ↓
    UsersController
         ↓
    UsersService
         ↓
    UsersRepository (TypeORM)
         ↓
    Returns User Entity Instance
         ↓
    NestJS converts to JSON (includes ALL properties)
         ↓
Response: { id, email, password }  ❌
```

#### The Nest-Recommended Solution

**Step 1: Add @Exclude() to the Entity**

```typescript
import { Exclude } from "class-transformer";
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Column()
  @Exclude() // Don't include in responses
  password: string;
}
```

**Step 2: Add ClassSerializerInterceptor to Controller**

```typescript
import {
  Controller,
  Get,
  UseInterceptors,
  ClassSerializerInterceptor,
} from "@nestjs/common";

@Controller("auth")
export class UsersController {
  @UseInterceptors(ClassSerializerInterceptor)
  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }
}
```

#### What is an Interceptor?

| Aspect     | Description                                          |
| ---------- | ---------------------------------------------------- |
| Purpose    | Intercept incoming requests or outgoing responses    |
| Similar to | Middleware in other frameworks                       |
| Use cases  | Transform data, logging, caching, exception mapping  |
| Scope      | Can apply to single handler, controller, or globally |

#### How ClassSerializerInterceptor Works

1. **Intercepts** the outgoing response
2. **Reads** the `@Exclude()` decorators on the entity
3. **Removes** excluded properties
4. **Returns** the sanitized JSON

#### Testing the Solution

**Request:**

```http
GET http://localhost:3000/auth/2
```

**Response (After Fix):**

```json
{
  "id": 2,
  "email": "test@test.com"
}
```

✅ Password is no longer included!

#### Required Package

The `class-transformer` package is already installed (companion to `class-validator`):

```bash
npm install class-transformer
```

#### Why This Matters

- **Security**: Never expose sensitive data like passwords
- **Best Practice**: Control what data leaves your API
- **Compliance**: Many regulations require data minimization

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=600&lines=🎬+Lecture+10.2+–+Solution+to+Serialization" alt="Lecture 10.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains the limitations of the Nest-recommended approach and introduces a better, more flexible solution using custom interceptors and DTOs for outgoing responses.

#### The Problem with @Exclude() on Entities

**Scenario: Multiple Route Handlers Need Different Data**

Imagine we add more user properties and have different routes:

```typescript
// User Entity with more properties
@Entity()
export class User {
  id: number;
  email: string;
  password: string;
  age: number; // New property
  name: string; // New property
}
```

**Admin Route** - Should return ALL user info:

```
GET /admin/auth/2  →  { id, email, age, name }
```

**Public Route** - Should return LIMITED info:

```
GET /auth/2  →  { id, email }
```

#### Why the Entity-Based Approach Fails

| Issue                   | Explanation                                           |
| ----------------------- | ----------------------------------------------------- |
| **Single Format**       | Entity can only define ONE set of serialization rules |
| **Not Flexible**        | Can't show different properties for different routes  |
| **View Logic in Model** | Entity shouldn't know about presentation concerns     |
| **Tightly Coupled**     | Changes affect ALL routes that return users           |

#### The Better Solution: Custom Interceptor + DTOs

Instead of attaching serialization rules to the entity, we'll:

1. **Create a Custom Interceptor** - Handles serialization logic
2. **Create Response DTOs** - Define what to expose per route
3. **Apply Per Route Handler** - Different DTOs for different routes

#### Architecture Diagram

```
                    ┌─────────────────────┐
                    │   User Entity       │
                    │   (No View Logic)   │
                    └──────────┬──────────┘
                               │
           ┌───────────────────┼───────────────────┐
           │                   │                   │
           ▼                   ▼                   ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│  Admin Route     │ │  Public Route    │ │  Profile Route   │
│  Handler         │ │  Handler         │ │  Handler         │
└────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘
         │                    │                    │
         ▼                    ▼                    ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│  AdminUserDto    │ │  UserDto         │ │  ProfileDto      │
│  id, email,      │ │  id, email       │ │  id, email,      │
│  age, name       │ │  (limited)       │ │  name            │
└──────────────────┘ └──────────────────┘ └──────────────────┘
         │                    │                    │
         └────────────────────┼────────────────────┘
                              ▼
                    ┌─────────────────────┐
                    │ Custom Interceptor  │
                    │ (Serializes based   │
                    │  on DTO rules)      │
                    └─────────────────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │   JSON Response     │
                    └─────────────────────┘
```

#### Benefits of Custom Solution

| Benefit         | Description                            |
| --------------- | -------------------------------------- |
| **Flexibility** | Different formats for different routes |
| **Separation**  | Entity doesn't know about presentation |
| **Reusability** | DTOs can be reused across controllers  |
| **Scalability** | Easy to add new response formats       |
| **Testability** | DTOs are simple classes to test        |

#### What is a Response DTO?

Previously, we used DTOs for **incoming** request validation. Now we'll also use DTOs for **outgoing** response formatting:

| DTO Type     | Purpose                | Example         |
| ------------ | ---------------------- | --------------- |
| Request DTO  | Validate incoming data | `CreateUserDto` |
| Response DTO | Format outgoing data   | `UserDto`       |

#### First Step: Clean Up Entity

Remove the `@Exclude()` decorator from the entity - we're moving this logic elsewhere:

```typescript
// user.entity.ts - Clean, no view logic
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Column()
  password: string; // No @Exclude() here anymore
}
```

#### Why This Matters

- **Clean Architecture**: Entities handle data, DTOs handle presentation
- **Multiple Views**: Same data, different representations
- **Future-Proof**: Easy to add new response formats
- **Real-World Ready**: This pattern scales with application complexity

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=600&lines=🎬+Lecture+10.3+–+How+to+Build+Interceptors" alt="Lecture 10.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture teaches the fundamentals of creating custom interceptors in NestJS. We'll learn the interceptor structure, lifecycle, and how to apply them at different levels.

#### What are Interceptors?

Interceptors are classes that can:

- **Intercept incoming requests** before they reach route handlers
- **Intercept outgoing responses** before they're sent to clients
- **Transform data** in either direction
- **Add extra logic** like logging, caching, or exception handling

#### Interceptor Application Levels

| Level          | Scope                     | Use Case                           |
| -------------- | ------------------------- | ---------------------------------- |
| **Handler**    | Single route method       | Specific response formatting       |
| **Controller** | All routes in controller  | Consistent formatting for resource |
| **Global**     | All routes in application | Logging, authentication            |

#### Interceptor Structure

```typescript
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";

export class CustomInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    // Code here runs BEFORE the request handler
    console.log("Before handler execution");

    return next.handle().pipe(
      map((data) => {
        // Code here runs AFTER the request handler
        // 'data' is the response from the handler
        console.log("After handler, before response sent");
        return data;
      })
    );
  }
}
```

#### Understanding the intercept() Method

| Parameter | Type               | Purpose                                             |
| --------- | ------------------ | --------------------------------------------------- |
| `context` | `ExecutionContext` | Wrapper around incoming request details             |
| `next`    | `CallHandler`      | Reference to the route handler (as RxJS Observable) |

#### The Request/Response Flow

```
Incoming Request
       │
       ▼
┌──────────────────┐
│   Interceptor    │◄── Code BEFORE next.handle()
│   (Before)       │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Route Handler   │◄── Your controller method
│  (Controller)    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   Interceptor    │◄── Code INSIDE map()
│   (After)        │
└────────┬─────────┘
         │
         ▼
   JSON Response
```

#### Creating the Serialize Interceptor

**File Structure:**

```
src/
├── interceptors/
│   └── serialize.interceptor.ts  ← Create this
├── users/
│   ├── users.controller.ts
│   └── dtos/
│       └── user.dto.ts
```

**Basic Interceptor Setup:**

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";

export class SerializeInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    // Runs before the handler
    console.log("Running before the handler", context);

    return next.handle().pipe(
      map((data: any) => {
        // Runs before response is sent out
        console.log("Running before response sent out", data);
        return data;
      })
    );
  }
}
```

#### Using implements NestInterceptor

The `implements` keyword is optional but helpful:

```typescript
// With implements - TypeScript ensures correct structure
export class SerializeInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    // TypeScript will error if method signature is wrong
  }
}
```

| Keyword      | Purpose                                        | Required?         |
| ------------ | ---------------------------------------------- | ----------------- |
| `implements` | Tells TypeScript to check we satisfy interface | Optional          |
| `extends`    | Inherit from parent class                      | Different purpose |

#### Applying the Interceptor

```typescript
// In controller
import { UseInterceptors } from "@nestjs/common";
import { SerializeInterceptor } from "../interceptors/serialize.interceptor";

@Controller("auth")
export class UsersController {
  @UseInterceptors(SerializeInterceptor)
  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }
}
```

#### Why This Matters

- **Reusability**: One interceptor for all serialization needs
- **Centralized Logic**: Keep transformation logic in one place
- **Testability**: Interceptors can be unit tested independently
- **Flexibility**: Apply different interceptors to different routes

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=650&lines=🎬+Lecture+10.4+–+Serialization+in+the+Interceptor" alt="Lecture 10.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements the actual serialization logic inside our custom interceptor. We'll create a User DTO with `@Expose()` decorators and use `plainToClass` for transformation.

#### Understanding the Data Flow

```
User Entity Instance
        │
        ▼
  ┌─────────────────────┐
  │  SerializeInterceptor│
  │  ┌───────────────┐  │
  │  │ plainToClass  │  │
  │  │ (Entity → DTO)│  │
  │  └───────────────┘  │
  └──────────┬──────────┘
             │
             ▼
    User DTO Instance
    (Only @Expose properties)
             │
             ▼
    NestJS converts to JSON
             │
             ▼
    { id, email }  ✅
```

#### Creating the User DTO

**File: `src/users/dtos/user.dto.ts`**

```typescript
import { Expose } from "class-transformer";

export class UserDto {
  @Expose()
  id: number;

  @Expose()
  email: string;

  // Note: password is NOT listed here
  // It won't be included in the response
}
```

#### @Expose vs @Exclude

| Decorator    | Behavior                         | Use Case           |
| ------------ | -------------------------------- | ------------------ |
| `@Expose()`  | Include this property in output  | Whitelist approach |
| `@Exclude()` | Remove this property from output | Blacklist approach |

**We use `@Expose()` because:**

- Explicitly declare what to show (safer)
- New properties are hidden by default
- More secure approach

#### Implementing Serialization Logic

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";
import { UserDto } from "../users/dtos/user.dto";

export class SerializeInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        // Convert User Entity → UserDto instance
        return plainToClass(UserDto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Understanding plainToClass

```typescript
plainToClass(UserDto, data, { excludeExtraneousValues: true });
```

| Parameter | Value     | Purpose                           |
| --------- | --------- | --------------------------------- |
| First     | `UserDto` | The class to transform into       |
| Second    | `data`    | The source data (entity instance) |
| Third     | Options   | Configuration object              |

#### The excludeExtraneousValues Option

**Critical option!** This makes `@Expose()` work correctly:

| Value             | Behavior                                 |
| ----------------- | ---------------------------------------- |
| `true`            | Only include properties with `@Expose()` |
| `false` (default) | Include all properties                   |

```typescript
// Without excludeExtraneousValues: true
// ALL properties would be copied, defeating the purpose!

// With excludeExtraneousValues: true
// ONLY @Expose() properties are included ✅
```

#### Complete Interceptor Code

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";
import { UserDto } from "../users/dtos/user.dto";

export class SerializeInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(UserDto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Testing the Serialization

**Request:**

```http
GET http://localhost:3000/auth/1
```

**Response:**

```json
{
  "id": 1,
  "email": "test@test.com"
}
```

✅ Password is excluded because it wasn't marked with `@Expose()`!

#### Why This Matters

- **Security by Default**: Unlisted properties are automatically hidden
- **Explicit Control**: You declare exactly what to expose
- **Transformation**: Entity → DTO conversion happens automatically
- **Clean Responses**: Only necessary data is sent to clients

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=650&lines=🎬+Lecture+10.5+–+Customizing+the+Interceptor's+DTO" alt="Lecture 10.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture makes our interceptor reusable by allowing different DTOs to be passed in. This enables different route handlers to use different serialization rules.

#### The Problem: Hardcoded DTO

Current implementation only works with `UserDto`:

```typescript
// ❌ Hardcoded - can only serialize users
export class SerializeInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(UserDto, data, {
          // ← Hardcoded!
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

What if we need to serialize:

- Reports with `ReportDto`?
- Comments with `CommentDto`?
- Admin users with `AdminUserDto`?

#### The Solution: Constructor Injection

Pass the DTO class when creating the interceptor:

```typescript
// ✅ Flexible - accepts any DTO class
export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: any) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          // ← Dynamic!
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Updated Interceptor Code

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";

export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: any) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Using the Customized Interceptor

```typescript
// users.controller.ts
import { UseInterceptors } from "@nestjs/common";
import { SerializeInterceptor } from "../interceptors/serialize.interceptor";
import { UserDto } from "./dtos/user.dto";

@Controller("auth")
export class UsersController {
  // Pass UserDto to the interceptor
  @UseInterceptors(new SerializeInterceptor(UserDto))
  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }
}
```

#### Different DTOs for Different Routes

```typescript
@Controller("auth")
export class UsersController {
  // Public route - limited info
  @UseInterceptors(new SerializeInterceptor(UserDto))
  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }

  // Admin route - full info
  @UseInterceptors(new SerializeInterceptor(AdminUserDto))
  @Get("/admin/:id")
  async findUserAdmin(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }
}
```

#### Example DTOs

**UserDto (Limited):**

```typescript
export class UserDto {
  @Expose()
  id: number;

  @Expose()
  email: string;
}
```

**AdminUserDto (Full):**

```typescript
export class AdminUserDto {
  @Expose()
  id: number;

  @Expose()
  email: string;

  @Expose()
  age: number;

  @Expose()
  name: string;

  @Expose()
  createdAt: Date;
}
```

#### The Remaining Problem

The current syntax is verbose:

```typescript
@UseInterceptors(new SerializeInterceptor(UserDto))
```

This requires:

- Importing `UseInterceptors`
- Importing `SerializeInterceptor`
- Importing the DTO
- Long decorator line

**Next lecture**: We'll create a custom decorator to simplify this!

#### Why This Matters

- **Reusability**: One interceptor for all serialization needs
- **Flexibility**: Different views for different use cases
- **DRY Principle**: Don't repeat serialization logic
- **Scalability**: Easy to add new DTOs as needed

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=DC3545&center=true&vCenter=true&width=700&lines=🎬+Lecture+10.6+–+Wrapping+the+Interceptor+in+a+Decorator" alt="Lecture 10.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture creates a custom decorator to simplify how we apply serialization. Instead of verbose interceptor syntax, we'll use a clean `@Serialize(UserDto)` decorator.

#### The Problem: Verbose Syntax

Current approach requires a long line:

```typescript
// ❌ Too verbose!
@UseInterceptors(new SerializeInterceptor(UserDto))
@Get('/:id')
async findUser(@Param('id') id: string) { ... }
```

Requires importing:

- `UseInterceptors`
- `SerializeInterceptor`
- The DTO class

#### The Solution: Custom Decorator

**Goal:**

```typescript
// ✅ Clean and simple!
@Serialize(UserDto)
@Get('/:id')
async findUser(@Param('id') id: string) { ... }
```

#### What is a Custom Decorator?

Decorators in TypeScript are just **functions**:

```typescript
// A decorator is just a function!
export function Serialize(dto: any) {
  return UseInterceptors(new SerializeInterceptor(dto));
}
```

#### Complete Interceptor File with Decorator

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";

// Custom decorator function
export function Serialize(dto: any) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

// The interceptor class
export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: any) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Using the Custom Decorator

```typescript
// users.controller.ts
import { Serialize } from "../interceptors/serialize.interceptor";
import { UserDto } from "./dtos/user.dto";

@Controller("auth")
export class UsersController {
  @Serialize(UserDto) // ← Clean and simple!
  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }
}
```

#### Before vs After Comparison

| Aspect             | Before                                                | After                   |
| ------------------ | ----------------------------------------------------- | ----------------------- |
| **Decorator Line** | `@UseInterceptors(new SerializeInterceptor(UserDto))` | `@Serialize(UserDto)`   |
| **Imports Needed** | 3 (UseInterceptors, Interceptor, DTO)                 | 2 (Serialize, DTO)      |
| **Readability**    | Verbose, hard to scan                                 | Clean, self-documenting |
| **Characters**     | ~55                                                   | ~20                     |

#### Multiple Routes, Different DTOs

```typescript
@Controller('auth')
export class UsersController {
  @Serialize(UserDto)
  @Get('/:id')
  async findUser(@Param('id') id: string) { ... }

  @Serialize(AdminUserDto)
  @Get('/admin/:id')
  async findUserAdmin(@Param('id') id: string) { ... }

  @Serialize(ProfileDto)
  @Get('/profile/:id')
  async getProfile(@Param('id') id: string) { ... }
}
```

#### How the Decorator Works

```
@Serialize(UserDto)
        │
        ▼
function Serialize(dto) {
  return UseInterceptors(          ← Returns another decorator
    new SerializeInterceptor(dto)  ← Creates interceptor with DTO
  );
}
        │
        ▼
Interceptor applied to route handler
```

#### Why This Matters

- **Clean Code**: Readable, self-documenting decorators
- **Less Boilerplate**: Fewer imports and shorter lines
- **Reusability**: Easy to apply across many routes
- **Consistency**: Team members use the same pattern
- **Maintainability**: Changes in one place affect all usages

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=17A2B8&center=true&vCenter=true&width=650&lines=🎬+Lecture+10.7+–+Controller-Wide+Serialization" alt="Lecture 10.7" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture demonstrates how to apply the `@Serialize()` decorator to an entire controller instead of individual route handlers, and when to choose each approach.

#### Two Options for Applying @Serialize

**Option 1: Per Route Handler**

```typescript
@Controller('auth')
export class UsersController {
  @Serialize(UserDto)
  @Get('/:id')
  async findUser() { ... }

  @Serialize(UserDto)
  @Get()
  async findAllUsers() { ... }

  @Serialize(UserDto)
  @Patch('/:id')
  async updateUser() { ... }
}
```

**Option 2: Controller Level**

```typescript
@Serialize(UserDto)  // ← Applied to ALL routes
@Controller('auth')
export class UsersController {
  @Get('/:id')
  async findUser() { ... }

  @Get()
  async findAllUsers() { ... }

  @Patch('/:id')
  async updateUser() { ... }
}
```

#### When to Use Each Approach

| Approach             | Use When                                |
| -------------------- | --------------------------------------- |
| **Per Handler**      | Different routes need different DTOs    |
| **Controller Level** | All routes return the same type of data |

#### Example: Controller-Level Application

```typescript
// All routes in this controller return User data
// So we apply serialization once at controller level

@Serialize(UserDto)
@Controller("auth")
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Get("/:id")
  async findUser(@Param("id") id: string) {
    return this.usersService.findOne(parseInt(id));
  }

  @Get()
  async findAllUsers(@Query("email") email: string) {
    return this.usersService.find(email);
  }

  @Patch("/:id")
  async updateUser(@Param("id") id: string, @Body() body: UpdateUserDto) {
    return this.usersService.update(parseInt(id), body);
  }

  @Delete("/:id")
  async removeUser(@Param("id") id: string) {
    return this.usersService.remove(parseInt(id));
  }
}
```

#### Testing All Routes

**GET /auth/1**

```json
{ "id": 1, "email": "test@test.com" } // ✅ No password
```

**GET /auth?email=test@test.com**

```json
[{ "id": 1, "email": "test@test.com" }] // ✅ No password
```

**PATCH /auth/1**

```json
{ "id": 1, "email": "updated@test.com" } // ✅ No password
```

#### Mixed Approach Example

If you need different serialization for specific routes:

```typescript
@Serialize(UserDto)  // Default for most routes
@Controller('auth')
export class UsersController {
  @Get('/:id')
  async findUser() { ... }  // Uses UserDto

  @Get()
  async findAllUsers() { ... }  // Uses UserDto

  @Serialize(AdminUserDto)  // Override for this route
  @Get('/admin/:id')
  async findUserAdmin() { ... }  // Uses AdminUserDto
}
```

#### Decorator Precedence

When both controller and handler have decorators:

```
Controller: @Serialize(UserDto)
Handler:    @Serialize(AdminUserDto)

Result: Handler decorator takes precedence → AdminUserDto
```

#### Best Practices

| Scenario                       | Recommendation                       |
| ------------------------------ | ------------------------------------ |
| Single resource controller     | Apply at controller level            |
| Mixed response types           | Apply per handler                    |
| Override needed for few routes | Controller level + handler overrides |
| Different DTOs per route       | Apply per handler                    |

#### Clean Up Tips

After applying serialization, clean up unused imports:

```typescript
// Remove if no longer needed:
// - ClassSerializerInterceptor
// - Exclude decorator imports
// - Old console.log statements
```

#### Why This Matters

- **DRY Code**: Don't repeat the same decorator
- **Maintainability**: Single place to change serialization
- **Flexibility**: Can still override per-handler when needed
- **Consistency**: All routes behave the same way

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=700&lines=🎬+Lecture+10.8+–+A+Bit+of+Type+Safety+Around+Serialize" alt="Lecture 10.8" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture adds TypeScript type safety to our `@Serialize()` decorator to catch errors at compile time rather than runtime.

#### The Problem: any Type Everywhere

Current implementation uses `any` types:

```typescript
// ❌ No type safety
export function Serialize(dto: any) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: any) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    // ...
  }
}
```

**Why is this bad?**

```typescript
// These would NOT cause TypeScript errors:
@Serialize("hello")      // ❌ String passed
@Serialize(123)          // ❌ Number passed
@Serialize({ foo: 1 })   // ❌ Plain object passed
```

#### The Challenge with Decorators

TypeScript's support for decorators is limited:

- Can't easily relate decorator argument to return type
- Can't validate that DTO properties match entity properties
- Decorator metadata is complex to work with

**Realistic Goal:** At minimum, ensure a **class** is passed (not a string, number, etc.)

#### Solution: ClassConstructor Interface

Create an interface that represents "any class":

```typescript
// An interface representing any class constructor
interface ClassConstructor {
  new (...args: any[]): {};
}
```

**Breaking this down:**

| Part               | Meaning                             |
| ------------------ | ----------------------------------- |
| `new`              | Must be callable with `new` keyword |
| `(...args: any[])` | Can accept any arguments            |
| `{}`               | Returns an object                   |

#### Updated Interceptor with Type Safety

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";

// Interface for any class
interface ClassConstructor {
  new (...args: any[]): {};
}

// Custom decorator with type safety
export function Serialize(dto: ClassConstructor) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

// Interceptor class
export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: ClassConstructor) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Now TypeScript Catches Errors

```typescript
// ✅ Valid - UserDto is a class
@Serialize(UserDto)

// ❌ TypeScript Error - string is not a class
@Serialize("hello")

// ❌ TypeScript Error - number is not a class
@Serialize(123)

// ❌ TypeScript Error - plain object is not a class
@Serialize({ id: 1 })
```

#### What We Can and Can't Validate

| Validation                    | Possible?  | Notes                       |
| ----------------------------- | ---------- | --------------------------- |
| Must be a class               | ✅ Yes     | ClassConstructor interface  |
| Class has specific properties | ⚠️ Limited | Would need generics         |
| DTO matches entity            | ❌ No      | Too complex with decorators |
| Return type matches DTO       | ❌ No      | TypeScript limitation       |

#### Complete Final Code

```typescript
// src/interceptors/serialize.interceptor.ts
import {
  UseInterceptors,
  NestInterceptor,
  ExecutionContext,
  CallHandler,
} from "@nestjs/common";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";
import { plainToClass } from "class-transformer";

interface ClassConstructor {
  new (...args: any[]): {};
}

export function Serialize(dto: ClassConstructor) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: ClassConstructor) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

#### Why This Matters

- **Catch Errors Early**: TypeScript errors at compile time
- **Better IDE Support**: Autocomplete knows to expect a class
- **Documentation**: Interface serves as documentation
- **Team Safety**: Prevents accidental misuse

---

## Section 10 Summary

### Key Concepts Learned

1. **The Problem**: Entity instances expose all properties (including sensitive data)
2. **Nest's Solution**: `@Exclude()` decorator - limited flexibility
3. **Better Solution**: Custom interceptor + Response DTOs
4. **Custom Decorator**: `@Serialize()` for clean syntax
5. **Type Safety**: `ClassConstructor` interface validates input

### Files Created/Modified

| File                                        | Purpose                          |
| ------------------------------------------- | -------------------------------- |
| `src/interceptors/serialize.interceptor.ts` | Custom interceptor and decorator |
| `src/users/dtos/user.dto.ts`                | Response DTO with `@Expose()`    |

### Complete Serialization Setup

**1. Create the Interceptor:**

```typescript
// src/interceptors/serialize.interceptor.ts
interface ClassConstructor {
  new (...args: any[]): {};
}

export function Serialize(dto: ClassConstructor) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

export class SerializeInterceptor implements NestInterceptor {
  constructor(private dto: ClassConstructor) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map((data: any) => {
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: true,
        });
      })
    );
  }
}
```

**2. Create Response DTO:**

```typescript
// src/users/dtos/user.dto.ts
import { Expose } from "class-transformer";

export class UserDto {
  @Expose()
  id: number;

  @Expose()
  email: string;

  // password NOT exposed
}
```

**3. Apply to Controller:**

```typescript
import { Serialize } from "../interceptors/serialize.interceptor";
import { UserDto } from "./dtos/user.dto";

@Serialize(UserDto)
@Controller("auth")
export class UsersController {
  // All routes will use UserDto serialization
}
```

### Benefits of This Approach

| Benefit         | Description                               |
| --------------- | ----------------------------------------- |
| **Security**    | Sensitive data never accidentally exposed |
| **Flexibility** | Different DTOs for different routes       |
| **Reusability** | One interceptor for all serialization     |
| **Clean Code**  | Simple `@Serialize(Dto)` syntax           |
| **Type Safety** | TypeScript catches invalid arguments      |
| **Scalability** | Easy to add new response formats          |

## Section 11: Authentication From Scratch (2026 Edition)

This section covers implementing a complete authentication system from scratch in NestJS using **2026 best practices**. You'll learn password hashing with Argon2id, JWT-based stateless authentication, and modern security patterns recommended by OWASP.

> **Updated for NestJS 11+** – This section reflects current conventions including native Node.js crypto APIs, the `@nestjs/jwt` package, and modern decorator patterns.

### 🎯 What You'll Learn & Why It Matters

| Concept | Why We Need It |
|---------|----------------|
| **Password Hashing** | Plain passwords in database = instant breach. Hashing protects users even if database is stolen |
| **JWT Tokens** | Stateless auth that works across servers, APIs, and mobile apps without storing sessions |
| **Auth Guards** | Protect routes so only logged-in users can access them |
| **Custom Decorators** | Clean code - get current user with `@CurrentUser()` instead of parsing request manually |
| **RBAC** | Different users have different permissions (admin vs user) |

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+11.1+–+Authentication+Overview" alt="Lecture 11.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture provides an overview of the authentication system we'll build, including the signup and signin flows, password encryption, and token-based authentication.

#### 🤔 Why Do We Need Authentication?

Without authentication, anyone can:
- Access any user's data
- Pretend to be someone else
- Modify or delete other users' information

**Authentication answers the question:** "Who is making this request?"

#### 🧠 The Big Picture: How Auth Works

```
┌────────────────────────────────────────────────────────────────────────────┐
│                        AUTHENTICATION FLOW                                  │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  STEP 1: SIGNUP                      STEP 2: SIGNIN                        │
│  ───────────────                     ─────────────                         │
│  User: "I want an account"           User: "I want to access my stuff"     │
│                                                                            │
│  ┌─────────────────────┐             ┌─────────────────────┐              │
│  │ email: test@test.com│             │ email: test@test.com│              │
│  │ password: secret123 │             │ password: secret123 │              │
│  └─────────┬───────────┘             └─────────┬───────────┘              │
│            │                                   │                           │
│            ▼                                   ▼                           │
│  ┌─────────────────────┐             ┌─────────────────────┐              │
│  │ Hash password       │             │ Verify password     │              │
│  │ Save to database    │             │ against stored hash │              │
│  └─────────┬───────────┘             └─────────┬───────────┘              │
│            │                                   │                           │
│            ▼                                   ▼                           │
│  ┌─────────────────────┐             ┌─────────────────────┐              │
│  │ Return JWT Token    │             │ Return JWT Token    │              │
│  │ (user's "key card") │             │ (user's "key card") │              │
│  └─────────────────────┘             └─────────────────────┘              │
│                                                                            │
│  STEP 3: ACCESSING PROTECTED RESOURCES                                     │
│  ─────────────────────────────────────                                     │
│                                                                            │
│  ┌─────────────────────────────────────────────────────────┐              │
│  │ Request: GET /users/profile                             │              │
│  │ Header: Authorization: Bearer eyJhbGciOi...             │              │
│  └───────────────────────┬─────────────────────────────────┘              │
│                          │                                                 │
│                          ▼                                                 │
│  ┌───────────────────────────────────────────────────────────┐            │
│  │ Server verifies token → Extracts user ID → Returns data   │            │
│  └───────────────────────────────────────────────────────────┘            │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

#### Authentication Flow Overview

Our authentication system will consist of two main flows:

**Signup Flow:**

1. User provides email and password
2. Validate input with class-validator
3. Check if email is already in use
4. Hash password with Argon2id (OWASP recommended)
5. Store the new user in the database
6. Issue JWT access token
7. Return token and user info

**Signin Flow:**

1. User provides email and password
2. Find user by email in database
3. Verify password against stored Argon2id hash
4. If valid, issue JWT access token
5. Return token and user info

#### 🔑 Key Concept: JWT is Like a Hotel Key Card

Think of JWT like a hotel key card:

| Hotel Key Card | JWT Token |
|----------------|-----------|
| Given at check-in | Given at signup/signin |
| Contains your room number (encoded) | Contains your user ID (encoded) |
| Hotel doesn't need to "remember" you | Server doesn't need to store session |
| Works until expiration | Works until token expires |
| Can't be forged (special encoding) | Can't be forged (cryptographic signature) |

#### Key Security Concepts (2026 Standards)

| Concept              | Description                                                                |
| -------------------- | -------------------------------------------------------------------------- |
| **Argon2id**         | OWASP-recommended password hashing algorithm (replaces bcrypt/scrypt)      |
| **JWT**              | Stateless JSON Web Tokens for API authentication                           |
| **Access Token**     | Short-lived token (15-60 min) for API access                               |
| **Refresh Token**    | Long-lived token for obtaining new access tokens (optional, covered later) |
| **HttpOnly Cookies** | Secure cookie storage for tokens (prevents XSS)                            |

#### Session vs JWT: When to Use Each

| Approach    | Use Case                               | Pros                              | Cons                         |
| ----------- | -------------------------------------- | --------------------------------- | ---------------------------- |
| **JWT**     | APIs, SPAs, Mobile apps, Microservices | Stateless, scalable, cross-origin | Token revocation complexity  |
| **Session** | Traditional web apps, SSR              | Easy revocation, simple           | Server state, scaling issues |

> **2026 Recommendation:** Use JWT for new projects. Use sessions only for traditional server-rendered applications.

#### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Auth Module                                  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────┐      ┌─────────────────┐                      │
│  │  AuthController │──────│   AuthService   │                      │
│  └────────┬────────┘      └────────┬────────┘                      │
│           │                        │                                │
│           │                        ├── Password hashing (Argon2id) │
│           │                        └── JWT generation              │
│           │                                                         │
│           ▼                        ▼                                │
│  ┌─────────────────┐      ┌─────────────────┐                      │
│  │  UsersService   │◄─────│    JwtService   │                      │
│  └────────┬────────┘      │  (@nestjs/jwt)  │                      │
│           │               └─────────────────┘                      │
│           ▼                                                         │
│  ┌─────────────────┐                                               │
│  │ UsersRepository │                                               │
│  │   (TypeORM)     │                                               │
│  └─────────────────┘                                               │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

#### What We'll Build

1. **AuthService** - Handles signup, signin, and token generation
2. **Password Hashing** - Secure storage using Argon2id (Node.js native)
3. **JWT Authentication** - Using `@nestjs/jwt` and `@nestjs/passport`
4. **AuthGuard** - Protecting routes with JWT validation
5. **CurrentUser Decorator** - Clean access to authenticated user

#### 🤔 Why Build From Scratch?

You might wonder: "Why not just use a library?"

**Building from scratch helps you:**
- **Understand security vulnerabilities** - Know where attacks happen
- **Debug issues** - When auth fails, you know where to look
- **Customize flows** - Add 2FA, social login, etc. later
- **Pass interviews** - Auth questions are common in tech interviews
- **Make better decisions** - Evaluate Auth0, Clerk, Firebase Auth properly

#### Why This Matters

Authentication is a critical part of almost every web application. Understanding the fundamentals helps you:

- Build secure applications following OWASP guidelines
- Debug authentication issues effectively
- Customize auth flows for specific requirements
- Evaluate third-party auth solutions (Auth0, Clerk, etc.) properly

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=650&lines=🎬+Lecture+11.2+–+Setting+Up+the+Auth+Module" alt="Lecture 11.2" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture sets up a dedicated Auth module following NestJS 2026 conventions, installing required packages, and configuring JWT authentication.

#### 🤔 Why Create a Separate Auth Module?

You might think: "Can't I just add auth methods to UsersService?"

**Problems with mixing auth + users:**
```
❌ UsersService handles BOTH user CRUD AND authentication
❌ Hard to test - need to mock everything
❌ Violates Single Responsibility Principle
❌ Difficult to swap auth strategies later
```

**Benefits of separate AuthModule:**
```
✅ AuthService handles ONLY authentication
✅ UsersService handles ONLY user data
✅ Easy to test each independently
✅ Can swap auth strategy without touching user code
✅ Clear separation of concerns
```

#### Installing Required Packages

```bash
npm install @nestjs/jwt @nestjs/passport passport passport-jwt
npm install -D @types/passport-jwt
```

#### 🤔 Why These Specific Packages?

| Package            | Why We Need It |
| ------------------ | ------------------------------- |
| `@nestjs/jwt`      | **Creates and verifies JWT tokens** - The core of our auth system |
| `@nestjs/passport` | **NestJS wrapper for Passport** - Makes Passport work with NestJS DI system |
| `passport`         | **The authentication "engine"** - Industry-standard auth middleware |
| `passport-jwt`     | **JWT strategy for Passport** - Teaches Passport how to validate JWTs |

#### Creating the Auth Module

Use the CLI to generate a dedicated auth module:

```bash
nest generate module auth
nest generate controller auth --no-spec
nest generate service auth --no-spec
```

#### 🤔 Why Use CLI Instead of Manual Creation?

```bash
# CLI automatically:
# 1. Creates the file with correct imports
# 2. Adds the class to the module's providers/controllers
# 3. Follows naming conventions
# 4. Saves time and prevents typos
```

#### Module Architecture (2026 Best Practice)

Separate `AuthModule` from `UsersModule` for better separation of concerns:

```
src/
├── auth/                          ← Authentication logic ONLY
│   ├── auth.module.ts
│   ├── auth.controller.ts         ← /auth/signup, /auth/signin endpoints
│   ├── auth.service.ts            ← Hash passwords, generate tokens
│   ├── strategies/
│   │   └── jwt.strategy.ts        ← How to validate incoming JWTs
│   ├── guards/
│   │   └── jwt-auth.guard.ts      ← Protect routes
│   ├── decorators/
│   │   ├── current-user.decorator.ts  ← @CurrentUser()
│   │   └── public.decorator.ts        ← @Public()
│   └── dto/
│       ├── signup.dto.ts
│       └── signin.dto.ts
└── users/                         ← User data management ONLY
    ├── users.module.ts
    ├── users.service.ts           ← findByEmail(), create(), update()
    └── user.entity.ts
```

#### Auth Module Setup

```typescript
// src/auth/auth.module.ts
import { Module } from "@nestjs/common";
import { JwtModule } from "@nestjs/jwt";
import { PassportModule } from "@nestjs/passport";
import { UsersModule } from "../users/users.module";
import { AuthController } from "./auth.controller";
import { AuthService } from "./auth.service";
import { JwtStrategy } from "./strategies/jwt.strategy";
import { ConfigModule, ConfigService } from "@nestjs/config";

@Module({
  imports: [
    UsersModule,
    PassportModule.register({ defaultStrategy: "jwt" }),
    JwtModule.registerAsync({
      imports: [ConfigModule],
      inject: [ConfigService],
      useFactory: (config: ConfigService) => ({
        secret: config.get<string>("JWT_SECRET"),
        signOptions: {
          expiresIn: config.get<string>("JWT_EXPIRES_IN", "15m"),
        },
      }),
    }),
  ],
  controllers: [AuthController],
  providers: [AuthService, JwtStrategy],
  exports: [AuthService],
})
export class AuthModule {}
```

#### 🔍 Breaking Down the Module Setup

```typescript
// Why import UsersModule?
imports: [UsersModule]  
// → AuthService needs UsersService to find/create users
// → We import the entire module, not just the service

// Why PassportModule.register()?
PassportModule.register({ defaultStrategy: "jwt" })
// → Tells Passport to use JWT as the default auth strategy
// → We don't need to specify 'jwt' every time we use @UseGuards()

// Why JwtModule.registerAsync()?
JwtModule.registerAsync({ ... })
// → We need to load JWT_SECRET from environment variables
// → registerAsync() allows us to inject ConfigService
// → Regular register() can't access environment at runtime
```

#### Environment Configuration

Create or update `.env`:

```env
JWT_SECRET=your-super-secret-key-min-32-chars-long
JWT_EXPIRES_IN=15m
```

#### 🤔 Why 15 Minutes for Token Expiry?

| Duration | Security | User Experience |
|----------|----------|-----------------|
| 5 min    | 🔒🔒🔒 Very secure | 😤 Annoying - login often |
| **15 min** | 🔒🔒 Secure | 😊 Balanced |
| 1 hour   | 🔒 Less secure | 😊 Convenient |
| 1 day    | ⚠️ Risky | 😊 Very convenient |

**15 minutes is the sweet spot** - short enough that stolen tokens can't be used long, but long enough that users aren't constantly re-authenticating.

> **Security Note:** In production, use a cryptographically random secret of at least 256 bits.

#### Updated Users Module

Export `UsersService` for use in `AuthModule`:

```typescript
// src/users/users.module.ts
import { Module } from "@nestjs/common";
import { TypeOrmModule } from "@nestjs/typeorm";
import { UsersService } from "./users.service";
import { User } from "./user.entity";

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  providers: [UsersService],
  exports: [UsersService], // Export for AuthModule
})
export class UsersModule {}
```

#### 🤔 Why Export UsersService?

```typescript
// Without exports: [UsersService]
// ❌ AuthModule cannot access UsersService
// ❌ Error: "Nest can't resolve dependencies of AuthService"

// With exports: [UsersService]  
// ✅ AuthModule can import UsersModule and use UsersService
// ✅ UsersService is now "public" to other modules
```

#### Dependency Flow

```
AuthModule
    │
    ├── imports UsersModule (for UsersService)
    ├── imports JwtModule (for JwtService)
    ├── imports PassportModule (for strategies)
    │
    └── provides
        ├── AuthService (uses UsersService + JwtService)
        └── JwtStrategy (validates tokens)
```

#### ✅ Summary: What We Did & Why

| Step | What | Why |
|------|------|-----|
| 1 | Install packages | Need JWT + Passport libraries |
| 2 | Generate AuthModule | Separate auth from user logic |
| 3 | Configure JwtModule | Set secret + expiry from env |
| 4 | Configure PassportModule | Set JWT as default strategy |
| 5 | Export UsersService | Allow AuthModule to use it |

#### Why This Matters

- **Separation of Concerns** - Auth logic isolated from user CRUD
- **Async Configuration** - JWT secrets loaded from environment
- **Module Exports** - Clean dependency sharing between modules
- **Testability** - Each module can be tested independently

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=700&lines=🎬+Lecture+11.3+–+Implementing+Signup+Functionality" alt="Lecture 11.3" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements the signup method in AuthService, using Argon2id for password hashing and returning a JWT token upon successful registration.

#### 🧠 The Signup Flow Visualized

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           SIGNUP PROCESS                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  User sends: { email: "test@test.com", password: "Secret123" }              │
│                                    │                                        │
│                                    ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 1: VALIDATE INPUT (DTO)                                        │   │
│  │ ─────────────────────────────                                       │   │
│  │ • Is email valid format? → @IsEmail()                               │   │
│  │ • Is password at least 8 chars? → @MinLength(8)                     │   │
│  │                                                                     │   │
│  │ WHY? Bad data = bad users. Catch problems early!                    │   │
│  └─────────────────────────────────┬───────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 2: CHECK IF EMAIL EXISTS                                       │   │
│  │ ────────────────────────────                                        │   │
│  │ • Query: SELECT * FROM users WHERE email = 'test@test.com'          │   │
│  │ • If found: throw ConflictException (409)                           │   │
│  │                                                                     │   │
│  │ WHY? One account per email. Prevent duplicate accounts.             │   │
│  └─────────────────────────────────┬───────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 3: HASH PASSWORD                                               │   │
│  │ ────────────────────                                                │   │
│  │ • "Secret123" → "$argon2id$v=19$m=65536,t=3,p=4$salt$hash..."      │   │
│  │ • Original password is NEVER stored!                                │   │
│  │                                                                     │   │
│  │ WHY? If database is stolen, attackers can't see real passwords.     │   │
│  └─────────────────────────────────┬───────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 4: SAVE USER TO DATABASE                                       │   │
│  │ ──────────────────────────                                          │   │
│  │ • INSERT INTO users (email, password) VALUES (...)                  │   │
│  │ • Returns user with generated ID                                    │   │
│  │                                                                     │   │
│  │ WHY? User account now exists and can be used for signin.            │   │
│  └─────────────────────────────────┬───────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ STEP 5: GENERATE JWT TOKEN                                          │   │
│  │ ───────────────────────                                             │   │
│  │ • Create payload: { sub: 1, email: "test@test.com" }                │   │
│  │ • Sign with secret → "eyJhbGciOiJIUzI1NiIs..."                      │   │
│  │                                                                     │   │
│  │ WHY? User is immediately logged in after signup.                    │   │
│  └─────────────────────────────────┬───────────────────────────────────┘   │
│                                    │                                        │
│                                    ▼                                        │
│  Response: { user: { id: 1, email: "..." }, accessToken: "eyJ..." }         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Creating the Signup DTO

```typescript
// src/auth/dto/signup.dto.ts
import { IsEmail, IsString, MinLength, MaxLength } from "class-validator";

export class SignupDto {
  @IsEmail({}, { message: "Please provide a valid email" })
  email: string;

  @IsString()
  @MinLength(8, { message: "Password must be at least 8 characters" })
  @MaxLength(128, { message: "Password must not exceed 128 characters" })
  password: string;
}
```

#### 🤔 Why These Validation Rules?

| Rule | Why |
|------|-----|
| `@IsEmail()` | Prevent typos like "test@testcom" - user can't login later |
| `@MinLength(8)` | NIST 2024 recommendation - shorter passwords are easily cracked |
| `@MaxLength(128)` | Prevent DoS attacks - hashing very long strings is slow |

#### Signup Method Implementation

```typescript
// src/auth/auth.service.ts
import {
  BadRequestException,
  Injectable,
  ConflictException,
} from "@nestjs/common";
import { JwtService } from "@nestjs/jwt";
import { UsersService } from "../users/users.service";
import * as crypto from "crypto";

@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService
  ) {}

  async signup(email: string, password: string) {
    // 1. Check if email is already in use
    const existingUser = await this.usersService.findByEmail(email);
    if (existingUser) {
      throw new ConflictException("Email already registered");
    }

    // 2. Hash the password with Argon2id
    const hashedPassword = await this.hashPassword(password);

    // 3. Create the new user
    const user = await this.usersService.create(email, hashedPassword);

    // 4. Generate JWT token
    const token = await this.generateToken(user.id, user.email);

    // 5. Return user info and token
    return {
      user: { id: user.id, email: user.email },
      accessToken: token,
    };
  }

  private async hashPassword(password: string): Promise<string> {
    // Argon2id with OWASP recommended parameters
    return new Promise((resolve, reject) => {
      crypto.hash("argon2id", password, (err, hash) => {
        if (err) reject(err);
        resolve(hash.toString("hex"));
      });
    });
  }

  private async generateToken(userId: number, email: string): Promise<string> {
    const payload = { sub: userId, email };
    return this.jwtService.signAsync(payload);
  }
}
```

#### 🔍 Code Walkthrough

```typescript
// Step 1: Why check email first?
const existingUser = await this.usersService.findByEmail(email);
if (existingUser) {
  throw new ConflictException("Email already registered");
}
// → If we don't check, database will throw duplicate key error
// → That error message might leak sensitive information
// → Better to handle it ourselves with a friendly message

// Step 2: Why hash before saving?
const hashedPassword = await this.hashPassword(password);
// → NEVER store plain passwords
// → If we save first, then hash, plain password exists in memory longer

// Step 3: Why create user with hashed password?
const user = await this.usersService.create(email, hashedPassword);
// → UsersService doesn't know about hashing - it just saves data
// → Separation of concerns: AuthService handles security

// Step 4: Why generate token immediately?
const token = await this.generateToken(user.id, user.email);
// → Better UX: user is logged in right after signup
// → No need for separate signin step
```

#### Signup Steps Breakdown

| Step | Action                      | Implementation                   |
| ---- | --------------------------- | -------------------------------- |
| 1    | Check email uniqueness      | Query database, throw if exists  |
| 2    | Hash password with Argon2id | Use Node.js native crypto.hash() |
| 3    | Create user                 | Call UsersService.create()       |
| 4    | Generate JWT                | Sign token with user payload     |
| 5    | Return response             | User info + access token         |

#### 🤔 Why ConflictException (409) Instead of BadRequest (400)?

```typescript
// ❌ Bad: 400 for duplicate
throw new BadRequestException("Email in use");
// → 400 means "your request format is wrong"
// → But the format IS correct, the data just conflicts

// ✅ Good: 409 for resource conflict
throw new ConflictException("Email already registered");
// → 409 means "resource already exists"
// → Semantically correct for duplicate email
// → Helps frontend distinguish between validation errors vs conflicts
```

#### Auth Controller

```typescript
// src/auth/auth.controller.ts
import { Controller, Post, Body, HttpCode, HttpStatus } from "@nestjs/common";
import { AuthService } from "./auth.service";
import { SignupDto } from "./dto/signup.dto";

@Controller("auth")
export class AuthController {
  constructor(private authService: AuthService) {}

  @Post("signup")
  async signup(@Body() body: SignupDto) {
    return this.authService.signup(body.email, body.password);
  }
}
```

#### ✅ Summary: What We Did & Why

| Step | What | Why |
|------|------|-----|
| 1 | Create SignupDto | Validate input before processing |
| 2 | Check email exists | Prevent duplicate accounts |
| 3 | Hash password | Never store plain passwords |
| 4 | Save user | Persist to database |
| 5 | Generate JWT | User is logged in immediately |

#### Why This Matters

- **Input Validation** - DTO with class-validator ensures data quality
- **Proper Status Codes** - 409 for conflicts, not 400
- **Argon2id** - OWASP 2024+ recommended algorithm
- **JWT Response** - Stateless authentication from signup

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=700&lines=🎬+Lecture+11.4+–+Understanding+Password+Hashing" alt="Lecture 11.4" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains the theory behind password hashing, salting, and the evolution to Argon2id as the current standard.

#### 🤔 Why Do We Need to Hash Passwords?

Imagine this scenario:

```
┌─────────────────────────────────────────────────────────────────┐
│                    😱 DATABASE BREACH!                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Hacker downloads your users table...                          │
│                                                                 │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │  PLAIN TEXT PASSWORDS (BAD!)                              │ │
│  ├───────────────────────────────────────────────────────────┤ │
│  │  email: alice@bank.com    password: MyBankPass123         │ │
│  │  email: bob@work.com      password: LetMeIn!              │ │
│  │  email: carol@gmail.com   password: Password123           │ │
│  └───────────────────────────────────────────────────────────┘ │
│                                                                 │
│  Hacker now has:                                               │
│  ✅ Access to your app (obviously)                             │
│  ✅ Access to Alice's BANK (she reused password)               │
│  ✅ Access to Bob's WORK email (he reused password)            │
│  ✅ Access to Carol's GMAIL (she reused password)              │
│                                                                 │
│  This is a CATASTROPHE! 💀                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    😌 DATABASE BREACH (with hashing)            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Hacker downloads your users table...                          │
│                                                                 │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │  HASHED PASSWORDS (GOOD!)                                 │ │
│  ├───────────────────────────────────────────────────────────┤ │
│  │  email: alice@bank.com                                    │ │
│  │  password: $argon2id$v=19$m=65536,t=3,p=4$abc123$xyz789   │ │
│  │                                                           │ │
│  │  email: bob@work.com                                      │ │
│  │  password: $argon2id$v=19$m=65536,t=3,p=4$def456$uvw012   │ │
│  └───────────────────────────────────────────────────────────┘ │
│                                                                 │
│  Hacker has:                                                   │
│  ✅ Access to your app (but we can reset all passwords)        │
│  ❌ Can't access Alice's bank (can't reverse the hash)         │
│  ❌ Can't access Bob's work (can't reverse the hash)           │
│                                                                 │
│  Damage is LIMITED! 🛡️                                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### The Problem: Plain Text Passwords

```
┌─────────────────────────────────────────┐
│           Users Table (BAD!)            │
├─────────┬─────────────────┬─────────────┤
│   ID    │      Email      │  Password   │
├─────────┼─────────────────┼─────────────┤
│    1    │ alice@test.com  │  password1  │  ← Plain text!
│    2    │ bob@test.com    │  secret123  │  ← Visible!
└─────────┴─────────────────┴─────────────┘
```

**Why This is Dangerous:**

- Database breaches expose all passwords
- Users often reuse passwords across sites
- Attackers can access users' other accounts

#### 🧠 How Hashing Works (Simple Explanation)

```
┌─────────────────────────────────────────────────────────────────┐
│                    HASHING = ONE-WAY FUNCTION                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  "password123"  ────────►  "$argon2id$v=19$m=..."              │
│                    HASH                                         │
│       ↑                         ↓                               │
│       │                         │                               │
│       │          ❌              │                               │
│       └─── CANNOT REVERSE ──────┘                               │
│                                                                 │
│  Think of it like a meat grinder:                              │
│                                                                 │
│  🥩 Steak  ────►  🍔 Ground Beef                               │
│                                                                 │
│  You can turn steak INTO ground beef...                        │
│  But you can't turn ground beef BACK into steak!               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Password Hashing Algorithm Evolution

| Era       | Algorithm    | Status             | Notes                            |
| --------- | ------------ | ------------------ | -------------------------------- |
| 1990s     | MD5          | ❌ **BROKEN**      | Fast, no salt, rainbow tables    |
| 2000s     | SHA-256      | ❌ **BROKEN**      | Fast, not designed for passwords |
| 2010s     | bcrypt       | ⚠️ Legacy          | Good but CPU-only                |
| 2015      | scrypt       | ⚠️ Legacy          | Memory-hard, complex params      |
| **2024+** | **Argon2id** | ✅ **RECOMMENDED** | Memory + time hard, OWASP std    |

#### 🤔 Why Did Old Algorithms Fail?

```
┌─────────────────────────────────────────────────────────────────┐
│                    THE SPEED PROBLEM                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  MD5/SHA: Designed to be FAST (for file checksums)             │
│                                                                 │
│  ┌─────────────────────────────────────────────────┐           │
│  │ GPU with 10,000 cores can try:                  │           │
│  │ • MD5: 50 BILLION passwords/second              │           │
│  │ • SHA-256: 10 BILLION passwords/second          │           │
│  │ • bcrypt: 50,000 passwords/second               │           │
│  │ • Argon2id: 1,000 passwords/second              │           │
│  └─────────────────────────────────────────────────┘           │
│                                                                 │
│  "password123" would be cracked in:                            │
│  • MD5: < 1 second                                             │
│  • SHA-256: < 1 second                                         │
│  • bcrypt: ~ 5 minutes                                         │
│  • Argon2id: ~ 3 hours                                         │
│                                                                 │
│  Argon2id is INTENTIONALLY SLOW! That's the feature!           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### What is Argon2id?

Argon2id combines the best of:

- **Argon2d** - Maximum resistance to GPU cracking
- **Argon2i** - Resistance to side-channel attacks

```
Password → Argon2id(memory, time, parallelism) → Hash
                     └──────────┬──────────────┘
                        Configurable work factors
```

#### OWASP 2024 Recommended Parameters

```typescript
// Argon2id configuration (Node.js 21+)
crypto.hash("argon2id", password, {
  memoryCost: 65536, // 64 MiB memory
  timeCost: 3, // 3 iterations
  parallelism: 4, // 4 parallel threads
});
```

| Parameter     | Minimum | Recommended | What It Does |
| ------------- | ------- | ----------- | ----------------------------- |
| `memoryCost`  | 19 MiB  | 64 MiB      | Forces attacker to use lots of RAM per guess |
| `timeCost`    | 2       | 3           | More iterations = slower hashing |
| `parallelism` | 1       | 4           | Uses multiple CPU threads |

#### 🤔 Why These Parameters Matter

```
┌─────────────────────────────────────────────────────────────────┐
│                    MAKING ATTACKS EXPENSIVE                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  memoryCost: 65536 (64 MiB)                                    │
│  ─────────────────────────                                      │
│  Each password guess needs 64 MB of RAM                        │
│  GPU with 1000 cores? Each core needs 64 MB                    │
│  = 64 GB RAM just for the GPU! 💰 Expensive!                   │
│                                                                 │
│  timeCost: 3                                                    │
│  ────────────                                                   │
│  3 iterations through the algorithm                            │
│  Roughly: 3x slower than timeCost: 1                           │
│                                                                 │
│  parallelism: 4                                                 │
│  ──────────────                                                 │
│  Uses 4 CPU threads for legitimate hashing                     │
│  Your server: 4 threads = fast login                           │
│  Attacker: Limited by memory, not parallelism                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Why Argon2id Beats bcrypt/scrypt

| Feature              | bcrypt     | scrypt     | Argon2id      |
| -------------------- | ---------- | ---------- | ------------- |
| Memory hardness      | ❌ No      | ✅ Yes     | ✅ Yes        |
| GPU resistance       | ⚠️ Limited | ✅ Good    | ✅ Excellent  |
| Side-channel resist. | ❌ No      | ❌ No      | ✅ Yes        |
| Modern standard      | ❌ Legacy  | ❌ Legacy  | ✅ OWASP 2024 |
| Native Node.js       | ❌ No      | ⚠️ Partial | ✅ Yes (21+)  |

#### Argon2id Output Format

```
$argon2id$v=19$m=65536,t=3,p=4$c2FsdHNhbHQ$aGFzaGhhc2g...
└───┬───┘└─┬─┘└─────┬──────┘└─────┬─────┘└──────┬──────┘
 Algorithm Version Parameters   Salt (b64)   Hash (b64)
```

**Key Insight:** Salt is embedded in the output – no manual salt handling needed!

#### 🤔 What's a Salt and Why Does Argon2id Include It?

```
┌─────────────────────────────────────────────────────────────────┐
│                    THE RAINBOW TABLE ATTACK                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  WITHOUT SALT (Bad):                                            │
│  "password123" → always produces same hash                      │
│                                                                 │
│  Attacker pre-computes hashes for 10 million common passwords  │
│  Stored in "rainbow table" - just look up hash = instant crack  │
│                                                                 │
│  WITH SALT (Good):                                              │
│  "password123" + random_salt_1 → hash_A                        │
│  "password123" + random_salt_2 → hash_B (completely different!) │
│                                                                 │
│  Rainbow tables become useless - can't pre-compute all salts   │
│                                                                 │
│  Argon2id generates random salt automatically! 🎉               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Verification Process

```typescript
// Signup: Hash password
const hash = await crypto.hash("argon2id", password);
// Store hash in database

// Signin: Verify password
const isValid = await crypto.verify("argon2id", password, storedHash);
// Returns true/false
```

The `verify()` function automatically:

1. Extracts salt from stored hash
2. Hashes provided password with same parameters
3. Compares securely (constant-time)

#### ✅ Summary: What We Learned

| Concept | Why It Matters |
|---------|----------------|
| **Never store plain passwords** | Database breaches expose everything |
| **Use slow hashing** | Makes brute-force attacks expensive |
| **Use Argon2id in 2024+** | OWASP recommended, memory-hard |
| **Salt is automatic** | Prevents rainbow table attacks |

#### Why This Matters

- **OWASP Standard** - Argon2id is the current recommendation
- **Built-in Salt** - No manual salt generation errors
- **Native Node.js** - No external packages needed (Node 21+)
- **Future-proof** - Parameters encoded for later verification

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=700&lines=🎬+Lecture+11.5+–+Implementing+Password+Hashing" alt="Lecture 11.5" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements password hashing using Node.js native crypto module with Argon2id, following OWASP 2024+ recommendations.

#### Node.js Version Requirements

| Node Version | Argon2id Support                            |
| ------------ | ------------------------------------------- |
| < 21         | ❌ Requires external package (argon2)       |
| 21+          | ✅ Native crypto.hash() and crypto.verify() |
| 22+ LTS      | ✅ Stable, production-ready                 |

> **Note:** If using Node < 21, install the `argon2` package instead.

#### Option A: Node.js 21+ (Native Argon2id)

```typescript
// src/auth/auth.service.ts
import * as crypto from "crypto";

@Injectable()
export class AuthService {
  private async hashPassword(password: string): Promise<string> {
    return new Promise((resolve, reject) => {
      crypto.hash(
        "argon2id",
        Buffer.from(password),
        {
          memoryCost: 65536, // 64 MiB
          timeCost: 3, // 3 iterations
          parallelism: 4, // 4 threads
        },
        (err, hash) => {
          if (err) reject(err);
          resolve(hash.toString("base64"));
        }
      );
    });
  }

  private async verifyPassword(
    password: string,
    hash: string
  ): Promise<boolean> {
    return new Promise((resolve, reject) => {
      crypto.verify(
        "argon2id",
        Buffer.from(password),
        Buffer.from(hash, "base64"),
        (err, result) => {
          if (err) reject(err);
          resolve(result);
        }
      );
    });
  }
}
```

#### Option B: Using argon2 Package (Node < 21 or Cross-Platform)

```bash
npm install argon2
```

```typescript
// src/auth/auth.service.ts
import * as argon2 from "argon2";

@Injectable()
export class AuthService {
  private async hashPassword(password: string): Promise<string> {
    return argon2.hash(password, {
      type: argon2.argon2id,
      memoryCost: 65536,
      timeCost: 3,
      parallelism: 4,
    });
  }

  private async verifyPassword(
    password: string,
    hash: string
  ): Promise<boolean> {
    return argon2.verify(hash, password);
  }
}
```

#### Complete AuthService with Hashing

```typescript
// src/auth/auth.service.ts
import {
  Injectable,
  ConflictException,
  UnauthorizedException,
} from "@nestjs/common";
import { JwtService } from "@nestjs/jwt";
import { UsersService } from "../users/users.service";
import * as argon2 from "argon2";

@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService
  ) {}

  async signup(email: string, password: string) {
    // 1. Check if email exists
    const existingUser = await this.usersService.findByEmail(email);
    if (existingUser) {
      throw new ConflictException("Email already registered");
    }

    // 2. Hash password with Argon2id
    const hashedPassword = await this.hashPassword(password);

    // 3. Create user
    const user = await this.usersService.create(email, hashedPassword);

    // 4. Generate and return JWT
    return this.createAuthResponse(user);
  }

  async signin(email: string, password: string) {
    // 1. Find user by email
    const user = await this.usersService.findByEmail(email);
    if (!user) {
      throw new UnauthorizedException("Invalid credentials");
    }

    // 2. Verify password
    const isValid = await this.verifyPassword(password, user.password);
    if (!isValid) {
      throw new UnauthorizedException("Invalid credentials");
    }

    // 3. Generate and return JWT
    return this.createAuthResponse(user);
  }

  private async hashPassword(password: string): Promise<string> {
    return argon2.hash(password, {
      type: argon2.argon2id,
      memoryCost: 65536,
      timeCost: 3,
      parallelism: 4,
    });
  }

  private async verifyPassword(
    password: string,
    hash: string
  ): Promise<boolean> {
    return argon2.verify(hash, password);
  }

  private async createAuthResponse(user: { id: number; email: string }) {
    const payload = { sub: user.id, email: user.email };
    const accessToken = await this.jwtService.signAsync(payload);

    return {
      user: { id: user.id, email: user.email },
      accessToken,
    };
  }
}
```

#### 🔍 Code Walkthrough: Why Each Part?

```typescript
// Why private methods for hashPassword/verifyPassword?
private async hashPassword(password: string): Promise<string> { ... }
// → Keeps the main signup/signin methods clean and readable
// → Can be reused in password reset, change password, etc.
// → Easy to swap hashing algorithm later (just change one place)

// Why createAuthResponse helper?
private async createAuthResponse(user) { ... }
// → Both signup and signin return the same structure
// → DRY principle - Don't Repeat Yourself
// → If we change response format, only change one place
```

#### 🛡️ Security Best Practice: Generic Error Messages

```typescript
// ❌ Bad: Reveals if email exists
throw new NotFoundException("User not found");
throw new BadRequestException("Wrong password");

// ✅ Good: Same error for both cases
throw new UnauthorizedException("Invalid credentials");
```

#### 🤔 Why Same Error Message for Both Cases?

```
┌─────────────────────────────────────────────────────────────────┐
│                    EMAIL ENUMERATION ATTACK                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Attacker tries: login("alice@target.com", "random")           │
│                                                                 │
│  ❌ BAD API Response: "User not found"                         │
│  → Attacker knows: alice@target.com is NOT registered          │
│                                                                 │
│  Attacker tries: login("bob@target.com", "random")             │
│  ❌ BAD API Response: "Wrong password"                         │
│  → Attacker knows: bob@target.com IS registered! 🎯             │
│  → Now attacker can brute-force Bob's password                 │
│  → Or send phishing email to Bob                               │
│                                                                 │
│  ✅ GOOD API Response: "Invalid credentials" (always)          │
│  → Attacker learns nothing about which emails exist            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### ✅ Summary: What We Implemented

| Method | Purpose |
|--------|---------|
| `hashPassword()` | Converts plain password → Argon2id hash |
| `verifyPassword()` | Checks if password matches stored hash |
| `createAuthResponse()` | Creates standard response with JWT |
| Generic errors | Prevents email enumeration attacks |

#### Why This Matters

- **OWASP Compliance** - Argon2id is the 2024+ standard
- **Memory-Hard** - Resistant to GPU/ASIC attacks
- **Native Support** - No external dependencies (Node 21+)
- **Secure Defaults** - Salt handled automatically

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=DC3545&center=true&vCenter=true&width=550&lines=🎬+Lecture+11.6+–+JWT+Token+Generation" alt="Lecture 11.6" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture explains JWT structure, token generation, and wiring up the complete signup flow with token response.

#### 🤔 Why Do We Need JWT Tokens?

The problem with HTTP:

```
┌─────────────────────────────────────────────────────────────────┐
│                    HTTP IS STATELESS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Request 1: POST /auth/signin                                   │
│  Response: "Welcome, you're logged in!"                        │
│                                                                 │
│  Request 2: GET /users/profile                                  │
│  Server: "Who are you? I don't remember Request 1"             │
│                                                                 │
│  HTTP doesn't remember previous requests!                       │
│  Each request is completely independent.                        │
│                                                                 │
│  SOLUTION: Send proof of identity with EVERY request           │
│  → That proof is the JWT token!                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### JWT Structure

A JWT consists of three parts separated by dots:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjEsImVtYWlsIjoidGVzdEB0ZXN0LmNvbSIsImlhdCI6MTcwNDA2NzIwMCwiZXhwIjoxNzA0MDY4MTAwfQ.signature
└──────────────┬──────────────┘ └─────────────────────────────────┬─────────────────────────────────┘ └────┬────┘
            Header                                              Payload                                Signature
```

| Part      | Contents                           | Encoded |
| --------- | ---------------------------------- | ------- |
| Header    | Algorithm, token type              | Base64  |
| Payload   | User claims (sub, email, iat, exp) | Base64  |
| Signature | HMAC of header + payload + secret  | Base64  |

#### 🔍 JWT Decoded (What's Inside?)

```
┌─────────────────────────────────────────────────────────────────┐
│                    JWT TOKEN ANATOMY                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  HEADER (tells how to verify):                                  │
│  {                                                              │
│    "alg": "HS256",    // Algorithm: HMAC with SHA-256          │
│    "typ": "JWT"       // Type: JSON Web Token                  │
│  }                                                              │
│                                                                 │
│  PAYLOAD (the actual data):                                     │
│  {                                                              │
│    "sub": 1,              // Subject: User ID                  │
│    "email": "test@test.com",  // Custom claim                  │
│    "iat": 1704067200,     // Issued At: When created           │
│    "exp": 1704068100      // Expires: When it's no longer valid│
│  }                                                              │
│                                                                 │
│  SIGNATURE (proves it's not tampered):                          │
│  HMACSHA256(                                                    │
│    base64(header) + "." + base64(payload),                     │
│    JWT_SECRET                                                   │
│  )                                                              │
│                                                                 │
│  ⚠️ IMPORTANT: Payload is NOT encrypted, just encoded!         │
│  Anyone can decode and read it. Don't put secrets in payload!  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### JWT Payload Claims

```typescript
{
  sub: 1,                    // Subject (user ID)
  email: 'test@test.com',    // Custom claim
  iat: 1704067200,           // Issued at (auto)
  exp: 1704068100            // Expires at (auto)
}
```

| Claim   | Meaning           | Required | Who Sets It |
| ------- | ----------------- | -------- | ----------- |
| `sub`   | Subject (user ID) | ✅ Yes   | You |
| `email` | User email        | Optional | You |
| `iat`   | Issued at time    | Auto     | JwtService |
| `exp`   | Expiration time   | Auto     | JwtService (from config) |

#### 🤔 Why Use `sub` for User ID?

```typescript
// ❌ Works but non-standard
{ userId: 1, userEmail: 'test@test.com' }

// ✅ Standard JWT claim names
{ sub: 1, email: 'test@test.com' }
```

- `sub` is the standard JWT claim for "subject" (who the token is about)
- Standard names are recognized by JWT libraries, debuggers, etc.
- Makes your tokens compatible with other systems

#### Token Generation with @nestjs/jwt

```typescript
// src/auth/auth.service.ts
import { JwtService } from "@nestjs/jwt";

@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService
  ) {}

  private async createAuthResponse(user: { id: number; email: string }) {
    const payload = {
      sub: user.id,
      email: user.email,
    };

    const accessToken = await this.jwtService.signAsync(payload);

    return {
      user: {
        id: user.id,
        email: user.email,
      },
      accessToken,
    };
  }
}
```

#### Auth Controller with Complete Signup

```typescript
// src/auth/auth.controller.ts
import { Controller, Post, Body, HttpCode, HttpStatus } from "@nestjs/common";
import { AuthService } from "./auth.service";
import { SignupDto } from "./dto/signup.dto";
import { SigninDto } from "./dto/signin.dto";

@Controller("auth")
export class AuthController {
  constructor(private authService: AuthService) {}

  @Post("signup")
  async signup(@Body() body: SignupDto) {
    return this.authService.signup(body.email, body.password);
  }

  @Post("signin")
  @HttpCode(HttpStatus.OK) // Return 200, not 201
  async signin(@Body() body: SigninDto) {
    return this.authService.signin(body.email, body.password);
  }
}
```

#### Testing the Signup Flow

**Request:**

```http
POST http://localhost:3000/auth/signup
Content-Type: application/json

{
  "email": "newuser@test.com",
  "password": "SecureP@ss123"
}
```

**Response (201 Created):**

```json
{
  "user": {
    "id": 1,
    "email": "newuser@test.com"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### Important: Never Return Password

```typescript
// ❌ Bad: Exposes hashed password
return user;

// ✅ Good: Return only safe fields
return {
  user: { id: user.id, email: user.email },
  accessToken,
};
```

#### Complete Flow

```
POST /auth/signup
        │
        ▼
AuthController.signup()
        │
        ▼
AuthService.signup()
        │
        ├── Check email uniqueness
        ├── Hash password (Argon2id)
        ├── Create user in DB
        ├── Generate JWT
        │
        ▼
Return { user, accessToken }
```

#### Why This Matters

- **Stateless Auth** - No server-side session storage
- **Scalable** - Works across multiple servers
- **Standard Format** - JWT is industry standard
- **Secure Response** - Never expose password hashes

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=17A2B8&center=true&vCenter=true&width=600&lines=🎬+Lecture+11.7+–+Implementing+Sign+In" alt="Lecture 11.7" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements the signin method, which verifies credentials using Argon2id and returns a JWT token.

#### 🤔 Why Is Signin Different from Signup?

```
┌─────────────────────────────────────────────────────────────────┐
│                    SIGNUP vs SIGNIN                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SIGNUP: "I don't have an account, please create one"          │
│  ─────────────────────────────────────────────────              │
│  • Check email is NOT already used                             │
│  • HASH the password (create new hash)                         │
│  • INSERT into database                                        │
│  • Return 201 Created                                          │
│                                                                 │
│  SIGNIN: "I already have an account, let me in"                │
│  ────────────────────────────────────────────                   │
│  • Check email IS already used                                 │
│  • VERIFY password against stored hash                         │
│  • SELECT from database (don't insert)                         │
│  • Return 200 OK                                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Signin Flow

```
User Input: email + password
              │
              ▼
┌─────────────────────────────────┐
│  1. Find user by email          │  ← Does this email exist?
└───────────────┬─────────────────┘
                │
                ▼
┌─────────────────────────────────┐
│  2. Verify password (Argon2id)  │  ← Does password match hash?
└───────────────┬─────────────────┘
                │
       ┌────────┴────────┐
       │                 │
    Valid?            Invalid?
       │                 │
       ▼                 ▼
  Generate JWT     401 Unauthorized
       │           "Invalid credentials"
       ▼
  Return token
```

#### Complete Signin Implementation

```typescript
// src/auth/auth.service.ts
async signin(email: string, password: string) {
  // 1. Find user by email
  const user = await this.usersService.findByEmail(email);
  if (!user) {
    // Use same error to prevent email enumeration
    throw new UnauthorizedException('Invalid credentials');
  }

  // 2. Verify password with Argon2id
  const isValid = await this.verifyPassword(password, user.password);
  if (!isValid) {
    throw new UnauthorizedException('Invalid credentials');
  }

  // 3. Generate and return JWT
  return this.createAuthResponse(user);
}
```

#### 🔍 Code Walkthrough: Why Each Step?

```typescript
// Step 1: Why find user first?
const user = await this.usersService.findByEmail(email);
// → Need the stored hash to verify password
// → If user doesn't exist, can't verify anything

// Step 2: Why use verifyPassword instead of comparing hashes?
const isValid = await this.verifyPassword(password, user.password);
// → Can't just compare: hash("password") !== stored_hash
// → Argon2id uses random salt, same password = different hash each time
// → argon2.verify() extracts salt from stored hash, re-hashes, compares

// Step 3: Why same response as signup?
return this.createAuthResponse(user);
// → After signin, user needs a token just like after signup
// → Consistent API: both return { user, accessToken }
```

#### Signin DTO

```typescript
// src/auth/dto/signin.dto.ts
import { IsEmail, IsString } from "class-validator";

export class SigninDto {
  @IsEmail()
  email: string;

  @IsString()
  password: string;
}
```

#### 🤔 Why Less Strict Validation on Signin?

```typescript
// Signup DTO - Strict validation
@MinLength(8, { message: 'Password must be at least 8 characters' })
// → We enforce rules when CREATING passwords

// Signin DTO - Just check it's a string
@IsString()
// → User might have old account with 6-char password
// → Don't lock them out! Let Argon2id verify
```

#### 🛡️ Security: Prevent Timing Attacks

```typescript
// ❌ Bad: Different response times reveal info
const user = await this.usersService.findByEmail(email);
if (!user) {
  // Returns quickly - no database lookup for password
  throw new UnauthorizedException("Invalid credentials");
}
// Returns slowly - database lookup + hash verification
const isValid = await this.verifyPassword(password, user.password);
```

```typescript
// ✅ Better: Always do verification work
const user = await this.usersService.findByEmail(email);
if (!user) {
  // Still run hash to match timing
  await this.verifyPassword(
    password,
    "$argon2id$v=19$m=65536,t=3,p=4$dummy$hash"
  );
  throw new UnauthorizedException("Invalid credentials");
}
```

#### Testing Signin

**Valid Credentials:**

```http
POST http://localhost:3000/auth/signin
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "SecureP@ss123"
}
```

**Response (200 OK):**

```json
{
  "user": {
    "id": 1,
    "email": "test@test.com"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Invalid Credentials:**

```http
POST http://localhost:3000/auth/signin
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "wrongpassword"
}
```

**Response (401 Unauthorized):**

```json
{
  "statusCode": 401,
  "message": "Invalid credentials",
  "error": "Unauthorized"
}
```

#### 🤔 Why @HttpCode Decorator?

```typescript
@Post('signin')
@HttpCode(HttpStatus.OK)  // Returns 200 instead of 201
async signin(@Body() body: SigninDto) {
  return this.authService.signin(body.email, body.password);
}
```

| Decorator                  | Effect      | Use Case                |
| -------------------------- | ----------- | ----------------------- |
| Default (none)             | 201 Created | When creating resources |
| `@HttpCode(HttpStatus.OK)` | 200 OK      | When authenticating     |

```
POST /auth/signup → 201 Created (we created a new user)
POST /auth/signin → 200 OK (we didn't create anything, just verified)
```

#### ✅ Summary: Signin vs Signup

| Aspect | Signup | Signin |
|--------|--------|--------|
| User exists? | Must NOT exist | Must exist |
| Password | HASH it (create) | VERIFY it (check) |
| Database | INSERT new user | SELECT existing user |
| HTTP Code | 201 Created | 200 OK |
| Same response? | ✅ { user, token } | ✅ { user, token } |

#### Why This Matters

- **Secure Verification** - Argon2id handles complexity
- **Generic Errors** - Prevent information leakage
- **Proper Status Codes** - 200 for signin, 401 for failure
- **JWT Response** - Client stores token for future requests

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=550&lines=🎬+Lecture+11.8+–+JWT+Strategy+Setup" alt="Lecture 11.8" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture creates the JWT Strategy for Passport, enabling automatic token validation on protected routes.

#### 🤔 Why Do We Need a "Strategy"?

Think of Passport like a security guard. The **Strategy** is the guard's training manual - it tells them:

1. **Where to find credentials** (Authorization header)
2. **How to verify them** (JWT signature + secret)
3. **What to do after verification** (fetch user from database)

```
┌─────────────────────────────────────────────────────────────────┐
│                    WITHOUT STRATEGY                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Every controller would need:                                   │
│  ❌ Extract token from header                                  │
│  ❌ Verify signature                                           │
│  ❌ Check expiration                                           │
│  ❌ Decode payload                                             │
│  ❌ Fetch user from database                                   │
│  ❌ Handle all error cases                                     │
│                                                                 │
│  Repeated in EVERY protected route! 😱                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    WITH STRATEGY                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Strategy handles all the work once:                            │
│  ✅ Token extraction                                           │
│  ✅ Signature verification                                     │
│  ✅ Expiration check                                           │
│  ✅ User lookup                                                │
│                                                                 │
│  Controller just adds @UseGuards(JwtAuthGuard) 🎉               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### What is a Passport Strategy?

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         JWT Strategy Flow                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Request with Authorization Header                                      │
│  ┌─────────────────────────────────────────────────────┐               │
│  │ Authorization: Bearer eyJhbGciOiJIUzI1Ni...         │               │
│  └──────────────────────┬──────────────────────────────┘               │
│                         │                                               │
│                         ▼                                               │
│              ┌─────────────────────┐                                   │
│              │    JwtStrategy      │  ← Passport runs this            │
│              │   (passport-jwt)    │                                   │
│              └──────────┬──────────┘                                   │
│                         │                                               │
│                         ▼  Extract & Validate Token                    │
│              ┌─────────────────────┐                                   │
│              │ Decoded Payload     │                                   │
│              │ { sub: 1, email }   │                                   │
│              └──────────┬──────────┘                                   │
│                         │                                               │
│                         ▼  YOUR validate() method                      │
│              ┌─────────────────────┐                                   │
│              │ Fetch user from DB  │                                   │
│              │ Return user object  │                                   │
│              │ Attached to request │  → request.user = user           │
│              └─────────────────────┘                                   │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

#### Creating the JWT Strategy

```typescript
// src/auth/strategies/jwt.strategy.ts
import { Injectable, UnauthorizedException } from "@nestjs/common";
import { ConfigService } from "@nestjs/config";
import { PassportStrategy } from "@nestjs/passport";
import { ExtractJwt, Strategy } from "passport-jwt";
import { UsersService } from "../../users/users.service";

export interface JwtPayload {
  sub: number;
  email: string;
  iat: number;
  exp: number;
}

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(
    private configService: ConfigService,
    private usersService: UsersService
  ) {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: configService.get<string>("JWT_SECRET"),
    });
  }

  async validate(payload: JwtPayload) {
    const user = await this.usersService.findOne(payload.sub);
    if (!user) {
      throw new UnauthorizedException("User not found");
    }
    return user;
  }
}
```

#### 🔍 Code Walkthrough: Why Each Part?

```typescript
// Why extend PassportStrategy(Strategy)?
export class JwtStrategy extends PassportStrategy(Strategy)
// → PassportStrategy is a NestJS wrapper
// → Strategy is passport-jwt's JWT strategy
// → Combines them to work with NestJS DI

// Why these super() options?
super({
  jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
  // → Tells Passport: Look for token in "Authorization: Bearer xxx"
  
  ignoreExpiration: false,
  // → Tells Passport: Reject expired tokens (we want this!)
  
  secretOrKey: configService.get<string>('JWT_SECRET'),
  // → The secret used to verify signature (must match sign secret)
});

// Why do we need validate()?
async validate(payload: JwtPayload) {
  // → Called ONLY AFTER token is verified
  // → Passport already checked signature and expiration
  // → We just need to fetch the user from database
  
  const user = await this.usersService.findOne(payload.sub);
  // → payload.sub is the user ID we put in the token at signin
  
  return user;
  // → This returned value becomes request.user
}
```

#### Strategy Configuration Options

| Option             | Value                                    | Why |
| ------------------ | ---------------------------------------- | --- |
| `jwtFromRequest`   | `ExtractJwt.fromAuthHeaderAsBearerToken` | Standard location for JWT in APIs |
| `ignoreExpiration` | `false`                                  | Expired tokens should be rejected |
| `secretOrKey`      | From config                              | Must match the signing secret |

#### Token Extraction Methods

```typescript
// From Authorization header (recommended for APIs)
ExtractJwt.fromAuthHeaderAsBearerToken();
// Expects: Authorization: Bearer <token>
// Why? Standard for REST APIs, works with mobile apps

// From cookie (for web apps with HttpOnly cookies)
ExtractJwt.fromExtractors([(request) => request?.cookies?.access_token]);
// Why? HttpOnly cookies prevent XSS attacks

// Combined (try multiple sources)
ExtractJwt.fromExtractors([
  ExtractJwt.fromAuthHeaderAsBearerToken(),
  (request) => request?.cookies?.access_token,
]);
// Why? Support both API clients and web apps
```

#### 🤔 Why Fetch User in validate()?

```typescript
async validate(payload: JwtPayload) {
  // We already have user info in payload (sub, email)
  // Why fetch from database again?
  
  // Reason 1: User might have been deleted
  const user = await this.usersService.findOne(payload.sub);
  if (!user) {
    throw new UnauthorizedException('User not found');
  }
  // → Token valid but user deleted = should deny access
  
  // Reason 2: Might need fresh user data (role changes, etc.)
  // → Token says "admin", but role was revoked
  // → Database has the truth
  
  // Reason 3: Controller needs full user object
  return user;
  // → request.user will have id, email, role, etc.
}
```

#### Register in Auth Module

```typescript
// src/auth/auth.module.ts
import { JwtStrategy } from "./strategies/jwt.strategy";

@Module({
  imports: [
    UsersModule,
    ConfigModule,
    PassportModule.register({ defaultStrategy: "jwt" }),
    JwtModule.registerAsync({
      /* ... */
    }),
  ],
  controllers: [AuthController],
  providers: [AuthService, JwtStrategy],  // ← Add JwtStrategy to providers
  exports: [AuthService],
})
export class AuthModule {}
```

#### ✅ Summary: What JwtStrategy Does

| Stage | Who Does It | What Happens |
|-------|-------------|--------------|
| 1. Extract | Passport | Finds token in Authorization header |
| 2. Decode | Passport | Base64 decodes header + payload |
| 3. Verify | Passport | Checks signature with secret |
| 4. Expiry | Passport | Rejects if exp < now |
| 5. Validate | **You** | Fetch user, attach to request |

#### Why This Matters

- **Automatic Validation** - Passport handles token parsing
- **Extensible** - Easy to add custom validation logic
- **Type-Safe** - TypeScript interfaces for payload
- **Decoupled** - Strategy separate from guards

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=700&lines=🎬+Lecture+11.9+–+Creating+the+JWT+Auth+Guard" alt="Lecture 11.9" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture creates the JWT Auth Guard for protecting routes, using the built-in `AuthGuard` from Passport.

#### 🤔 Why Do We Need a Guard?

Think of it like a security checkpoint:

```
┌─────────────────────────────────────────────────────────────────┐
│                    REAL-WORLD ANALOGY                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  🏢 Office Building Security                                    │
│  ─────────────────────────────                                  │
│                                                                 │
│  STRATEGY = "How to verify the key card"                        │
│  → Knows the algorithm, has the master key                      │
│                                                                 │
│  GUARD = "The security checkpoint"                              │
│  → Decides: "Do you need to show a key card?"                   │
│  → Public areas: No check needed                                │
│  → Restricted areas: Must verify card                           │
│                                                                 │
│  Without guard: Strategy never runs (no checkpoint!)            │
│  Without strategy: Guard has nothing to verify with             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 🤔 Why Global Guard with @Public() Opt-out?

Two approaches to security:

```
┌─────────────────────────────────────────────────────────────────┐
│                    APPROACH 1: OPT-IN (Not Recommended)         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  @Get('public-route')                                           │
│  publicRoute() { }          // ⚠️ Open by default               │
│                                                                 │
│  @UseGuards(JwtAuthGuard)   // Must remember to add!            │
│  @Get('protected-route')                                        │
│  protectedRoute() { }                                           │
│                                                                 │
│  PROBLEM: Forget @UseGuards = security hole! 😱                 │
│  Human error is inevitable over time.                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    APPROACH 2: OPT-OUT (Recommended) ✅          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  @Get('protected-route')                                        │
│  protectedRoute() { }       // ✅ Protected by default          │
│                                                                 │
│  @Public()                  // Explicitly mark as open          │
│  @Get('public-route')                                           │
│  publicRoute() { }                                              │
│                                                                 │
│  BENEFIT: Forget @Public() = route stays protected              │
│  Safe by default! 🛡️                                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Creating the JWT Auth Guard

```typescript
// src/auth/guards/jwt-auth.guard.ts
import { Injectable, ExecutionContext } from "@nestjs/common";
import { AuthGuard } from "@nestjs/passport";
import { Reflector } from "@nestjs/core";
import { IS_PUBLIC_KEY } from "../decorators/public.decorator";

@Injectable()
export class JwtAuthGuard extends AuthGuard("jwt") {
  constructor(private reflector: Reflector) {
    super();
  }

  canActivate(context: ExecutionContext) {
    // Check if route is marked as public
    const isPublic = this.reflector.getAllAndOverride<boolean>(IS_PUBLIC_KEY, [
      context.getHandler(),
      context.getClass(),
    ]);

    if (isPublic) {
      return true;
    }

    // Otherwise, use JWT validation
    return super.canActivate(context);
  }
}
```

#### 🔍 Code Walkthrough: Understanding Each Part

```typescript
// Why extend AuthGuard('jwt')?
export class JwtAuthGuard extends AuthGuard('jwt')
// → AuthGuard is Passport's generic guard
// → 'jwt' tells it to use JwtStrategy we created
// → Automatically handles token extraction + validation

// Why inject Reflector?
constructor(private reflector: Reflector) {
  super();
}
// → Reflector reads metadata (decorators) from routes
// → We need it to check for @Public() decorator

// Why override canActivate?
canActivate(context: ExecutionContext) {
  // ExecutionContext = information about current request
  
  const isPublic = this.reflector.getAllAndOverride<boolean>(
    IS_PUBLIC_KEY,  // The metadata key we're looking for
    [
      context.getHandler(),  // Check the route method first
      context.getClass(),    // Then check the controller class
    ]
  );
  // → Returns true if @Public() decorator is present

  if (isPublic) {
    return true;  // Skip authentication
  }

  return super.canActivate(context);
  // → Calls AuthGuard's logic (runs JwtStrategy)
}
```

#### Creating the @Public() Decorator

```typescript
// src/auth/decorators/public.decorator.ts
import { SetMetadata } from "@nestjs/common";

export const IS_PUBLIC_KEY = "isPublic";
export const Public = () => SetMetadata(IS_PUBLIC_KEY, true);
```

#### 🔍 How SetMetadata Works

```typescript
// When you write:
@Public()
@Post('signup')
signup() { }

// NestJS internally does:
SetMetadata('isPublic', true)
// → Attaches { isPublic: true } as metadata to signup()

// Later, Reflector reads it:
reflector.get('isPublic', context.getHandler())
// → Returns true
```

#### Using the Guard

**Option 1: Per-Route (Not Recommended)**

```typescript
import { UseGuards } from "@nestjs/common";
import { JwtAuthGuard } from "./guards/jwt-auth.guard";

@Controller("reports")
export class ReportsController {
  @Get()
  @UseGuards(JwtAuthGuard)  // Must add to every route!
  getReports() {
    // Protected route
  }
}
```

**Option 2: Per-Controller**

```typescript
@Controller("reports")
@UseGuards(JwtAuthGuard)  // All routes in this controller protected
export class ReportsController {
  // All routes protected
}
```

**Option 3: Global (Recommended) ✅**

```typescript
// src/app.module.ts
import { APP_GUARD } from "@nestjs/core";
import { JwtAuthGuard } from "./auth/guards/jwt-auth.guard";

@Module({
  providers: [
    {
      provide: APP_GUARD,
      useClass: JwtAuthGuard,
    },
  ],
})
export class AppModule {}
```

#### 🤔 Why Use APP_GUARD?

```typescript
// APP_GUARD is a special token
{
  provide: APP_GUARD,    // NestJS recognizes this
  useClass: JwtAuthGuard // Uses DI to create the guard
}

// Why not just use useValue?
// ❌ { provide: APP_GUARD, useValue: new JwtAuthGuard() }
// → Guard needs Reflector injected, can't do that manually

// ✅ useClass lets NestJS handle dependency injection
```

#### Making Public Routes

With global guard, use `@Public()` to skip authentication:

```typescript
import { Public } from "./auth/decorators/public.decorator";

@Controller("auth")
export class AuthController {
  @Public()  // ← Anyone can access signup
  @Post("signup")
  signup(@Body() body: SignupDto) {
    return this.authService.signup(body.email, body.password);
  }

  @Public()  // ← Anyone can access signin
  @Post("signin")
  signin(@Body() body: SigninDto) {
    return this.authService.signin(body.email, body.password);
  }
  
  // No @Public() = requires valid JWT token
  @Get("whoami")
  whoAmI(@CurrentUser() user: User) {
    return user;
  }
}
```

#### Guard Execution Flow

```
Request arrives
      │
      ▼
┌─────────────────────────────────────┐
│         JwtAuthGuard.canActivate()  │
├─────────────────────────────────────┤
│                                     │
│  1. Check for @Public() metadata    │
│     ├──► Yes ──► return true        │──► Skip to Route Handler
│     └──► No ──► continue            │
│                                     │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│     super.canActivate(context)      │
├─────────────────────────────────────┤
│                                     │
│  2. Extract token from header       │
│     └──► No token ──► 401           │
│                                     │
│  3. Verify token signature          │
│     └──► Invalid ──► 401            │
│                                     │
│  4. Check expiration                │
│     └──► Expired ──► 401            │
│                                     │
│  5. Call JwtStrategy.validate()     │
│     └──► User not found ──► 401     │
│                                     │
│  6. Attach user to request.user     │
│                                     │
└─────────────────┬───────────────────┘
                  │ Success
                  ▼
            Route Handler
```

#### ✅ Summary: Guard vs Strategy

| Component | Purpose | When It Runs |
|-----------|---------|--------------|
| **JwtAuthGuard** | Decides IF to authenticate | Before every request |
| **JwtStrategy** | HOW to authenticate | Only if guard says "check" |
| **@Public()** | Opt-out marker | Read by guard |
| **Reflector** | Reads decorator metadata | Inside guard |

#### Why This Matters

- **Global Protection** - All routes protected by default
- **Opt-out Model** - Use @Public() for open routes
- **Safe by Default** - Forgetting a decorator doesn't create holes
- **Passport Integration** - Leverages battle-tested library

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=600&lines=🎬+Lecture+11.10+–+CurrentUser+Decorator" alt="Lecture 11.10" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture creates a custom `@CurrentUser()` decorator to cleanly access the authenticated user in route handlers.

#### 🤔 Why Do We Need a Custom Decorator?

The problem with accessing `request.user` directly:

```
┌─────────────────────────────────────────────────────────────────┐
│                    WITHOUT @CurrentUser()                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  @Get('profile')                                                │
│  getProfile(@Req() req: Request) {                              │
│    return req.user;                                             │
│  }                                                              │
│                                                                 │
│  PROBLEMS:                                                      │
│  ❌ req.user is type `any` - no autocomplete                   │
│  ❌ Must import Request from express                           │
│  ❌ Couples code to express (what about Fastify?)              │
│  ❌ Verbose - accessing nested property                        │
│  ❌ Hard to test - must mock entire request object             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    WITH @CurrentUser() ✅                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  @Get('profile')                                                │
│  getProfile(@CurrentUser() user: User) {                        │
│    return user;                                                 │
│  }                                                              │
│                                                                 │
│  BENEFITS:                                                      │
│  ✅ user is type User - full autocomplete & type safety        │
│  ✅ Platform agnostic - works with Express or Fastify          │
│  ✅ Clean, declarative code                                    │
│  ✅ Easy to test - just pass a User object                     │
│  ✅ Self-documenting - clear what the parameter is             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### The Problem in Detail

After JWT validation, user is attached to `request.user`:

```typescript
@Get('profile')
@UseGuards(JwtAuthGuard)
getProfile(@Req() req: Request) {
  const user = req.user;
  // user is type 'any' 😞
  // No autocomplete for user.id, user.email, etc.
  // TypeScript can't catch typos like user.emial
  return user;
}
```

#### The Solution: @CurrentUser() Decorator

```typescript
// src/auth/decorators/current-user.decorator.ts
import { createParamDecorator, ExecutionContext } from "@nestjs/common";
import { User } from "../../users/user.entity";

export const CurrentUser = createParamDecorator(
  (data: unknown, ctx: ExecutionContext): User => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;
  }
);
```

#### 🔍 Code Walkthrough: How It Works

```typescript
// createParamDecorator creates a custom parameter decorator
import { createParamDecorator, ExecutionContext } from '@nestjs/common';

export const CurrentUser = createParamDecorator(
  // data: Any value passed to the decorator, e.g., @CurrentUser('email')
  // ctx: ExecutionContext - access to request, response, etc.
  (data: unknown, ctx: ExecutionContext): User => {
    
    // Get the HTTP request object
    const request = ctx.switchToHttp().getRequest();
    // Why switchToHttp()? 
    // → ExecutionContext can be HTTP, WebSocket, or gRPC
    // → We need to specify we want the HTTP request
    
    // Return the user that JwtStrategy attached
    return request.user;
    // → This becomes the parameter value in the controller
  }
);
```

#### Optional: Extract Specific User Property

```typescript
// Enhanced version that can extract specific properties
export const CurrentUser = createParamDecorator(
  (data: keyof User | undefined, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    const user = request.user as User;
    
    // If a property name was passed, return just that property
    return data ? user[data] : user;
  }
);

// Usage:
@Get('my-email')
getEmail(@CurrentUser('email') email: string) {
  return { email };  // Just the email, not whole user
}

@Get('profile')
getProfile(@CurrentUser() user: User) {
  return user;  // Whole user object
}
```

#### Using the Decorator

```typescript
import { CurrentUser } from "../auth/decorators/current-user.decorator";
import { User } from "./user.entity";

@Controller("users")
export class UsersController {
  @Get("me")
  @UseGuards(JwtAuthGuard)
  getMe(@CurrentUser() user: User) {
    return user; // ✅ Type-safe! Autocomplete works!
  }

  @Get("profile")
  @UseGuards(JwtAuthGuard)
  getProfile(@CurrentUser() user: User) {
    return {
      id: user.id,        // ✅ TypeScript knows these exist
      email: user.email,  // ✅ Catches typos at compile time
    };
  }
}
```

#### With Global Guard (Cleaner!)

When using global `JwtAuthGuard`:

```typescript
@Controller("users")
export class UsersController {
  @Get("me")
  getMe(@CurrentUser() user: User) {
    // No @UseGuards needed - global guard handles it!
    return user;
  }
}
```

#### Creating a "Who Am I" Route

```typescript
// src/auth/auth.controller.ts
@Controller("auth")
export class AuthController {
  @Public()
  @Post("signup")
  signup(@Body() body: SignupDto) {
    /* ... */
  }

  @Public()
  @Post("signin")
  signin(@Body() body: SigninDto) {
    /* ... */
  }

  // No @Public() = requires authentication
  @Get("whoami")
  whoAmI(@CurrentUser() user: User) {
    return {
      id: user.id,
      email: user.email,
    };
  }
}
```

#### Testing the Flow

**Step 1: Sign In**

```http
POST http://localhost:3000/auth/signin
Content-Type: application/json

{
  "email": "test@test.com",
  "password": "password123"
}
```

Response:

```json
{
  "user": { "id": 1, "email": "test@test.com" },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Step 2: Access Protected Route**

```http
GET http://localhost:3000/auth/whoami
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Response:

```json
{
  "id": 1,
  "email": "test@test.com"
}
```

#### How JWT Flow Works

```
┌─────────────────────────────────────────────────────────────────┐
│                    JWT Authentication Flow                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. User Signs In                                               │
│     └─► AuthService validates credentials                       │
│     └─► Returns JWT token                                       │
│     └─► Client stores token (localStorage, cookie, etc.)        │
│                                                                 │
│  2. Subsequent Requests                                         │
│     └─► Client sends Authorization: Bearer <token>              │
│     └─► JwtAuthGuard validates token                            │
│     └─► JwtStrategy.validate() fetches user                     │
│     └─► User attached to request.user                           │
│                                                                 │
│  3. @CurrentUser() Decorator                                    │
│     └─► Extracts user from request.user                         │
│     └─► Returns type-safe User entity                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### ✅ Summary: Custom Parameter Decorators

| Step | What Happens |
|------|--------------|
| 1 | `@CurrentUser()` triggers `createParamDecorator` callback |
| 2 | Callback receives `ExecutionContext` |
| 3 | Extract request via `ctx.switchToHttp().getRequest()` |
| 4 | Return `request.user` (attached by JwtStrategy) |
| 5 | Returned value becomes the parameter in your method |

#### Why This Matters

- **Type Safety** - Full TypeScript support for user object
- **Clean Code** - No need to access request object directly
- **Reusable** - Use across all controllers
- **Framework Pattern** - Follows NestJS conventions

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=3178C6&center=true&vCenter=true&width=550&lines=🎬+Lecture+11.11+–+Token+Refresh+Strategy" alt="Lecture 11.11" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture covers JWT token refresh strategies for maintaining user sessions without re-authentication.

#### 🤔 Why Do Tokens Expire?

```
┌─────────────────────────────────────────────────────────────────┐
│                    THE SECURITY DILEMMA                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  If token NEVER expires:                                        │
│  ❌ Stolen token = permanent access                            │
│  ❌ User can't revoke access                                   │
│  ❌ Compromised accounts stay compromised                      │
│                                                                 │
│  If token expires QUICKLY (1 minute):                           │
│  ✅ Short attack window if stolen                              │
│  ❌ User must re-login constantly                              │
│  ❌ Terrible user experience                                   │
│                                                                 │
│  THE SOLUTION: Two types of tokens!                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### The Token Expiration Problem

```
Access Token (15 min lifetime)
        │
        ▼
   ┌────────────┐
   │  Valid     │───► Access Granted
   └────────────┘
        │
        ▼ (15 min later)
   ┌────────────┐
   │  Expired   │───► 401 Unauthorized
   └────────────┘
        │
        ▼
   User must sign in again 😕
```

#### Solution: Refresh Tokens

```
┌─────────────────────────────────────────────────────────────────┐
│                  Two-Token Strategy                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ACCESS TOKEN                  REFRESH TOKEN                    │
│  ─────────────                 ─────────────                    │
│  🏃 Short-lived (15 min)       🐢 Long-lived (7 days)           │
│  📤 Sent with every request    💾 Stored securely               │
│  📋 In Authorization header    🍪 In HttpOnly cookie            │
│  ⚡ Stateless validation       📝 Can be revoked in database    │
│                                                                 │
│  WHY TWO TOKENS?                                                │
│  ─────────────                                                  │
│  Access token stolen? 15 min max damage window                  │
│  Refresh token stolen? Revoke it in database                    │
│  User logs out? Invalidate refresh token                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 🤔 Why This Works

```
┌─────────────────────────────────────────────────────────────────┐
│                    TOKEN REFRESH ANALOGY                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Think of a gym membership:                                     │
│                                                                 │
│  ACCESS TOKEN = Day pass (given at entrance)                    │
│  → Valid for limited time                                       │
│  → No need to check database each time                          │
│  → Lost? Just wait, it expires soon                             │
│                                                                 │
│  REFRESH TOKEN = Membership card (in your wallet)               │
│  → Valid for months                                             │
│  → Can be cancelled if stolen                                   │
│  → Gets you new day passes                                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Implementing Refresh Tokens

**Step 1: Update AuthService**

```typescript
// src/auth/auth.service.ts
@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService,
    private configService: ConfigService
  ) {}

  async generateTokens(userId: number, email: string) {
    const payload = { sub: userId, email };

    // Generate both tokens in parallel for speed
    const [accessToken, refreshToken] = await Promise.all([
      this.jwtService.signAsync(payload, {
        expiresIn: "15m",  // Short lifetime
      }),
      this.jwtService.signAsync(payload, {
        secret: this.configService.get("JWT_REFRESH_SECRET"), // Different secret!
        expiresIn: "7d",   // Long lifetime
      }),
    ]);

    return { accessToken, refreshToken };
  }

  async refreshTokens(refreshToken: string) {
    try {
      // Verify with the refresh secret (not the access secret!)
      const payload = await this.jwtService.verifyAsync(refreshToken, {
        secret: this.configService.get("JWT_REFRESH_SECRET"),
      });

      // Check user still exists (might have been deleted)
      const user = await this.usersService.findOne(payload.sub);
      if (!user) {
        throw new UnauthorizedException("User not found");
      }

      // Issue fresh tokens
      return this.generateTokens(user.id, user.email);
    } catch {
      throw new UnauthorizedException("Invalid refresh token");
    }
  }
}
```

#### 🔍 Code Walkthrough: Why Each Part?

```typescript
// Why different secrets for access and refresh tokens?
secret: this.configService.get('JWT_REFRESH_SECRET')

// Security reason: If access token secret is compromised,
// attacker still can't forge refresh tokens (and vice versa).
// Defense in depth!

// Why check user still exists in refreshTokens()?
const user = await this.usersService.findOne(payload.sub);
if (!user) {
  throw new UnauthorizedException('User not found');
}
// → User might have been deleted since token was issued
// → Account might be banned/suspended
// → Database is the source of truth

// Why generate BOTH tokens on refresh?
return this.generateTokens(user.id, user.email);
// This is called "token rotation"
// → Fresh access token (expected)
// → Fresh refresh token (extra security)
// → Old refresh token becomes invalid
// → Limits damage if refresh token leaked
```

**Step 2: Add Refresh Endpoint**

```typescript
// src/auth/auth.controller.ts
@Controller("auth")
export class AuthController {
  @Public()  // No auth required - we're using the refresh token!
  @Post("refresh")
  @HttpCode(HttpStatus.OK)
  async refresh(@Body("refreshToken") refreshToken: string) {
    return this.authService.refreshTokens(refreshToken);
  }
}
```

#### Secure Refresh Token Storage

**Option 1: HttpOnly Cookie (Recommended for Web)**

```typescript
@Post('signin')
async signin(
  @Body() body: SigninDto,
  @Res({ passthrough: true }) response: Response,
) {
  const { accessToken, refreshToken } = await this.authService.signin(
    body.email,
    body.password,
  );

  // Store refresh token in HttpOnly cookie
  response.cookie('refreshToken', refreshToken, {
    httpOnly: true,         // JavaScript can't access = XSS protected
    secure: true,           // HTTPS only
    sameSite: 'strict',     // CSRF protection
    maxAge: 7 * 24 * 60 * 60 * 1000, // 7 days in ms
  });

  // Only return access token in response body
  return { accessToken };
}
```

#### 🤔 Why HttpOnly Cookie?

```
┌─────────────────────────────────────────────────────────────────┐
│                    STORAGE COMPARISON                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  localStorage:                                                  │
│  ❌ JavaScript can read it                                     │
│  ❌ XSS attack = token stolen                                  │
│  ❌ Persists across sessions                                   │
│                                                                 │
│  sessionStorage:                                                │
│  ❌ JavaScript can read it                                     │
│  ❌ XSS attack = token stolen                                  │
│  ✅ Cleared on browser close                                   │
│                                                                 │
│  HttpOnly Cookie:                                               │
│  ✅ JavaScript CANNOT read it                                  │
│  ✅ XSS attack cannot steal token                              │
│  ✅ Browser automatically sends with requests                  │
│  ⚠️  Need CSRF protection (sameSite: 'strict')                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Option 2: Secure Storage (Mobile Apps)**

- Use platform-specific secure storage
- Keychain (iOS), Keystore (Android)
- Never store in SharedPreferences/AsyncStorage

#### Token Refresh Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                    REFRESH FLOW TIMELINE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  0:00   Sign in                                                 │
│         ├─► Get access token (expires 0:15)                     │
│         └─► Get refresh token (expires day 7)                   │
│                                                                 │
│  0:05   Make API request                                        │
│         └─► Access token valid ✅                               │
│                                                                 │
│  0:16   Make API request                                        │
│         └─► Access token expired ❌                             │
│         └─► 401 Unauthorized returned                           │
│                                                                 │
│  0:16   Client detects 401                                      │
│         └─► Calls /auth/refresh with refresh token              │
│         └─► Gets new access token (expires 0:31)                │
│         └─► Gets new refresh token (expires day 8)              │
│                                                                 │
│  0:17   Retry original request                                  │
│         └─► Access token valid ✅                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### ✅ Summary: Token Lifetimes

| Token Type | Lifetime | Why |
|------------|----------|-----|
| Access Token | 15 min | Short = limited damage window |
| Refresh Token | 7 days | Long = good UX (no re-login) |

#### Why This Matters

- **Better UX** - Users don't need to re-login frequently
- **Security** - Short access token lifetime limits damage
- **Revocable** - Refresh tokens can be blacklisted in database
- **Standard Pattern** - OAuth2/OIDC compatible

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=28A745&center=true&vCenter=true&width=550&lines=🎬+Lecture+11.12+–+Role-Based+Access+Control" alt="Lecture 11.12" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture implements Role-Based Access Control (RBAC) using custom decorators and guards - a common pattern in modern NestJS applications.

#### 🤔 Why Do We Need Roles?

Authentication answers: **"Who are you?"**
Authorization answers: **"What can you do?"**

```
┌─────────────────────────────────────────────────────────────────┐
│                    AUTHENTICATION vs AUTHORIZATION              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  AUTHENTICATION (Lectures 11.1-11.10)                           │
│  ───────────────────────────────────                            │
│  "Prove you are who you claim to be"                            │
│  ✅ Valid JWT token = You're authenticated                      │
│                                                                 │
│  AUTHORIZATION (This Lecture)                                   │
│  ───────────────────────────────                                │
│  "Do you have permission for this action?"                      │
│  ✅ Authenticated + correct role = You're authorized            │
│                                                                 │
│  EXAMPLE:                                                       │
│  ─────────                                                      │
│  User with valid JWT: Can view their own profile ✅              │
│  User with valid JWT: Can delete other users? ❌ (not admin)    │
│  Admin with valid JWT: Can delete other users? ✅               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 🤔 Why Roles Instead of Permissions?

```
┌─────────────────────────────────────────────────────────────────┐
│                    PERMISSION-BASED (Complex)                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  User has: [                                                    │
│    "users.read", "users.update.self",                           │
│    "reports.read", "reports.create",                            │
│    "reports.delete.own", ...50 more                             │
│  ]                                                              │
│                                                                 │
│  ❌ Complex to manage                                           │
│  ❌ Token size grows with permissions                           │
│  ❌ Need to update every user for new features                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    ROLE-BASED (Simple) ✅                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  User has: role = "admin"                                       │
│                                                                 │
│  ✅ Simple to understand                                        │
│  ✅ Token stays small                                           │
│  ✅ Permissions defined in code, not per-user                   │
│  ✅ Add new permission? Just update RolesGuard                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Adding Roles to User Entity

```typescript
// src/users/user.entity.ts
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

export enum UserRole {
  USER = "user",
  ADMIN = "admin",
  MODERATOR = "moderator",
}

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Column()
  password: string;

  @Column({
    type: "enum",
    enum: UserRole,
    default: UserRole.USER,  // New users are regular users by default
  })
  role: UserRole;
}
```

#### Creating the @Roles() Decorator

```typescript
// src/auth/decorators/roles.decorator.ts
import { SetMetadata } from "@nestjs/common";
import { UserRole } from "../../users/user.entity";

export const ROLES_KEY = "roles";
export const Roles = (...roles: UserRole[]) => SetMetadata(ROLES_KEY, roles);
```

#### 🔍 How @Roles() Works

```typescript
// When you write:
@Roles(UserRole.ADMIN, UserRole.MODERATOR)
@Delete(':id')
deleteUser() { }

// NestJS internally does:
SetMetadata('roles', [UserRole.ADMIN, UserRole.MODERATOR])
// → Attaches { roles: ['admin', 'moderator'] } as metadata

// RolesGuard reads it:
const requiredRoles = reflector.get('roles', context.getHandler());
// → Returns ['admin', 'moderator']
```

#### Creating the Roles Guard

```typescript
// src/auth/guards/roles.guard.ts
import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";
import { Reflector } from "@nestjs/core";
import { ROLES_KEY } from "../decorators/roles.decorator";
import { UserRole } from "../../users/user.entity";

@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}

  canActivate(context: ExecutionContext): boolean {
    // Step 1: Check what roles are required for this route
    const requiredRoles = this.reflector.getAllAndOverride<UserRole[]>(
      ROLES_KEY,
      [context.getHandler(), context.getClass()]
    );

    // Step 2: No @Roles() decorator = anyone authenticated can access
    if (!requiredRoles) {
      return true;
    }

    // Step 3: Get user from request (attached by JwtStrategy)
    const { user } = context.switchToHttp().getRequest();
    
    // Step 4: Check if user's role is in the required roles
    return requiredRoles.includes(user.role);
  }
}
```

#### 🔍 Code Walkthrough: Guard Execution

```typescript
canActivate(context: ExecutionContext): boolean {
  // Why getAllAndOverride?
  const requiredRoles = this.reflector.getAllAndOverride<UserRole[]>(
    ROLES_KEY,
    [context.getHandler(), context.getClass()]
  );
  // → Checks handler (method) first, then class (controller)
  // → Method @Roles() overrides class @Roles()

  // Why return true if no requiredRoles?
  if (!requiredRoles) {
    return true;
  }
  // → No @Roles() = any authenticated user can access
  // → JwtAuthGuard already verified authentication

  // Why check includes(user.role)?
  const { user } = context.switchToHttp().getRequest();
  return requiredRoles.includes(user.role);
  // → User role must be in the list of allowed roles
  // → @Roles(ADMIN, MOD) = admin OR moderator can access
}
```

#### Using RBAC in Controllers

```typescript
import { Roles } from "../auth/decorators/roles.decorator";
import { RolesGuard } from "../auth/guards/roles.guard";
import { UserRole } from "./user.entity";

@Controller("users")
@UseGuards(JwtAuthGuard, RolesGuard)  // Both guards!
export class UsersController {
  @Get()
  @Roles(UserRole.ADMIN)  // Only admins
  findAll() {
    return this.usersService.findAll();
  }

  @Delete(":id")
  @Roles(UserRole.ADMIN)  // Only admins
  remove(@Param("id") id: string) {
    return this.usersService.remove(+id);
  }

  @Get("me")
  // No @Roles = any authenticated user
  getProfile(@CurrentUser() user: User) {
    return user;
  }
}
```

#### 🤔 Why Two Guards in Sequence?

```
┌─────────────────────────────────────────────────────────────────┐
│                    GUARD EXECUTION ORDER                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  @UseGuards(JwtAuthGuard, RolesGuard)                           │
│                                                                 │
│  1. JwtAuthGuard runs FIRST                                     │
│     └─► Validates token                                         │
│     └─► Attaches user to request                                │
│     └─► Fails? Returns 401 Unauthorized                         │
│                                                                 │
│  2. RolesGuard runs SECOND                                      │
│     └─► Reads @Roles() metadata                                 │
│     └─► Checks request.user.role                                │
│     └─► Fails? Returns 403 Forbidden                            │
│                                                                 │
│  WHY THIS ORDER MATTERS:                                        │
│  RolesGuard needs request.user to exist!                        │
│  JwtAuthGuard creates request.user.                             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Global RBAC Setup

```typescript
// src/app.module.ts
import { APP_GUARD } from "@nestjs/core";

@Module({
  providers: [
    {
      provide: APP_GUARD,
      useClass: JwtAuthGuard,  // Runs first
    },
    {
      provide: APP_GUARD,
      useClass: RolesGuard,    // Runs second
    },
  ],
})
export class AppModule {}
```

#### RBAC Flow Diagram

```
Request with JWT
      │
      ▼
┌─────────────────────────────────────┐
│         JwtAuthGuard                │
├─────────────────────────────────────┤
│ ✅ Token valid                      │
│ → User attached to request          │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│         RolesGuard                  │
├─────────────────────────────────────┤
│                                     │
│ 1. Read @Roles() metadata           │
│    └─► None? return true            │
│                                     │
│ 2. Get user.role from request       │
│    └─► 'user', 'admin', etc.        │
│                                     │
│ 3. Check: is role in required?      │
│    └─► No? return false → 403       │
│    └─► Yes? return true             │
│                                     │
└─────────────────┬───────────────────┘
                  │ Allowed
                  ▼
            Route Handler
```

#### ✅ Summary: Complete Auth Routes

| Route           | Method | Purpose           | Auth Required | Roles |
| --------------- | ------ | ----------------- | ------------- | ----- |
| `/auth/signup`  | POST   | Create new user   | ❌ Public     | -     |
| `/auth/signin`  | POST   | Authenticate user | ❌ Public     | -     |
| `/auth/refresh` | POST   | Refresh tokens    | ❌ Public     | -     |
| `/auth/whoami`  | GET    | Get current user  | ✅ Required   | Any   |
| `/users`        | GET    | List all users    | ✅ Required   | Admin |
| `/users/:id`    | DELETE | Delete user       | ✅ Required   | Admin |

#### Why This Matters

- **Fine-Grained Control** - Different permissions per role
- **Declarative** - Roles defined via decorators
- **Scalable** - Easy to add new roles
- **Composable** - Works with JwtAuthGuard
- **Secure by Default** - No @Roles = still needs authentication

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=FFC107&center=true&vCenter=true&width=600&lines=🎬+Lecture+11.13+–+Serialization+and+Response+Transformation" alt="Lecture 11.13" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture covers response serialization to ensure sensitive data like passwords never leak in API responses.

#### 🤔 Why Is This Critical?

```
┌─────────────────────────────────────────────────────────────────┐
│                    THE PROBLEM                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Your database User entity:                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ {                                                        │   │
│  │   id: 1,                                                 │   │
│  │   email: "user@example.com",                             │   │
│  │   password: "$argon2id$v=19$m=65536...",  ← 😱           │   │
│  │   role: "user",                                          │   │
│  │   createdAt: "2024-01-15",                               │   │
│  │   internalNotes: "VIP customer",          ← 😱           │   │
│  │   failedLoginAttempts: 3                  ← 😱           │   │
│  │ }                                                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  If you return the entity directly, ALL fields go to client!   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### The Problem: Exposing Sensitive Data

```typescript
// ❌ DANGEROUS: Password hash in response!
@Get('me')
getProfile(@CurrentUser() user: User) {
  return user;  // Returns entire entity including password!
}
```

Response that goes to client:

```json
{
  "id": 1,
  "email": "test@test.com",
  "password": "$argon2id$v=19$m=65536...", // 😱 PASSWORD HASH EXPOSED!
  "role": "user"
}
```

Even though it's hashed, exposing password hashes is a security risk - attackers can attempt offline brute-force attacks.

#### Solution: ClassSerializerInterceptor

**Step 1: Enable Global Serialization**

```typescript
// src/main.ts
import { ClassSerializerInterceptor } from "@nestjs/common";
import { Reflector } from "@nestjs/core";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // Enable automatic serialization using class-transformer
  app.useGlobalInterceptors(new ClassSerializerInterceptor(app.get(Reflector)));

  await app.listen(3000);
}
```

**Step 2: Use @Exclude() Decorator**

```typescript
// src/users/user.entity.ts
import { Exclude } from "class-transformer";
import { Entity, Column, PrimaryGeneratedColumn } from "typeorm";

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Exclude()  // ← Never include in responses!
  @Column()
  password: string;

  @Column({ default: "user" })
  role: string;
}
```

Now the response is safe:

```json
{
  "id": 1,
  "email": "test@test.com",
  "role": "user"
}
// ✅ No password field!
```

#### 🔍 How It Works Under the Hood

```typescript
// When your controller returns a User entity:
@Get('me')
getProfile(@CurrentUser() user: User) {
  return user;
}

// ClassSerializerInterceptor does this:
// 1. Intercepts the response
// 2. Runs class-transformer's instanceToPlain()
// 3. Checks each property for @Exclude(), @Expose(), etc.
// 4. Removes excluded properties
// 5. Returns clean JSON

// Before: { id, email, password, role }
// After:  { id, email, role }
```

#### Serialization Decorators

| Decorator      | Purpose                                 | Example |
| -------------- | --------------------------------------- | ------- |
| `@Exclude()`   | Never include in response               | Password, internal IDs |
| `@Expose()`    | Include in response (when using groups) | Selected fields |
| `@Transform()` | Transform value before serialization    | Format dates, mask data |
| `@Type()`      | Specify nested type for transformation  | Nested objects |

#### 🤔 When to Use Each Decorator

```typescript
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;  // Included by default

  @Column()
  email: string;  // Included by default

  @Exclude()  // ← Security: Never expose
  @Column()
  password: string;

  @Exclude()  // ← Privacy: Internal tracking
  @Column()
  failedLoginAttempts: number;

  @Transform(({ value }) => value.toISOString().split('T')[0])
  // ← Formatting: Convert Date to "2024-01-15"
  @Column()
  createdAt: Date;

  @Expose({ groups: ['admin'] })  // ← Conditional: Only for admins
  @Column()
  internalNotes: string;
}
```

#### Advanced: Response DTOs (Recommended for Complex Cases)

For more control, create dedicated response DTOs:

```typescript
// src/users/dto/user-response.dto.ts
import { Expose } from "class-transformer";

export class UserResponseDto {
  @Expose()
  id: number;

  @Expose()
  email: string;

  @Expose()
  role: string;

  // password not included = never exposed
  // createdAt not included = not exposed
}
```

```typescript
// src/users/users.controller.ts
import { plainToInstance } from 'class-transformer';

@Get('me')
getProfile(@CurrentUser() user: User): UserResponseDto {
  return plainToInstance(UserResponseDto, user, {
    excludeExtraneousValues: true,  // Only include @Expose() fields
  });
}
```

#### 🤔 When Entity @Exclude vs DTO?

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENTITY @Exclude()                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✅ Simple - just add decorator to entity                      │
│  ✅ Works automatically everywhere                              │
│  ⚠️  Same shape for all endpoints                              │
│  ⚠️  Can't include password in internal APIs                   │
│                                                                 │
│  BEST FOR: Simple apps, consistent responses                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    Response DTOs                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ✅ Full control per endpoint                                  │
│  ✅ Different DTOs for different contexts                      │
│  ✅ Clear API contract                                         │
│  ⚠️  More code to write                                        │
│  ⚠️  Must remember to use DTO                                  │
│                                                                 │
│  BEST FOR: Complex APIs, multiple clients                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Groups for Conditional Exposure

```typescript
// src/users/user.entity.ts
import { Expose } from "class-transformer";

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  email: string;

  @Exclude()
  @Column()
  password: string;

  @Expose({ groups: ["admin"] })  // Only visible when group='admin'
  @Column({ default: false })
  isVerified: boolean;

  @Expose({ groups: ["admin"] })
  @Column()
  lastLoginIp: string;
}
```

```typescript
// In controller - use @SerializeOptions to specify groups
@Get('admin/users')
@Roles(UserRole.ADMIN)
@SerializeOptions({ groups: ['admin'] })
findAllForAdmin() {
  return this.usersService.findAll();
  // Response includes isVerified and lastLoginIp
}

@Get('users')
findAll() {
  return this.usersService.findAll();
  // Response does NOT include isVerified or lastLoginIp
}
```

#### ✅ Summary: What Gets Serialized

| Field | Default Behavior | With @Exclude() | With @Expose({ groups }) |
|-------|-----------------|-----------------|--------------------------|
| `id` | Included | Excluded | Only if group matches |
| `email` | Included | Excluded | Only if group matches |
| `password` | Included 😱 | **Excluded** ✅ | Only if group matches |

#### Why This Matters

- **Security** - Never expose passwords or sensitive data
- **Clean API** - Consistent response shapes
- **Flexibility** - Different views for different contexts
- **Defense in Depth** - Even if code has bugs, serialization catches leaks

<br>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=6F42C1&center=true&vCenter=true&width=600&lines=🎬+Lecture+11.14+–+Testing+Authentication" alt="Lecture 11.14" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

#### What This Lecture Covers

This lecture covers unit and e2e testing strategies for JWT authentication in NestJS.

#### 🤔 Why Test Authentication Specifically?

```
┌─────────────────────────────────────────────────────────────────┐
│                    WHY AUTH TESTING IS CRITICAL                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Auth bugs are SECURITY VULNERABILITIES, not just bugs:        │
│                                                                 │
│  🐛 Bug in a CRUD endpoint:                                     │
│     → Wrong data displayed                                      │
│     → User is annoyed                                           │
│                                                                 │
│  🚨 Bug in authentication:                                      │
│     → Anyone can access any account                             │
│     → Data breach                                               │
│     → Legal liability                                           │
│     → Company reputation destroyed                              │
│                                                                 │
│  Auth is the GATEKEEPER to everything else.                     │
│  It MUST be thoroughly tested.                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### 🤔 Unit Tests vs E2E Tests

```
┌─────────────────────────────────────────────────────────────────┐
│                    TWO TYPES OF TESTS                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  UNIT TESTS (Isolated)                                          │
│  ─────────────────────                                          │
│  Test: AuthService.signup()                                     │
│  Mock: UsersService, JwtService                                 │
│  Why:  Fast, focused, catch logic errors                        │
│                                                                 │
│  "Does the signup method hash passwords correctly?"             │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  E2E TESTS (Integration)                                        │
│  ─────────────────────                                          │
│  Test: POST /auth/signup endpoint                               │
│  Use:  Real database, real everything                           │
│  Why:  Catch integration issues, realistic scenarios            │
│                                                                 │
│  "Does the whole signup flow work from HTTP to database?"       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Unit Testing AuthService

```typescript
// src/auth/auth.service.spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { JwtService } from "@nestjs/jwt";
import { AuthService } from "./auth.service";
import { UsersService } from "../users/users.service";
import { ConflictException, UnauthorizedException } from "@nestjs/common";

describe("AuthService", () => {
  let service: AuthService;
  let usersService: Partial<UsersService>;
  let jwtService: Partial<JwtService>;

  beforeEach(async () => {
    // Create a simple in-memory "database"
    const users: any[] = [];

    // Mock UsersService - simulates database operations
    usersService = {
      findByEmail: (email: string) =>
        Promise.resolve(users.find((u) => u.email === email)),
      create: (email: string, password: string) => {
        const user = { id: users.length + 1, email, password };
        users.push(user);
        return Promise.resolve(user);
      },
    };

    // Mock JwtService - we don't need real tokens for unit tests
    jwtService = {
      signAsync: jest.fn().mockResolvedValue("mock-token"),
    };

    // Build test module with mocked dependencies
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        AuthService,  // The real service we're testing
        { provide: UsersService, useValue: usersService },  // Mock
        { provide: JwtService, useValue: jwtService },      // Mock
      ],
    }).compile();

    service = module.get<AuthService>(AuthService);
  });

  it("should be defined", () => {
    expect(service).toBeDefined();
  });

  describe("signup", () => {
    it("creates a new user with hashed password", async () => {
      const result = await service.signup("test@test.com", "password");

      expect(result.user.email).toBe("test@test.com");
      expect(result.accessToken).toBe("mock-token");
      // Password should be hashed, not plain text
      expect(result.user.password).not.toBe("password");
    });

    it("throws ConflictException if email in use", async () => {
      // First signup succeeds
      await service.signup("test@test.com", "password");

      // Second signup with same email should fail
      await expect(service.signup("test@test.com", "password")).rejects.toThrow(
        ConflictException
      );
    });
  });

  describe("signin", () => {
    it("throws UnauthorizedException for invalid email", async () => {
      // No user exists, should fail
      await expect(
        service.signin("wrong@test.com", "password")
      ).rejects.toThrow(UnauthorizedException);
    });

    it("throws UnauthorizedException for wrong password", async () => {
      // Create a user first
      await service.signup("test@test.com", "correctpassword");

      // Try to sign in with wrong password
      await expect(
        service.signin("test@test.com", "wrongpassword")
      ).rejects.toThrow(UnauthorizedException);
    });

    it("returns token for valid credentials", async () => {
      // Create a user
      await service.signup("test@test.com", "password123");

      // Sign in with correct credentials
      const result = await service.signin("test@test.com", "password123");
      
      expect(result.accessToken).toBe("mock-token");
      expect(result.user.email).toBe("test@test.com");
    });
  });
});
```

#### 🔍 Why Mock Dependencies?

```typescript
// Why do we mock UsersService and JwtService?

// 1. ISOLATION - Test only AuthService logic
//    If test fails, we know AuthService is the problem
//    Not the database, not JWT library

// 2. SPEED - No database = instant tests
//    Real DB: 500ms per test
//    Mocked:  5ms per test

// 3. CONTROL - Simulate any scenario
//    Want to test "what if user already exists"?
//    Just put a user in the mock array!

// 4. NO SIDE EFFECTS - Each test starts fresh
//    Real DB might have leftover data
//    Mock resets every beforeEach()
```

#### E2E Testing Auth Endpoints

```typescript
// test/auth.e2e-spec.ts
import { Test, TestingModule } from "@nestjs/testing";
import { INestApplication, ValidationPipe } from "@nestjs/common";
import * as request from "supertest";
import { AppModule } from "../src/app.module";

describe("Auth (e2e)", () => {
  let app: INestApplication;

  beforeEach(async () => {
    // Create real NestJS application
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],  // Use real AppModule!
    }).compile();

    app = moduleFixture.createNestApplication();
    // Apply same pipes as production
    app.useGlobalPipes(new ValidationPipe({ whitelist: true }));
    await app.init();
  });

  afterEach(async () => {
    await app.close();
  });

  describe("/auth/signup (POST)", () => {
    it("should create a new user", () => {
      return request(app.getHttpServer())
        .post("/auth/signup")
        .send({ email: "test@test.com", password: "password123" })
        .expect(201)
        .expect((res) => {
          expect(res.body.accessToken).toBeDefined();
          expect(res.body.user.email).toBe("test@test.com");
          // CRITICAL: Password must NOT be in response!
          expect(res.body.user.password).toBeUndefined();
        });
    });

    it("should reject invalid email", () => {
      return request(app.getHttpServer())
        .post("/auth/signup")
        .send({ email: "invalid", password: "password123" })
        .expect(400);  // ValidationPipe rejects
    });

    it("should reject short password", () => {
      return request(app.getHttpServer())
        .post("/auth/signup")
        .send({ email: "test@test.com", password: "123" })
        .expect(400);
    });
  });

  describe("/auth/whoami (GET)", () => {
    it("should return current user when authenticated", async () => {
      // Step 1: Sign up to get a token
      const signupRes = await request(app.getHttpServer())
        .post("/auth/signup")
        .send({ email: "test@test.com", password: "password123" });

      const token = signupRes.body.accessToken;

      // Step 2: Access protected route with token
      return request(app.getHttpServer())
        .get("/auth/whoami")
        .set("Authorization", `Bearer ${token}`)
        .expect(200)
        .expect((res) => {
          expect(res.body.email).toBe("test@test.com");
        });
    });

    it("should return 401 without token", () => {
      return request(app.getHttpServer())
        .get("/auth/whoami")
        .expect(401);  // No token = unauthorized
    });

    it("should return 401 with invalid token", () => {
      return request(app.getHttpServer())
        .get("/auth/whoami")
        .set("Authorization", "Bearer invalid-token-here")
        .expect(401);  // Bad token = unauthorized
    });
  });
});
```

#### 🤔 What to Test in Auth?

```
┌─────────────────────────────────────────────────────────────────┐
│                    AUTH TEST CHECKLIST                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SIGNUP:                                                        │
│  ✅ Creates user with valid data                               │
│  ✅ Rejects invalid email format                               │
│  ✅ Rejects password too short                                 │
│  ✅ Rejects duplicate email                                    │
│  ✅ Returns token (not password!)                              │
│  ✅ Password is hashed in database                             │
│                                                                 │
│  SIGNIN:                                                        │
│  ✅ Returns token for valid credentials                        │
│  ✅ Rejects non-existent email                                 │
│  ✅ Rejects wrong password                                     │
│  ✅ Same error message for both (no enumeration!)              │
│                                                                 │
│  PROTECTED ROUTES:                                              │
│  ✅ 401 when no token provided                                 │
│  ✅ 401 when token is invalid/expired                          │
│  ✅ 200 when token is valid                                    │
│  ✅ Correct user data returned                                 │
│                                                                 │
│  ROLES:                                                         │
│  ✅ Admin can access admin routes                              │
│  ✅ User cannot access admin routes (403)                      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Mocking JwtAuthGuard in Tests

Sometimes you want to test a controller without real auth:

```typescript
// For testing protected routes without real auth
const mockJwtAuthGuard = {
  canActivate: (context: ExecutionContext) => {
    const req = context.switchToHttp().getRequest();
    // Attach a fake user
    req.user = { id: 1, email: "test@test.com", role: "user" };
    return true;  // Always allow
  },
};

const module = await Test.createTestingModule({
  imports: [AppModule],
})
  .overrideGuard(JwtAuthGuard)
  .useValue(mockJwtAuthGuard)  // Replace real guard with mock
  .compile();

// Now all protected routes work without a real token!
```

#### 🤔 When to Mock the Guard?

```
┌─────────────────────────────────────────────────────────────────┐
│                    MOCK GUARD OR NOT?                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  TEST AUTH ITSELF? → DON'T mock the guard                      │
│  → You want to verify the guard actually works                  │
│                                                                 │
│  TEST OTHER FEATURES? → DO mock the guard                      │
│  → ReportsController test doesn't care about auth               │
│  → Just need a user attached to request                         │
│  → Faster tests, simpler setup                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### ✅ Summary: Test Coverage Goals

| Component   | Coverage Target | Key Tests                         |
| ----------- | --------------- | --------------------------------- |
| AuthService | 90%+            | signup, signin, password hashing  |
| JwtStrategy | 80%+            | validate(), user lookup           |
| Guards      | 100%            | canActivate(), @Public() handling |
| Controllers | 85%+            | All endpoints, error cases        |

#### Why This Matters

- **Confidence** - Auth is critical, must be well-tested
- **Regression Prevention** - Catch breaking changes early
- **Documentation** - Tests describe expected behavior
- **Security Assurance** - Prove auth works correctly
- **CI/CD Ready** - Automated testing in pipelines

<br>

---

## Section 11 Summary

### What We Built

A complete, production-ready JWT authentication system following NestJS 11+ and OWASP 2024+ best practices:

```
┌─────────────────────────────────────────────────────────────────┐
│              JWT Authentication System (2026)                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PUBLIC ROUTES (@Public decorator):                             │
│  ├── POST /auth/signup    → Create user, return tokens         │
│  ├── POST /auth/signin    → Verify user, return tokens         │
│  └── POST /auth/refresh   → Exchange refresh for new access    │
│                                                                 │
│  PROTECTED ROUTES (JwtAuthGuard - default):                     │
│  ├── GET  /auth/whoami    → Get current user (@CurrentUser)    │
│  └── All other routes     → Require valid access token         │
│                                                                 │
│  ROLE-PROTECTED ROUTES (@Roles decorator):                      │
│  └── Admin-only endpoints → Require specific roles             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

````

### Key Concepts Covered

| Lecture | Topic | Key Takeaway |
|---------|-------|--------------|
| 11.1 | Authentication Overview | JWT vs Sessions - stateless auth with Bearer tokens |
| 11.2 | Setting Up Auth Module | `@nestjs/jwt`, `@nestjs/passport`, `passport-jwt` |
| 11.3 | Signup Functionality | Hash password, create user, return tokens |
| 11.4 | Password Hashing Theory | Argon2id - OWASP 2024+ recommended algorithm |
| 11.5 | Password Hashing Implementation | Node 21+ native crypto or argon2 package |
| 11.6 | JWT Token Generation | Access + refresh token pattern |
| 11.7 | Sign In | Verify credentials, return token pair |
| 11.8 | JWT Strategy | Passport strategy extracts and validates JWT |
| 11.9 | JWT Auth Guard | Global guard with @Public() opt-out |
| 11.10 | CurrentUser Decorator | Extract user from request.user |
| 11.11 | Token Refresh | Secure token rotation pattern |
| 11.12 | Role-Based Access Control | @Roles() decorator with RolesGuard |
| 11.13 | Serialization | ClassSerializerInterceptor, @Exclude() |
| 11.14 | Testing Authentication | Unit and e2e tests for auth |

### Files Created

| File | Purpose |
|------|---------|
| `src/auth/auth.module.ts` | Auth module with JWT configuration |
| `src/auth/auth.service.ts` | Signup, signin, refresh, password hashing |
| `src/auth/auth.controller.ts` | Auth endpoints |
| `src/auth/strategies/jwt.strategy.ts` | Passport JWT strategy |
| `src/auth/guards/jwt-auth.guard.ts` | Global authentication guard |
| `src/auth/guards/roles.guard.ts` | Role-based access control |
| `src/auth/decorators/current-user.decorator.ts` | Extract current user |
| `src/auth/decorators/public.decorator.ts` | Mark routes as public |
| `src/auth/decorators/roles.decorator.ts` | Assign required roles |

### Package Dependencies

```json
{
  "dependencies": {
    "@nestjs/jwt": "^11.0.0",
    "@nestjs/passport": "^11.0.0",
    "passport": "^0.7.0",
    "passport-jwt": "^4.0.1",
    "argon2": "^0.41.0"
  },
  "devDependencies": {
    "@types/passport-jwt": "^4.0.1"
  }
}
````

### Environment Variables

```env
JWT_SECRET=your-super-secret-jwt-key-change-in-production
JWT_EXPIRES_IN=15m
JWT_REFRESH_SECRET=your-super-secret-refresh-key-change-in-production
JWT_REFRESH_EXPIRES_IN=7d
```

### Security Best Practices Implemented

| Practice          | Implementation                                |
| ----------------- | --------------------------------------------- |
| Password Hashing  | Argon2id with OWASP parameters                |
| Token Security    | Short-lived access tokens (15min)             |
| Token Refresh     | Secure rotation with separate secret          |
| Global Protection | JwtAuthGuard applied to all routes by default |
| Role-Based Access | RolesGuard for fine-grained permissions       |
| Response Security | Sensitive fields excluded via serialization   |

### Quick Reference

**Protect a route (default behavior):**

```typescript
@Get('/protected')
protectedRoute(@CurrentUser() user: User) {
  return user;
}
```

**Make a route public:**

```typescript
@Public()
@Get('/public')
publicRoute() {
  return 'Anyone can access';
}
```

**Require specific roles:**

```typescript
@Roles(Role.Admin)
@Get('/admin')
adminOnly(@CurrentUser() user: User) {
  return 'Admin access granted';
}
```

**Get current user in any protected route:**

```typescript
@Get('/profile')
getProfile(@CurrentUser() user: User) {
  return user;
}
```

### Migration from Session-Based Auth

If migrating from `cookie-session` to JWT:

| Old (Sessions)                     | New (JWT)                              |
| ---------------------------------- | -------------------------------------- |
| `cookie-session` middleware        | `@nestjs/jwt` + `passport-jwt`         |
| `request.session.userId`           | `request.user` (from JWT payload)      |
| `scrypt` for password hashing      | `argon2id`                             |
| CurrentUserInterceptor + Decorator | Simple `@CurrentUser()` decorator      |
| Session cookie                     | `Authorization: Bearer <token>` header |

### Next Steps

With authentication complete, you can:

1. Add more protected resources (reports, admin features)
2. Implement permission-based access (beyond roles)
3. Add OAuth/social login providers
4. Implement password reset flow
5. Add two-factor authentication (2FA)

<br>

---

<!-- End of Section 11 -->
