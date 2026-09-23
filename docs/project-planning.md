# Plan an OCI project before building it

Start with the problem, not a framework. A short written plan gives Codex the context it needs to make useful technical choices, and gives you a place to review those choices before code and cloud resources appear.

This guide helps you choose a project shape for an OCI application. It does not make the choice for you. The best option depends on what the project must do, who will use it, what your team can maintain, and how much change you expect.

## Separate the experience from the work

Most applications have three jobs. They can live in one small program at first, or become separate parts as the application grows.

```text
People or other systems
        │
        ▼
Presentation and request edge
CLI • web page • desktop window • HTTP API
        │
        ▼
Application logic
rules • validation • workflows • tests
        │
        ▼
OCI integration
SDK or HTTPS calls • authentication • Object Storage • other OCI services
```

**Presentation** is how a person or another program interacts with the application. A CLI (command-line interface) is good for operators and automation. A browser UI (user interface) is good for frequent, interactive work. A desktop app is useful when local files, OS integration, or offline work matter. An HTTP API (application programming interface) is the entry point for other applications.

**Application logic** is the durable work: rules, validation, workflows, and error handling. Keep it separate from buttons and UI so it can be tested and reused.  For example, the same application core can be used for a desktop / web / CLI application.

**OCI integration** is the boundary that calls OCI. Keep OCI clients, credential resolution, and service-specific operations in one place. An SDK (software development kit) is one way to call OCI; direct HTTPS calls are another. This lets the presentation and application logic stay understandable, and keeps secrets and privileged access out of UI code.  Python and Node.js each provide SDKs that you can ask Codex to use.

Do not split these into separate services just because the diagram has three boxes. Begin with the smallest shape that meets the goal. Split a presentation layer from the logic when you need more than one client, separate release schedules, stricter privilege boundaries, or independent scaling. Keep one application when the project is small and one team owns the whole workflow.

## Make the decisions in order

Write down the following before asking Codex to build. Short answers are enough at first.

1. **Goal and outcome** — What problem should be easier after this project exists? What does success look like?
2. **Audience and workflow** — Who uses it, how often, and from where? Are they operators, developers, customers, or another system?
3. **Presentation** — Is the right entry point a CLI, API, browser UI, desktop app, or a combination?
4. **Logic and data** — What rules, workflows, data, and failure cases matter? What should never happen?
5. **OCI boundary** — Which OCI services are used? How will local development authenticate? How will a workload authenticate after deployment?
6. **Deployment and operations** — Is local-only enough? If it runs in OCI, who owns the network, Load Balancer, image repository, and IAM (access-control) policy?
7. **Team fit** — Which language and tools can the people maintaining it confidently test, update, and secure?
8. **Proof of done** — What commands, tests, documentation, and first useful user action must work before the project is accepted?

Record decisions, assumptions, and open questions. A decision is not permanent, but making it visible is much better than allowing a framework choice to become an accidental architecture.

## Choosing a Python approach

Use Python when the team is strongest in Python, the work is data- or automation-heavy, or existing Python libraries are central to the project.

