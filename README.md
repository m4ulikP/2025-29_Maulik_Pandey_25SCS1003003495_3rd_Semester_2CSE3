# FlyRank AI — Back-End AI Engineering Internship

## Multi-Tenant Usage Metering & Billing Engine

This repository contains my capstone project completed during my **8-week Back-End AI Engineering Internship at FlyRank AI / FlyRank Corp.**

The project focuses on building a reliable backend system for **multi-tenant usage metering, subscription quota management, usage-based billing, idempotent request processing, and Stripe integration** for an AI-oriented application.

---

## 👤 Student Details

| Field | Details |
|---|---|
| **Name** | Maulik Pandey |
| **Roll Number** | 25SCS1003003495 |
| **University** | IILM University |
| **Programme** | B.Tech Computer Science & Engineering (AI/ML) |
| **Batch** | 2025–2029 |
| **Internship Organization** | FlyRank AI / FlyRank Corp. |
| **Role** | Back-End AI Engineering Intern |
| **Duration** | 8 Weeks |
| **Start Date** | 1 July 2026 |
| **End Date** | 26 August 2026 |

---

## 🏢 About FlyRank AI

**FlyRank AI** is an AI-native organic growth and search visibility platform focused on helping organizations improve their visibility across modern search and AI-driven discovery environments.

The internship provided practical exposure to backend engineering for AI-powered products, including API development, usage tracking, billing systems, databases, integrations, testing, and reliability engineering.

**Website:** https://flyrank.ai/

---

# 🚀 Capstone Project

## Multi-Tenant Usage Metering & Billing Engine

The capstone project is a backend service designed to provide reliable **usage metering and billing infrastructure** for a multi-tenant AI-oriented application.

AI applications can generate variable usage depending on API requests, token consumption, subscription plans, and other billable operations. The system therefore needs to accurately measure usage, enforce quotas, calculate charges, and handle payment-related events without incorrectly charging customers.

This project addresses these requirements through a backend architecture centered around:

- Multi-tenant usage tracking
- API usage metering
- AI token usage tracking
- Subscription plans and quotas
- Usage-based billing
- Idempotent request processing
- Database transactions
- Stripe integration
- Webhook processing
- Subscription synchronization
- Reconciliation
- Automated testing

---

## 🎯 Objectives

The primary objectives of the project were:

- Build a backend system capable of tracking usage across multiple tenants.
- Meter API and AI-related usage accurately.
- Enforce subscription-based usage quotas.
- Calculate usage-based billing reliably.
- Prevent duplicate billing caused by retries or repeated requests.
- Integrate Stripe for checkout and subscription management.
- Process Stripe webhooks securely and reliably.
- Maintain consistent subscription and billing state.
- Provide automated tests for important business and edge cases.
- Build a maintainable backend architecture suitable for further development.

---

# ⭐ Key Features

## 1. Multi-Tenant Usage Metering

The system tracks billable usage while keeping tenant-level data separated.

Usage records can be associated with the appropriate tenant and billing context, allowing the backend to calculate usage and charges independently for different customers.

---

## 2. API & AI Usage Tracking

The backend supports metering of application usage relevant to AI workloads.

This includes tracking usage information such as API requests and token-based consumption where applicable.

The metering layer provides the foundation for quota enforcement and billing.

---

## 3. Subscription & Quota Management

The system associates tenants with subscription plans and applies the corresponding usage limits.

Quota enforcement helps prevent customers from exceeding the usage permitted by their subscription.

The backend must handle quota boundaries carefully so that usage and billing remain consistent.

---

## 4. Usage-Based Billing

The project implements usage-based billing logic for billable operations.

The billing system is designed to produce deterministic calculations rather than relying on floating-point arithmetic for monetary values.

This is important because financial calculations require predictable and accurate results.

---

## 5. Idempotency

Idempotency is used to prevent the same billable request from being processed multiple times.

This is particularly important for distributed systems because clients may retry requests when they do not immediately receive a response.

The backend can use an idempotency key and request information to determine whether a request has already been processed.

This helps prevent:

- Duplicate usage records
- Duplicate quota consumption
- Duplicate charges
- Inconsistent billing state

---

## 6. Stripe Integration

Stripe is integrated into the backend for payment and subscription-related functionality.

The integration includes functionality such as:

- Stripe Checkout
- Subscription handling
- Webhook processing
- Webhook signature verification
- Replay protection
- Subscription synchronization

Stripe webhook events are treated carefully because payment systems can deliver events more than once or in an unexpected order.

---

## 7. Webhook Reliability

