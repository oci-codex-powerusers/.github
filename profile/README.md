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

## Learnings

* Learn to read and improve code.
* Learn GitHub collaboration through real contributions.
* Set up and use Codex effectively.

## Guidelines

Keep contributions focused, documented, tested, and free of credentials or private OCI configuration. Each repository may add project-specific contribution instructions.