| Option | Best for | Benefits | Trade-offs |
| --- | --- | --- | --- |
| [FastAPI](https://fastapi.tiangolo.com/) | Typed HTTP APIs and interactive web products with a separate frontend | Async-friendly, clear API contracts, and OpenAPI support | You choose the surrounding database, authentication, admin, and UI pieces |
| [Flask](https://flask.palletsprojects.com/) | Small APIs or server-rendered applications | Small, familiar, and flexible | The project must establish more of its own structure and conventions |
| [Django](https://www.djangoproject.com/) | Business applications with users, records, forms, and administration | Includes database models, migrations, authentication, and an admin interface | More conventions and framework surface than a focused API needs |
| [Litestar](https://docs.litestar.dev/) | Typed ASGI (async Python server interface) APIs where dependency injection and schema generation appeal | Modern API-focused features and a clear application structure | Smaller ecosystem and team familiarity than Flask or Django in many organizations |
| [Streamlit](https://streamlit.io/) | Internal, data-centric dashboards | Very fast path from Python data work to a useful interface | Less control over a custom product experience |
| [Flet](https://flet.dev/) | A Python-led web or desktop interface | One Python codebase can target web and desktop, with built-in run/build tooling | The UI follows Flet's control model rather than normal HTML/CSS/JavaScript patterns |
| [PySide6 / Qt](https://doc.qt.io/qtforpython-6/) | Deep native desktop tools | Mature native widgets and strong desktop capabilities | More traditional desktop UI development and packaging work |

Useful starting combinations:

- An operator job: Python CLI plus a small OCI adapter.
- An internal dashboard: Streamlit, or FastAPI plus a small browser frontend when the UI will grow.
- A record-heavy business app: Django.
- A public or multi-client API: FastAPI or Litestar.
- A local desktop operator tool: Flet for speed, or PySide6 when native desktop depth matters.

## Choosing a Node.js approach

Use Node.js or TypeScript when the team is strongest in web development, the browser or desktop experience is central, or shared TypeScript across UI and server will reduce friction.

| Option | Best for | Benefits | Trade-offs |
| --- | --- | --- | --- |
| [Fastify](https://fastify.dev/) | Typed JSON APIs and focused services | Lean, plugin-oriented, and a strong default for a new Node service | Less familiar than Express for some teams |
| [Express](https://expressjs.com/) | Small services or teams with established Express knowledge | Simple and widely understood with a large ecosystem | The project must establish more of its own validation, typing, and architecture |
| [NestJS](https://docs.nestjs.com/) | Larger services and teams that value a prescribed structure | Modules, dependency injection, and testing conventions; supports Express or Fastify underneath | More boilerplate and framework ceremony for a small application |
| [React + Vite](https://vite.dev/) | A browser product with a separately deployed API | Fast UI iteration and broad frontend talent availability | You still choose routing, data access, and application conventions |
| [Next.js](https://nextjs.org/docs) | React products that need server rendering or a full-stack React convention | Integrated routing and rendering model | It is a product framework, not a substitute for deciding API and OCI boundaries |
| [Electron](https://www.electronjs.org/) | Desktop tools needing local files, native integrations, or familiar web tooling | Mature desktop ecosystem and a clear web-to-desktop path | Larger distribution footprint and a meaningful main/renderer security boundary |
| [Tauri](https://tauri.app/) | Smaller desktop binaries with a web frontend | Can use a web frontend while using Rust for native functionality | Requires Rust tooling and has less direct reuse of Node-native modules |

### Useful starting combinations

- An operator job: TypeScript CLI plus a small OCI adapter.
- A focused API: Fastify.
- A larger service: NestJS, often with Fastify underneath.
- A browser product: React + Vite or Next.js with a deliberate API boundary.
- A desktop operator tool: Electron when web and Node skills dominate; Tauri when smaller binaries and Rust expertise matter.

## Create a context file

At the root of the new repository, create `PROJECT_PLAN.md` before implementation. It is a lightweight context file for you and Codex, not a contract that prevents learning or change.

**NOTE:** You can/should tell Codex to make this planning file with you.  Always review and tell Codex what to change in the planning file.  YOU get the final say here - make edits yourself if you like.

```markdown
# Project plan: <project name>

## Goal

- Problem to solve:
- Outcome that proves it is useful:
- Not in scope for the first version:

## Audience and workflow

- Primary users:
- What they need to accomplish:
- Where and how they work:

## Proposed shape

- Presentation: CLI, web, desktop, API, or combination
- Application logic: key workflows and rules
- Language and framework: decision and reason
- OCI services and integration boundary:

## Security and operations

- Local authentication:
- OCI workload authentication:
- Deployment target:
- Resource ownership and IAM assumptions:

## Decisions and open questions

| Decision or question | Current answer | Why / owner |
| --- | --- | --- |
| Example: local-only or container deployment? | Local-only for v1 | Revisit after users validate the workflow |

## Definition of done

- First useful user action:
- Tests and checks:
- Documentation and run instructions:
```

Never put credentials, private keys, tokens, complete PAR URLs, or real OCI identifiers in this file. Use names, placeholders, and links to approved secret-management locations instead.

## Ask Codex to plan, then build

Start with a planning request. Ask Codex to write or refine `PROJECT_PLAN.md`, explain its recommendations, and stop before implementation if a decision needs your input.

> Help me plan an OCI project before building it. The goal is to help **[audience]** accomplish **[outcome]**. They work **[where/how often]**. We expect to use **[OCI services]** and the team is strongest in **[Python/TypeScript/etc.]**. Create `PROJECT_PLAN.md`, recommend the smallest suitable presentation and logic shape using the options in this guide, list trade-offs and open questions, and do not implement it yet.

Once the plan reads correctly, ask Codex to build from it:

> Read `PROJECT_PLAN.md` and build the project it describes. Apply the `oci-python-project` or `oci-node-project` skill as appropriate. Preserve the decisions and constraints in the plan, ask before making a material architecture or OCI deployment change, and document any necessary exception.

Review the plan whenever the audience, workflow, OCI services, deployment target, or team ownership changes. Update the context file first, then ask Codex to implement the revised plan.

## Related

- [OCI Codex Power Users profile and skill installation](../profile/README.md)
