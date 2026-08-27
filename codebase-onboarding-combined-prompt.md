# Combined Copilot Codebase Onboarding Prompt

This is a single end-to-end prompt that combines codebase discovery, business-flow analysis, and the creation of maintainable project-specific Copilot knowledge and Skills.

It is intended for developers taking over an unfamiliar Java backend project and using GitHub Copilot Agent mode together with the `acquire-codebase-knowledge` Skill.

## Prompt

```text
Use the `acquire-codebase-knowledge` skill to systematically analyze the current codebase and help me take over this project.

I am a Java backend developer who has just taken over this project and currently has limited knowledge of the codebase.

Your goal is not merely to explain individual classes. You should progressively build an evidence-based understanding of the system, its business logic, and its development conventions, and then turn that verified knowledge into maintainable project-specific context for GitHub Copilot and coding agents.

Work through the following phases in order.

# Phase 1 — Build the Codebase Knowledge Map

Systematically analyze the repository and establish a high-level understanding of:

1. Overall system architecture
2. Module responsibilities and dependencies
3. Core business domains and capabilities
4. Major business flows
5. Database models and key tables
6. External system integrations
7. Project-specific coding conventions and development patterns
8. Testing strategy and existing test conventions
9. Important technical debt, risks, and non-obvious design decisions

Identify important technologies and infrastructure where applicable, including:

- Java and framework versions
- Spring Boot / Spring Cloud
- Maven / Gradle modules
- Persistence frameworks
- Databases
- Messaging systems
- Caching
- HTTP / RPC clients
- Scheduled jobs
- Authentication and authorization
- Configuration management
- Logging and monitoring
- Deployment and CI/CD

Do not simply list directories or dependencies. Explain what each important module does and how modules interact.

# Phase 2 — Understand the Core Business Flows

Based on the knowledge acquired in Phase 1, identify the most important business domains, capabilities, and end-to-end business flows.

Prioritize them by importance and analyze them one by one.

Do not focus only on technical structure. I need to understand both:

- What the code does
- Why the business works this way

For each important business flow, trace the actual execution path through the repository where applicable:

API / Event / Job
→ Controller / Consumer / Scheduler
→ Application or Service Layer
→ Domain Logic
→ Repository / Mapper
→ Database
→ External Systems
→ Response / Event

For every step, identify concrete implementation references whenever possible:

- File path
- Module
- Class
- Method
- API endpoint
- Request / response DTO
- Database table
- SQL
- External API
- Message topic or queue
- Configuration

Pay special attention to non-obvious behavior, including:

- Business rules and validations
- Status transitions and state machines
- Important enums and constants
- Transaction boundaries
- Idempotency
- Retry mechanisms
- Distributed locks
- Asynchronous processing
- Message consistency
- Error handling
- External system dependencies
- Cross-module dependencies
- Hidden prerequisites or ordering constraints

At the end of this phase, produce a prioritized list of the business flows that a developer taking over this project should understand first.

# Phase 3 — Create Maintainable Copilot Project Knowledge

After the architecture and important business flows have been sufficiently analyzed and verified, design a maintainable AI knowledge system for this repository.

Do not dump everything into one large document.

Separate knowledge according to its purpose.

## Repository-wide Instructions

Create or improve:

`.github/copilot-instructions.md`

Keep this file concise. It should act as the AI entry point and navigation map for the repository.

Include only information and rules that broadly apply to future development.

## Project Documentation

Create appropriate project knowledge documents for topics such as:

- System architecture
- Module responsibilities
- Core business domains
- Major business flows
- Database model
- External integrations
- Development conventions
- Testing conventions
- Troubleshooting
- Known risks and technical debt

Avoid duplicating the same information across multiple documents.

## Project-Specific Skills

Identify recurring development tasks that genuinely benefit from dedicated project-specific Skills.

Possible examples include:

- Implementing a new business feature
- Modifying an existing business flow
- Adding or changing an API
- Making database changes
- Integrating with external systems
- Fixing bugs
- Writing tests
- Reviewing code
- Troubleshooting production issues

Each Skill should define:

- When it should be used
- What project knowledge should be read first
- Recommended analysis workflow
- Project-specific constraints
- Checks required before modifying code
- Verification required after modifying code

Do not fill Skills with generic Java, Spring, Maven, Git, or software-engineering knowledge that Copilot already understands.

Prioritize repository-specific knowledge that cannot be reliably inferred without understanding this project, especially:

- Business rules
- Internal conventions
- Non-obvious architectural decisions
- Required development sequences
- Cross-module dependencies
- Database relationships
- Status transitions
- External integration constraints
- Known pitfalls

# Evidence and Accuracy Rules

These rules apply throughout all phases:

1. All conclusions must be grounded in actual repository evidence.
2. Do not infer or invent behavior merely from common Java/Spring conventions.
3. Verify important claims against code, configuration, SQL, documentation, and tests whenever possible.
4. Whenever possible, cite concrete references such as file paths, classes, methods, configuration properties, database tables, APIs, and SQL.
5. Clearly distinguish between:
   - Verified from code
   - Reasonable interpretation
   - Unconfirmed
6. If something cannot be verified, explicitly mark it as `Unconfirmed` or leave a TODO rather than presenting it as fact.
7. Do not convert assumptions into permanent project documentation or Skills.

# Modification Rules

During the discovery and business-analysis phases, do not modify production or business code.

Before creating or modifying repository instruction files, documentation, or Skills:

1. Summarize the verified knowledge gathered so far.
2. Identify important remaining unknowns.
3. Propose the recommended documentation / instruction / Skill directory structure.
4. Explain the purpose of each proposed file.
5. Wait for my confirmation before creating or modifying those files.

# Final Goal

The final result should allow both me and future Copilot sessions to quickly understand:

- What this system does
- How it is architected
- How its core business flows work
- Where important business rules live
- How data moves through the system
- How external systems interact with it
- How new features should normally be implemented
- What project-specific rules must be followed
- What common pitfalls should be avoided

The guiding principle is:

**Verified project knowledge is more valuable than generic framework knowledge.**

Start with Phase 1. Progress through the phases in order, and do not sacrifice accuracy for speed or completeness.
```

## Related

- [Three-stage version](./codebase-onboarding-prompts.md)
- [GitHub Awesome Copilot](https://github.com/github/awesome-copilot)
- [`acquire-codebase-knowledge` Skill](https://github.com/github/awesome-copilot/tree/main/skills/acquire-codebase-knowledge)
