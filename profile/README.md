# OCI Codex Power Users

This organization is a place to build, share, and contribute OCI projects with Codex. Start new OCI-backed Python or Node.js projects with our standard skills, then bring your improvements back to the community.


## Start an OCI Python project

Clone the [OCI Python Project Standard](https://github.com/oci-codex-powerusers/oci-python-project-skill) and link the included skill into Codex:

```bash
git clone https://github.com/oci-codex-powerusers/oci-python-project-skill.git
cd oci-python-project-skill
mkdir -p ~/.codex/skills
ln -s "$PWD/skills/oci-python-project" ~/.codex/skills/oci-python-project
```

The symbolic link keeps your local skill current when you pull updates in the cloned repository. If `~/.codex/skills/oci-python-project` already exists, inspect and update that installation instead of overwriting it.

Open a new Codex task after installing the skill, then create an empty repository for your project:

```bash
mkdir my-oci-project
cd my-oci-project
git init
codex
```

The Python skill guides implementation choices and includes documentation and a structural checker. Before considering a project complete, run its `uv` setup, tests, linting, and the included `check_project.py` checker. Start with the planning workflow below so the skill has a clear, reviewed context file to follow.

## Start an OCI Node.js project

Clone the [OCI Node.js Project Standard](https://github.com/oci-codex-powerusers/oci-node-project-skill), then link the included skill into Codex:

```bash
git clone https://github.com/oci-codex-powerusers/oci-node-project-skill.git
cd oci-node-project-skill
mkdir -p ~/.codex/skills
ln -s "$PWD/skills/oci-node-project" ~/.codex/skills/oci-node-project
```

The symbolic link keeps your local skill current when you pull updates in the cloned repository. If `~/.codex/skills/oci-node-project` already exists, inspect and update that installation instead of overwriting it.

Open a new Codex task after installing the skill, then create an empty repository for your project:

```bash
mkdir my-oci-node-project
cd my-oci-node-project
git init
codex
```

The Node.js skill adds or validates the project contract, operational documentation, `check`, `test`, `build`, and safe `clean` commands, and the included `check-project.mjs` structural checker. For an OCI container deployment, it first requires an explicit deployment plan and scripts that operate only on named, pre-existing OCI network and Load Balancer resources. Start with the planning workflow below so the skill has a clear, reviewed context file to follow.

## Project Planning

Before asking Codex to build, make a short plan with goals, decisions, and context. This gives the project a shared starting point: who it serves, the outcome it should deliver, the chosen presentation and logic shape, OCI boundaries, and the questions that still need an answer.

Read the [project planning guide](../docs/project-planning.md). It explains how to separate presentation, application logic, and OCI integration; compare Python and Node.js options by purpose and team skill set; and create a `PROJECT_PLAN.md` context file. Do not put credentials, private keys, tokens, or real OCI identifiers in that file.

**Start with a planning prompt, not an implementation prompt.**

### For a Python project

> Help me plan an OCI Python project before building it. The goal is to help a team that inventories Object Storage buckets understand what they own and act on stale data. The primary users are cloud operators who work from a terminal during weekly reviews. We need Object Storage access, local config-file authentication for development, and instance-principal authentication after deployment. Create `PROJECT_PLAN.md`, recommend the smallest suitable project shape, list trade-offs and open questions, and do not implement it yet.

### For a Node.js project

> Help me plan an OCI Node.js project before building it. The goal is to help a team safely browse and use Object Storage PAR links. The primary users are support and operations staff who need a desktop workflow and local file selection. The application calls OCI through PAR HTTPS URLs, and the team is strongest in TypeScript. Create `PROJECT_PLAN.md`, recommend the smallest suitable presentation and logic shape, list trade-offs and open questions, and do not implement it yet.


## Codex Execution

When the plan is correct, ask Codex to build from it:

> Read `PROJECT_PLAN.md` and build the project it describes. Apply the `oci-python-project` or `oci-node-project` skill as appropriate. Preserve the plan's decisions and constraints, ask before making a material architecture or OCI deployment change, and document any necessary exception.

When Codex is done, either check the built project's `README.md` or ask it how to run the project.  It is
likely that some setup is required from the terminal, such as Python or Node.js runtimes.  You can ask
Codex how to set those up too if you get stuck.

### Read approval prompts before accepting

Codex asks for approval before actions that can change your computer, repository, cloud resources, or external services. Those prompts are intentional safety checkpoints, not routine buttons to click through.

Before approving, read the proposed command or action and confirm its target, scope, and expected effect. In particular, pause for actions that install software, create or change OCI resources, publish or delete data, modify Git history, or send information outside your computer. If the request is unclear or broader than you expected, decline it and ask Codex to explain or narrow the action first.

## Contribute

Don't keep useful improvements in a personal repository. Build projects using the shared standard, test and verify them, then contribute your improvements here. Adding documentation, tests, templates, and fixes to an existing repository is a great way to learn the collaboration workflow.

### 1. Build in your own GitHub account

Create and own the repository in your personal GitHub account while you are developing it. Run the project locally, verify its behavior, and make the initial history before asking the organization to take ownership:

```bash
git init
git add .
git commit -m "Initial project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/my-oci-project.git
git push -u origin main
```

Before the handoff, run the project's setup, tests, linting, and `check_project.py` check. Review `git status` and the files being committed to ensure no OCI configuration, private keys, tokens, `.env` files, or generated artifacts are included.

### 2. Move the repository into the organization

When the project is ready for shared ownership, ask an organization owner to review it and confirm the intended repository name, visibility, maintainers, and any required license or contribution files. Then choose one of these paths:

**Transfer the repository** — use this when the organization should become the repository's owner while preserving its full Git history, issues, releases, and pull requests. In the personal repository, open **Settings** → **General** → **Danger Zone** → **Transfer**, enter `oci-codex-powerusers` as the new owner, and confirm the repository name. You need administrator access to the personal repository and permission to create repositories in the organization. GitHub keeps the original owner as a collaborator; organization policies apply after the transfer. See GitHub's [repository-transfer requirements and steps](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository).

**Push to a new organization repository** — use this when an organization maintainer creates an empty destination repository first. Preserve the personal remote, add the organization remote, and push the reviewed branch after you have been granted write access:

```bash
git remote rename origin personal
git remote add origin git@github.com:oci-codex-powerusers/my-oci-project.git
git push -u origin main
```

If you do not have the necessary organization permission, do not attempt the transfer or push. Send the personal repository URL to an organization owner and ask them to create the destination repository or approve the transfer.