Webhook processing includes safeguards intended to prevent invalid or repeated events from corrupting application state.

Important reliability considerations include:

- Signature verification
- Event identification
- Replay protection
- Safe database updates
- Subscription synchronization

---

## 8. Reconciliation

Reconciliation provides a mechanism for checking and correcting inconsistencies between application billing/subscription state and the external payment system where applicable.

This adds an additional reliability layer beyond normal request and webhook processing.

---

# 🏗️ System Architecture

The project follows a backend service architecture where API requests pass through validation and business logic before interacting with persistent storage.

```text
                    ┌─────────────────────┐
                    │   API Consumer      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Express.js API      │
                    │ Routes / Controllers│
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Validation &        │
                    │ Middleware          │
                    └──────────┬──────────┘
                               │
                               ▼
              ┌────────────────────────────────┐
              │      Business Logic Layer      │
              │                                │
              │  • Usage Metering              │
              │  • Quota Enforcement           │
              │  • Billing                     │
              │  • Idempotency                 │
              │  • Subscription Management     │
              └────────────────┬───────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Repository / Data   │
                    │ Access Layer        │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │    PostgreSQL       │
                    └─────────────────────┘


                    External Payment System
                              │
                              ▼
                         ┌─────────┐
                         │ Stripe  │
                         └────┬────┘
                              │
                         Webhooks
                              │
                              ▼
                    ┌─────────────────────┐
                    │ Signature Validation│
                    │ & Replay Protection │
                    └──────────┬──────────┘
                               │
                               ▼
                    Subscription Sync
```

## 🛠️ Technology Stack

The project uses a backend-focused technology stack.

- **Backend**: TypeScript, Node.js, Express.js
- **Database**: PostgreSQL
- **Database / Query Layer**: Knex.js
- **Validation**: Zod
- **Payments**: Stripe, Stripe Checkout, Stripe Webhooks
- **Testing**: Vitest, Supertest
- **Infrastructure**: Docker, Docker Compose
- **Development & Version Control**: npm, Git, GitHub

## 🔌 Backend API

The project exposes backend APIs for functionality such as:

- Health/status checking
- Usage-related operations
- Billing functionality
- Checkout/subscription operations
- Stripe webhook processing

For the exact routes, request schemas, responses, and implementation details, refer to the route/controller definitions in the source code.

API documentation should always be kept synchronized with the implementation.

## 💰 Billing Model

The billing engine is designed around measurable application usage.

A billable request can contain usage information such as:

- API usage
- Input tokens
- Output tokens
- Other supported usage metrics

The billing calculation converts the recorded usage into a monetary amount according to the applicable pricing rules.

Monetary values should be represented using integer-based currency units where applicable rather than relying on floating-point arithmetic.

This reduces the risk of rounding errors during financial calculations.

## 🗄️ Database

PostgreSQL is used as the primary persistent database.

The database stores information required for areas such as:

- Tenants
- Subscription plans
- Subscriptions
- Usage
- Billable requests
- Webhook events
- Reconciliation

Database migrations are used to manage schema changes in a controlled and repeatable manner.

Transactions are important for operations where multiple database changes must succeed or fail together.

## 🔐 Reliability & Security

Reliability and correctness were major considerations throughout the project.

Key mechanisms include:

- **Idempotency**: Prevents repeated requests from creating duplicate billable operations.
- **Database Transactions**: Helps maintain consistency when multiple related database operations are performed together.
- **Webhook Signature Verification**: Ensures Stripe webhook requests can be validated before being processed.
- **Webhook Replay Protection**: Prevents the same webhook event from being processed repeatedly.
- **Input Validation**: Request data is validated before reaching important business logic.
- **Error Handling**: The backend handles invalid requests and operational failures through structured error handling.

## 🧪 Testing

Automated testing is used to validate important parts of the backend system.

Testing covers areas such as:

- API behavior
- Business logic
- Billing calculations
- Usage metering
- Idempotency
- Quota enforcement
- Subscription workflows
- Stripe-related functionality
- Webhook handling
- Error and edge cases

The project uses:

- **Vitest** for testing
- **Supertest** for HTTP/API testing

Run the project's test suite using the `test` command defined in `package.json`.

## 🐳 Local Development

### Prerequisites

Before running the project locally, ensure the required development tools and services are installed.

Typical requirements include:

- Node.js
- npm
- PostgreSQL or Docker
- Docker Desktop (if using the containerized setup)
- Git

### Installation

Clone the repository:

```bash
git clone https://github.com/m4ulikP/flyrank-capstone-metering-billing.git
```

Enter the project directory:

