# ci-required-workflows

Workflows that org rulesets inject into other repositories as **required workflows**.

This repository is **public on purpose**. A ruleset's `workflows` rule can only
inject a workflow that the *target* repository is allowed to read. The previous
home, `upwindsecurity/infra-github-actions`, is private — so in the org's public
repositories the required workflow never ran, the check never reported, and every
pull request was blocked waiting on a check that could never arrive.

Nothing secret belongs here. Credentials are referenced as organization secrets
and are never stored in this repository.

| Workflow | Injected by | Applies to |
|---|---|---|
| `require-jira-ticket.yaml` | ruleset `require-jira-ticket` (26618354) | all repos except the documented exclusions |

## Editing

These files run in every repository in the organization. A mistake here blocks
the whole org, so:

- a change ships to `evaluate` first where the behaviour is in question;
- the workflow must degrade safely — it fails closed when Jira is unreachable,
  and it must never publish Jira content into a public repository;
- `main` is what the rulesets fetch. There is no staging branch.
