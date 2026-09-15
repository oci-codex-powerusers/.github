# OCI Codex Power Users

This organization is a place to build, share, and contribute OCI projects with Codex. Start new OCI-backed Python projects with our standard skill, then bring your improvements back to the community.

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
