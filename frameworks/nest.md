# 🚀 NestJS

This repository defines a base structure for **NestJS** projects within the Fidooo ecosystem. It's designed to maximize scalability, maintainability, and development velocity using modern NestJS patterns and tools.

## 📋 Table of Contents

- [Directory Structure](#-directory-structure)
- [Technologies and Rationale](#-technologies-and-rationale)
  - [Database → TypeORM](#-typeorm)
  - [Validation → class-validator + class-transformer](#-class-validator--class-transformer)
  - [API Documentation → Swagger](#-swagger)
  - [Authentication → Passport + JWT](#-passport--jwt)
  - [Configuration → ConfigModule](#-configmodule)
  - [Testing → Jest](#-jest)
  - [Logging → Winston](#-winston)
  - [Caching → Redis](#-redis)
  - [Queue Management → Bull](#-bull)
  - [File Upload → Multer](#-multer)
  - [Rate Limiting → Throttler](#-throttler)
  - [Health Checks → Terminus](#-terminus)

---

## 📁 Directory Structure

```bash
/
├── 📄 package.json                    # Dependencies and scripts
├── 📄 tsconfig.json                   # TypeScript configuration
├── 📄 nest-cli.json                   # NestJS CLI configuration
├── 📄 Dockerfile                      # Docker configuration
├── 📄 jest.setup.ts                   # Jest configuration
├── 📄 .eslintrc.js                    # ESLint rules
├── 📄 .prettierrc                     # Prettier configuration
├── 📄 deploy_instructions.txt         # Deployment instructions
├── 📄 env-script.js                   # Environment variables script
│
├── 📁 src/                            # Main source code
│   ├── 📄 main.ts                     # Application entry point
│   ├── 📄 app.module.ts               # Root application module
│   │
│   ├── 📁 common/                     # Shared code between modules
│   │   ├── 📁 constants/              # Global constants
│   │   ├── 📁 decorators/             # Custom decorators
│   │   ├── 📁 enums/                  # Shared enumerations
│   │   ├── 📁 exceptions/             # Global exception filters
│   │   ├── 📁 factories/              # Factories for complex objects
│   │   ├── 📁 guards/                 # Authentication/authorization guards
│   │   ├── 📁 helpers/                # Utility functions
│   │   ├── 📁 interceptors/           # Request/response interceptors
│   │   ├── 📁 interfaces/             # Shared interfaces
│   │   ├── 📁 middlewares/            # Custom middlewares
│   │   ├── 📁 pipes/                  # Validation pipes
│   │   ├── 📁 schemas/                # Database schemas
│   │   ├── 📁 services/               # Shared services
│   │   ├── 📁 swagger/                # API documentation configuration
│   │   └── 📁 validators/             # Custom validators
│   │
│   ├── 📁 config/                     # Application configuration
│   │   ├── 📄 config.service.ts       # Configuration service
│   │   ├── 📄 config.module.ts        # Configuration module
│   │   ├── 📄 validation.ts           # Configuration validation
│   │   └── 📄 app-options.constants.ts # Application options
│   │
│   ├── 📁 helpers/                    # Application-specific helpers
│   │   └── 📄 retry-helper.ts         # Retry helper
│   │
│   └── 📁 modules/                    # Application modules
│       ├── 📁 auth/                   # Authentication and authorization
│       │   ├── 📄 auth.controller.ts  # Authentication controller
│       │   ├── 📄 auth.service.ts     # Authentication service
│       │   ├── 📄 auth.module.ts      # Authentication module
│       │   ├── 📁 dto/                # Data Transfer Objects
│       │   ├── 📁 schemas/            # Authentication schemas
│       │   ├── 📁 guards/             # Auth-specific guards
│       │   ├── 📁 strategies/         # Passport strategies
│       │   └── 📁 interfaces/         # Auth interfaces
│       │
│       ├── 📁 users/                  # User management
│       │   ├── 📄 users.controller.ts # Users controller
│       │   ├── 📄 users.service.ts    # Users service
│       │   ├── 📄 users.module.ts     # Users module
│       │   ├── 📁 dto/                # User DTOs
│       │   ├── 📁 schemas/            # User schemas
│       │   ├── 📁 repositories/       # User repositories
│       │   ├── 📁 helpers/            # User helpers
│       │   └── 📁 decorators/         # User decorators
│       │
│       ├── 📁 notifications/          # Notification system
│       │   ├── 📄 notifications.controller.ts
│       │   ├── 📄 notifications.service.ts
│       │   ├── 📄 notifications.module.ts
│       │   ├── 📁 dto/                # Notification DTOs
│       │   ├── 📁 schemas/            # Notification schemas
│       │   ├── 📁 providers/          # Notification providers (email, SMS, push)
│       │   └── 📁 templates/          # Notification templates
│       │
│       ├── 📁 files/                  # File management
│       │   ├── 📄 files.controller.ts # Files controller
│       │   ├── 📄 files.service.ts    # Files service
│       │   ├── 📄 files.module.ts     # Files module
│       │   ├── 📁 dto/                # File DTOs
│       │   ├── 📁 schemas/            # File schemas
│       │   ├── 📁 storage/            # Storage providers (local, S3, etc.)
│       │   └── 📁 validators/         # File validators
│       │
│       ├── 📁 analytics/              # Analytics and reporting
│       │   ├── 📄 analytics.controller.ts
│       │   ├── 📄 analytics.service.ts
│       │   ├── 📄 analytics.module.ts
│       │   ├── 📁 dto/                # Analytics DTOs
│       │   ├── 📁 schemas/            # Analytics schemas
│       │   ├── 📁 reports/            # Report generators
│       │   └── 📁 metrics/            # Metrics collectors
│       │
│       ├── 📁 webhooks/               # Webhook management
│       │   ├── 📄 webhooks.controller.ts
│       │   ├── 📄 webhooks.service.ts
│       │   ├── 📄 webhooks.module.ts
│       │   ├── 📁 dto/                # Webhook DTOs
│       │   ├── 📁 schemas/            # Webhook schemas
│       │   ├── 📁 providers/          # Webhook providers
│       │   └── 📁 validators/         # Webhook validators
│       │
│       ├── 📁 settings/               # Application settings
│       │   ├── 📄 settings.controller.ts
│       │   ├── 📄 settings.service.ts
│       │   ├── 📄 settings.module.ts
│       │   ├── 📁 dto/                # Settings DTOs
│       │   ├── 📁 schemas/            # Settings schemas
│       │   ├── 📁 repositories/       # Settings repositories
│       │   └── 📁 validators/         # Settings validators
│       │
│       ├── 📁 events/                 # Event system
│       │   ├── 📄 events.module.ts
│       │   ├── 📁 services/           # Event services
│       │   ├── 📁 handlers/           # Event handlers
│       │   ├── 📁 emitters/           # Event emitters
│       │   └── 📁 enums/              # Event enumerations
│       │
│       ├── 📁 health/                 # Health checks
│       │   ├── 📄 health.controller.ts
│       │   ├── 📄 health.module.ts
│       │   ├── 📁 indicators/         # Health indicators
│       │   └── 📁 services/           # Health services
│       │
│       └── 📁 [feature]/              # Feature-specific modules
│           ├── 📄 [feature].controller.ts
│           ├── 📄 [feature].service.ts
│           ├── 📄 [feature].module.ts
│           ├── 📁 dto/                # Feature DTOs
│           ├── 📁 schemas/            # Feature schemas
│           ├── 📁 repositories/       # Feature repositories
│           ├── 📁 helpers/            # Feature helpers
│           ├── 📁 interfaces/         # Feature interfaces
│           ├── 📁 enums/              # Feature enumerations
│           └── 📁 constants/          # Feature constants
│
├── 📁 tests/                          # Application tests
│   ├── 📁 e2e/                        # End-to-end tests
│   ├── 📁 unit/                       # Unit tests
│   ├── 📁 integration/                # Integration tests
│   ├── 📁 mocks/                      # Test mocks
│   └── 📁 fixtures/                   # Test fixtures
│
└── 📁 scripts/                        # Migration and utility scripts
    ├── 📄 README.md                   # Scripts documentation
    ├── 📄 seed.ts                     # Database seeding
    ├── 📄 migrate.ts                  # Database migration
    ├── 📁 setup/                      # Setup scripts
    ├── 📁 maintenance/                # Maintenance scripts
    └── 📁 deployment/                 # Deployment scripts
```

### Module Structure Pattern

Each module follows a consistent structure:

```bash
📁 [module-name]/
├── 📄 [module-name].controller.ts     # HTTP endpoints
├── 📄 [module-name].service.ts        # Business logic
├── 📄 [module-name].module.ts         # Module definition
├── 📁 dto/                           # Data Transfer Objects
│   ├── 📄 create-[entity].dto.ts
│   ├── 📄 update-[entity].dto.ts
│   └── 📄 query-[entity].dto.ts
├── 📁 schemas/                       # Database entities
│   └── 📄 [entity].schema.ts
├── 📁 repositories/                  # Data access layer
│   └── 📄 [entity].repository.ts
├── 📁 interfaces/                    # TypeScript interfaces
│   └── 📄 [entity].interface.ts
├── 📁 enums/                         # Enumerations
│   └── 📄 [entity].enum.ts
├── 📁 constants/                     # Module constants
│   └── 📄 [entity].constants.ts
├── 📁 helpers/                       # Utility functions
│   └── 📄 [entity].helper.ts
├── 📁 validators/                    # Custom validators
│   └── 📄 [entity].validator.ts
└── 📁 decorators/                    # Custom decorators
    └── 📄 [entity].decorator.ts
```

---

## 🧰 Technologies and Rationale

### ✅ TypeORM

- **Type-safe database operations** with excellent TypeScript integration.
- **Multiple database support** (PostgreSQL, MySQL, SQLite, MongoDB).
- **Migration system** for database schema management.
- **Repository pattern** for clean data access layer.
- **Query builder** for complex database operations.
- **Perfect for NestJS** with built-in integration.
- Alternatives: Prisma, Sequelize, Mongoose.

### ✅ class-validator + class-transformer

- **Declarative validation** using decorators and class-based schemas.
- **Automatic transformation** of incoming data to DTOs.
- **Type-safe validation** with excellent error messages.
- **Custom validators** for complex business rules.
- **Perfect integration** with NestJS pipes and DTOs.
- **Reduces boilerplate** compared to manual validation.
- Alternatives: Joi, Yup, Zod.

### ✅ Swagger

- **Automatic API documentation** generation from decorators.
- **Interactive API explorer** for testing endpoints.
- **Type-safe documentation** with TypeScript integration.
- **Perfect for team collaboration** and client integration.
- **OpenAPI 3.0 specification** compliance.
- **Easy to maintain** with decorator-based approach.
- Alternatives: Redoc, Postman Collections.

### ✅ Passport + JWT

- **Flexible authentication** with multiple strategies.
- **JWT token-based** authentication for stateless APIs.
- **Multiple providers** support (Google, Facebook, etc.).
- **Role-based access control** with guards.
- **Perfect for microservices** architecture.
- **Industry standard** authentication solution.
- Alternatives: Auth0, Firebase Auth, Supabase Auth.

### ✅ ConfigModule

- **Environment-based configuration** management.
- **Type-safe configuration** with validation.
- **Multiple environment** support (dev, staging, prod).
- **Secret management** integration.
- **Perfect for** different deployment environments.
- **Reduces configuration errors** with validation.
- Alternatives: dotenv, convict, nconf.

### ✅ Jest

- **Comprehensive testing framework** for NestJS applications.
- **Unit, integration, and e2e tests** in one framework.
- **Perfect for** testing controllers, services, and modules.
- **Fast execution** with excellent debugging capabilities.
- **Mocking support** for dependencies and external services.
- **Coverage reporting** for code quality metrics.
- Alternatives: Mocha, Vitest, Ava.

### ✅ Winston

- **Structured logging** with multiple transport support.
- **Log levels** and formatting for different environments.
- **Performance monitoring** and error tracking.
- **Perfect for** production debugging and monitoring.
- **Customizable** log formats and destinations.
- **Integration** with monitoring services.
- Alternatives: Pino, Bunyan, Morgan.

### ✅ Redis

- **High-performance caching** for improved response times.
- **Session storage** for distributed applications.
- **Rate limiting** and throttling support.
- **Perfect for** microservices architecture.
- **Pub/Sub messaging** for real-time features.
- **Data structures** for complex caching scenarios.
- Alternatives: Memcached, Hazelcast, In-Memory.

### ✅ Bull

- **Queue management** for background job processing.
- **Job scheduling** and retry mechanisms.
- **Progress tracking** and monitoring.
- **Perfect for** heavy computational tasks.
- **Redis-based** with excellent performance.
- **Dashboard** for queue monitoring.
- Alternatives: Agenda, Bee-Queue, Sidekiq.

### ✅ Multer

- **File upload handling** with streaming support.
- **Multiple file formats** and size limits.
- **File validation** and filtering.
- **Perfect for** user-generated content.
- **Memory and disk** storage options.
- **Integration** with cloud storage providers.
- Alternatives: Busboy, formidable, multer-s3.

### ✅ Throttler

- **Rate limiting** to prevent API abuse.
- **Flexible throttling** strategies (IP, user, endpoint).
- **Storage backends** (Redis, Memory, Database).
- **Perfect for** public APIs and security.
- **Customizable** rate limit rules.
- **Integration** with authentication.
- Alternatives: express-rate-limit, rate-limiter-flexible.

### ✅ Terminus

- **Health check endpoints** for monitoring.
- **Database connectivity** checks.
- **External service** health monitoring.
- **Perfect for** container orchestration.
- **Custom health indicators** for business logic.
- **Integration** with monitoring tools.
- Alternatives: health-check, nestjs-health.

---

## 🎯 Key Benefits

- **Modular Architecture**: Scalable and maintainable codebase with NestJS modules
- **Type Safety**: Full TypeScript support with validation and transformation
- **API Documentation**: Automatic Swagger documentation generation
- **Database Integration**: Type-safe database operations with TypeORM
- **Authentication**: Flexible authentication with Passport and JWT
- **Testing**: Comprehensive testing framework with Jest
- **Configuration**: Environment-based configuration management
- **Logging**: Structured logging with Winston for monitoring
- **Caching**: High-performance caching with Redis
- **Queue Management**: Background job processing with Bull
- **Health Checks**: Monitoring endpoints with Terminus
- **Rate Limiting**: API protection with Throttler
- **File Upload**: Secure file handling with Multer

This setup enables Fidooo to have a solid, modular, and scalable foundation for backend applications. The architecture promotes clean separation of concerns, testability, and maintainability while leveraging the best NestJS ecosystem tools. 