```bash
cd flyrank-capstone-metering-billing
```

Install dependencies:

```bash
npm install
```

### Environment Variables

Create a local environment file using the project's environment-variable template where available.

Typical configuration may include values for:

```env
DATABASE_URL=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
```

Never commit real API keys, database credentials, webhook secrets, or other sensitive information to GitHub.

Refer to the project's environment configuration files for the complete list of required variables.

### Database Setup

Configure PostgreSQL and run the database migrations using the migration command provided by the project.

The database schema should be initialized before starting the backend.

### Running the Application

Use the development/start command defined in `package.json`.

For example:

```bash
npm run dev
```

Use the exact script available in the repository's `package.json`.

### Running Tests

Run the automated test suite using the project's configured test command.

For example:

```bash
npm test
```

Use the exact test script defined in `package.json`.

## 📁 Repository Structure

The repository is organized around the backend application, database layer, tests, and supporting configuration.

A typical high-level structure includes:

```
flyrank-capstone-metering-billing/
│
├── src/
│   ├── routes/
│   ├── controllers/
│   ├── services/
│   ├── repositories/
│   └── ...
│
├── migrations/
│
├── tests/
│
├── Dockerfile
├── docker-compose.yml
├── package.json
├── tsconfig.json
├── .env.example
└── README.md
```

The exact directory structure should be verified against the current repository.

## 📚 Key Learning Outcomes

This internship provided practical experience in backend engineering for AI-oriented applications.

- **Backend Development**: Designing REST APIs, Structuring backend services, Working with TypeScript and Node.js, Implementing business logic
- **Database Engineering**: PostgreSQL, Database migrations, Relational data modeling, Transactions, Data consistency
- **AI Backend Infrastructure**: AI usage metering, Token-based usage tracking, Usage-aware backend design, Quota enforcement
- **Billing Systems**: Usage-based billing, Subscription management, Monetary calculations, Payment workflows
- **Reliability Engineering**: Idempotency, Retry handling, Webhook replay protection, Transactional processing, Reconciliation
- **Payment Integration**: Stripe Checkout, Stripe subscriptions, Stripe webhooks, Webhook signature verification
- **Software Engineering**: Automated testing, Docker, Git/GitHub, Debugging, Documentation, Incremental development

## 🏆 Internship Completion

I completed an 8-week Back-End AI Engineering Internship at FlyRank AI / FlyRank Corp.

| Field | Details |
|---|---|
| **Organization** | FlyRank AI / FlyRank Corp. |
| **Role** | Back-End AI Engineering Intern |
| **Start Date** | 1 July 2026 |
| **End Date** | 26 August 2026 |
| **Duration** | 8 Weeks |
| **Capstone** | Multi-Tenant Usage Metering & Billing Engine |

The internship provided hands-on exposure to backend engineering, AI-oriented infrastructure, databases, billing systems, payment integrations, testing, and reliability-focused software development.

## 📄 Internship Documents

The internship documentation may include:

- Internship Report
- Internship Presentation
- Internship Offer / Confirmation Letter
- Internship Completion Certificate

These documents provide supporting evidence of the internship and its completion.

## 🔗 Project Links

- **GitHub Repository**: https://github.com/m4ulikP/flyrank-capstone-metering-billing
- **FlyRank AI**: https://flyrank.ai/
- **IILM University**: https://iilm.edu/

## 📖 References

- **FlyRank AI** — https://flyrank.ai/
- **PostgreSQL** — https://www.postgresql.org/
- **Node.js** — https://nodejs.org/
- **Express.js** — https://expressjs.com/
- **TypeScript** — https://www.typescriptlang.org/
- **Stripe** — https://stripe.com/
- **Stripe Documentation** — https://docs.stripe.com/
- **Docker** — https://www.docker.com/
- **GitHub** — https://github.com/

## 🙏 Acknowledgement

I would like to express my sincere gratitude to FlyRank AI / FlyRank Corp. for providing me with the opportunity to work as a Back-End AI Engineering Intern and gain practical experience in backend and AI-oriented software engineering.

I also thank IILM University for its academic support and guidance throughout the internship.

## 👨‍💻 Author

**Maulik Pandey**

- B.Tech Computer Science & Engineering (AI/ML)
- IILM University
- Batch: 2025–2029
- Roll Number: 25SCS1003003495

**Internship**: Back-End AI Engineering Intern — FlyRank AI  
**Capstone Project**: Multi-Tenant Usage Metering & Billing Engine  

**Repository**: https://github.com/m4ulikP/flyrank-capstone-metering-billing

© 2026 Maulik Pandey | IILM University
