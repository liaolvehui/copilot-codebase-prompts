# Copilot Codebase Onboarding Prompts

A reusable set of prompts for using GitHub Copilot to understand an unfamiliar codebase, analyze its core business flows, and turn verified project knowledge into maintainable Copilot instructions, documentation, and project-specific skills.

These prompts are designed to be used sequentially:

1. **Build a Codebase Knowledge Map**
2. **Analyze Core Business Flows**
3. **Create Project-Specific Copilot Knowledge and Skills**

For best results, use the first prompt together with the `acquire-codebase-knowledge` skill from GitHub's `awesome-copilot` repository.

---

## 1. Build a Codebase Knowledge Map

```text
Use the `acquire-codebase-knowledge` skill to analyze the current codebase.

I am a Java backend developer who has just taken over this project and currently has limited knowledge of the codebase.

My goal is to systematically understand:

1. The overall system architecture
2. Module responsibilities and dependencies
3. Core business domains and capabilities
4. Major business flows
5. Database models and key tables
6. External system integrations
7. Project-specific coding conventions and development patterns
8. Testing strategy and existing test conventions
9. Important technical debt, risks, and non-obvious design decisions

All conclusions must be based on evidence from the actual codebase.

Do not infer or invent behavior based only on common Java/Spring conventions. If something cannot be verified from the code, configuration, SQL, documentation, or tests, explicitly mark it as **Unconfirmed**.

Whenever possible, provide concrete references such as:

- File paths
- Module names
- Class names
- Method names
- Configuration properties
- Database tables
- API endpoints
- SQL statements

Do not modify any production or business code at this stage.

Start by building a high-level **codebase knowledge map**. Then recommend the order in which I should explore the project in more depth.
```

---

## 2. Analyze Core Business Flows

```text
Based on the codebase knowledge acquired so far, identify the most important business domains, capabilities, and end-to-end business flows in this project.

Prioritize them by importance and analyze them one by one.

Do not focus only on the technical structure of the code. I want to understand both:

- **What the code does**
- **Why the business works this way**

For each major business flow, trace the actual execution path through the codebase, including where applicable:

API / Event / Job
→ Controller / Consumer / Scheduler
→ Application or Service Layer
→ Domain Logic
→ Repository / Mapper
→ Database
→ External Systems
→ Response / Event

For every step, provide concrete code references such as:

- File path
- Class name
- Method name
- Database table
- SQL
- External API
- Message topic or queue
- Relevant configuration

Pay special attention to:

- Business rules and validations
- Status transitions and state machines
- Important enums and constants
- Transaction boundaries
- Idempotency
- Retry mechanisms
- Distributed locks
- Asynchronous processing
- Error handling
- External system dependencies
- Non-obvious business rules

Clearly distinguish between:

- **Verified from code**
- **Reasonable interpretation**
- **Unconfirmed**

At the end, create a prioritized list of the business flows that I should understand first as a developer taking over this project.
```

---

## 3. Create Project-Specific Copilot Knowledge and Skills

```text
Based on the verified codebase knowledge and business-flow analysis completed so far, create a maintainable AI knowledge system for this repository that can be used by GitHub Copilot and coding agents during future development.

Do not simply summarize the entire repository into one large file.

Separate the knowledge according to its purpose:

### 1. Repository-wide Instructions

Create or improve:

`.github/copilot-instructions.md`

Keep this file concise. It should act as the AI entry point and navigation map for the repository.

Include only information and rules that should apply broadly to future development.

### 2. Project Documentation

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

### 3. Project-Specific Skills

Identify recurring development tasks that would benefit from dedicated project-specific Skills.

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

Only create Skills that are genuinely useful for this repository.

Each Skill should describe:

- When the Skill should be used
- What project knowledge it should read first
- The recommended analysis workflow
- Project-specific constraints
- What must be checked before modifying code
- What must be verified after modifying code

Do not fill Skills with generic Java, Spring, Maven, or Git knowledge that Copilot already understands.

Prioritize knowledge that Copilot cannot easily infer without understanding this specific project, especially:

- Business rules
- Internal conventions
- Non-obvious architectural decisions
- Required development sequences
- Cross-module dependencies
- Database relationships
- Status transitions
- External integration constraints
- Known pitfalls

### Important

All generated instructions, documentation, and Skills must be based on verified evidence from the repository.

Do not turn assumptions into permanent project knowledge.

If any information is still uncertain, mark it as **Unconfirmed** or leave a TODO instead of presenting it as fact.

Before creating or modifying files, first propose the recommended directory structure and explain the purpose of each file. Wait for my confirmation before making changes.
```

---

## Recommended Workflow

```text
Step 1: Map the codebase
        ↓
Step 2: Understand the core business flows
        ↓
Step 3: Verify important assumptions against code, configuration, SQL, and tests
        ↓
Step 4: Create repository-wide Copilot instructions
        ↓
Step 5: Create maintainable project documentation
        ↓
Step 6: Create project-specific reusable Skills
        ↓
Step 7: Use the accumulated context for future feature development, debugging, testing, and code review
```

> **Verified project knowledge is more valuable than generic framework knowledge.**

## Related Resources

- GitHub Awesome Copilot: https://github.com/github/awesome-copilot
- `acquire-codebase-knowledge` Skill: https://github.com/github/awesome-copilot/tree/main/skills/acquire-codebase-knowledge
