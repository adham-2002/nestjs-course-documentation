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

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=24&pause=1000&color=E0234E&center=true&vCenter=true&width=500&lines=🎬+Lecture+2.1+–+Project+Setup" alt="Lecture 2.1" />
</p>

<p align="center">━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</p>
<!-- ══════════════════════════════════════════════════════════════════════════ -->

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

## Summary

This section covered the foundational concepts of NestJS:

1. **Project Setup** - Understanding dependencies and their roles
2. **TypeScript Configuration** - Enabling decorators for NestJS
3. **Controllers** - Handling and routing incoming requests
4. **Modules** - Organizing application components
5. **File Conventions** - Maintaining clean project structure
6. **Routing** - Defining API endpoints with decorators

These basics form the foundation for building more complex NestJS applications.
