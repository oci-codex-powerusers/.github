# OCI Codex Power Users

This organization is a place to build, share, and contribute OCI projects with Codex. Start new OCI-backed Python or Node.js projects with our standard skills, then bring your improvements back to the community.

## Read approval prompts before accepting

Codex asks for approval before actions that can change your computer, repository, cloud resources, or external services. Those prompts are intentional safety checkpoints, not routine buttons to click through.

Before approving, read the proposed command or action and confirm its target, scope, and expected effect. In particular, pause for actions that install software, create or change OCI resources, publish or delete data, modify Git history, or send information outside your computer. If the request is unclear or broader than you expected, decline it and ask Codex to explain or narrow the action first.

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
```

Ask Codex to use the skill with a request that states your project purpose, preferred format, OCI services, and authentication or deployment needs. For example:

> Create a new OCI Python project for a team that inventories Object Storage buckets. Use the CLI format, instance-principal authentication in production, local config-file authentication for development, and `uv` for dependencies. Apply the `oci-python-project` skill and explain the IAM permissions it needs.

The skill guides you through the choices that matter, generates the appropriate project shape, and includes documentation and a structural checker. Before considering the project complete, run its `uv` setup, tests, linting, and the included `check_project.py` checker.

## Start an OCI Node.js project

You need Git and the Codex desktop app. Clone the [OCI Node.js Project Standard](https://github.com/oci-codex-powerusers/oci-node-project-skill), then link the included skill into Codex:

```bash
git clone https://github.com/oci-codex-powerusers/oci-node-project-skill.git
cd oci-node-project-skill
mkdir -p ~/.codex/skills
ln -s "$PWD/skills/oci-node-project" ~/.codex/skills/oci-node-project
```

The symbolic link keeps your local skill current when you run `git pull --ff-only` in the cloned repository. Check that the installation worked with `ls -l ~/.codex/skills/oci-node-project`. If that path already exists, do not overwrite it; check where it points, then update the existing clone or replace it only when you are sure it is no longer needed.

Open a **new Codex task** after installing the skill, then create an empty repository for your project:

```bash
mkdir my-oci-node-project
cd my-oci-node-project
git init
```

Ask Codex for the project you want. State the project purpose, users, OCI services, authentication model, and whether it should run locally only or deploy to OCI Container Instances behind an existing Load Balancer. For example:

> Create a new OCI Node.js project for a team that inventories Object Storage buckets. Use the CLI format, local config-file authentication for development, instance principals in OCI, and local-only deployment. Apply the `oci-node-project` skill and explain the IAM permissions it needs.

To bring an existing Node application into the standard, keep its working public behavior and ask for the appropriate format rather than asking for a rewrite. For example:

> Ensure my PAR browser follows best practices around OCI Node apps. Apply the `oci-node-project` skill, preserve its existing user-facing behavior, treat direct Object Storage PAR HTTPS calls as OCI use, document any temporary standard exceptions, and explain the changes before making them.

The skill adds or validates the project contract, operational documentation, `check`, `test`, `build`, and safe `clean` commands, and the included `check-project.mjs` structural checker. For an OCI container deployment, it first requires an explicit deployment plan and scripts that operate only on named, pre-existing OCI network and Load Balancer resources.

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

## Learnings

* Learn to read and improve code.
* Learn GitHub collaboration through real contributions.
* Set up and use Codex effectively.

## Guidelines

Keep contributions focused, documented, tested, and free of credentials or private OCI configuration. Each repository may add project-specific contribution instructions.
