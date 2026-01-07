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

<br>
