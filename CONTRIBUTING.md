# Contributing to Savanna Institute repositories

This guide describes the contribution process taking effect on December 4, 2026. Each change to a
repository's default branch requires a pull request and passing automated checks. The requirements
apply equally to repository owners, contributors, and work produced with coding agents.

## Access and responsibility

Each repository has a designated owner who assigns contributors and merges pull requests. Owners and
designated contributors work on branches within the repository. Other contributors submit pull
requests from forks, subject to repository access and forking permissions. Confirm your role with
the repository owner; contact Zack if the owner is unclear or you need organization membership.

Private repositories require access before they can be cloned or forked. Their owners may disable
forking. If access or forking restrictions prevent a contribution, contact the owner to arrange it.
Two-factor authentication is required from November 20, 2026.

Only the repository owner merges changes into the default branch, usually named `main`. Owners may
merge their own pull requests once all required checks pass; another person's approval is not
required. Direct pushes, force pushes, and deletion of the default branch are prohibited.

## Preparing a change

Clone the repository if you are an owner or designated contributor. Otherwise, use GitHub's Fork
button and clone your fork. Follow the repository README for environment setup, dependencies, and
test commands. Start a branch from the current default branch:

```sh
git checkout main
git pull --ff-only
git checkout -b fix-plot-labels
```

Substitute the repository's default branch if it differs from `main`. When working in a fork, sync
the fork with the original repository before starting. Commit the changes and push the branch:

```sh
git add <changed-files>
git commit -m "Correct plot labels"
git push -u origin fix-plot-labels
```

Include tests for changed behavior and update affected documentation. Requirements for source files,
data, dependencies, and documentation are listed in the
[automated check reference](https://github.com/savannainstitute/standards/blob/main/docs/RULES.md).
Binary data uses Git LFS; run `git lfs install` once before working with it. Record data sources,
licenses, units, and input or output status in the data README.

## Pull requests

Open a pull request using the link returned by the push or GitHub's Compare and pull request button.
Select the original repository's default branch as the destination, including when submitting from a
fork. Describe the problem, the change, and how it was validated.

Complete the applicable fields in the pull request template. The automated check reads these labels:

- `Dependencies:` names each added package and its purpose.
- `Docs added` lists new Markdown files outside the docs directory and their purpose. README files
  and the standard root files listed in the check reference are exempt.
- `Tests removed or skipped` identifies affected tests and explains the reason.
- `No test because` explains a source change submitted without a test change.

Retain the template's labels and leave inapplicable fields empty. An explanation documents an
exception for review; it does not disable other checks.

## Checks and merge

Continuous integration (CI) runs the shared checks on each pull request. These include formatting,
static analysis, tests and coverage where applicable, secret detection, and the organization rules.
Open a failed check's Details link to inspect its output. Rule findings identify the rule, file,
line, and corrective action. Installation, infrastructure, and test failures may require reviewing
the job log rather than a file-level finding.

Correct failures on the same branch, commit, and push; this reruns the checks on the existing pull
request. Warnings are available for review and do not block merging. Report an incorrect finding or
a requirement that prevents valid work through the feedback process below.

The owner reviews and merges the pull request after the required checks pass. GitHub automatically
deletes merged branches within the repository. Update your local default branch before beginning the
next change.

Local checks are optional and can identify problems before submission. In the project's environment,
install and run the configured pre-commit hooks:

```sh
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

Local hooks use the versions configured in the repository; hosted checks determine whether the pull
request can merge. Repository instructions for coding agents support the same contribution process.

## Feedback on the standards

Submit feedback through a
[standards issue](https://github.com/savannainstitute/standards/issues/new) or contact Zack
directly. Feedback before December 4 will inform the rollout; problems can also be reported
afterward.

Identify the requirement or rule ID, the repository or type of work affected, and the practical
effect. Useful feedback includes requirements worth retaining, unclear instructions, unnecessary
effort, incorrect findings, and steps that block an analysis or collaboration. Include an example
and a suggested alternative where possible. State whether work is blocked and any relevant deadline.
Send sensitive examples directly rather than posting them in a public issue.
