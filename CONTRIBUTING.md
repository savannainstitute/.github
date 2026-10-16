# Contributing to Savanna Institute repositories

This guide is a draft for review, including the requirements and adoption schedule. Initial feedback
is due November 13, 2026. The schedule starts the contribution policy and staged migration on
December 4, 2026, with March 5, 2027 as the target for active repositories to meet the agreed
standards. Feedback continues during migration and afterward.

The
[automated check reference](https://github.com/savannainstitute/standards/blob/main/docs/RULES.md)
describes the available checks. Each project's adoption includes validation and coordination with
its owner. Scientific validation requires the evidence and review described below.

## Ownership and access

Each repository has a designated owner responsible for its contributors, maintenance, and merges.
Owners and designated contributors work on branches within the repository. Other contributors use
forks where access and forking permissions allow. If private repository access or forking
restrictions prevent a contribution, contact the owner to arrange access. Contact Zack if ownership
is unclear. The draft schedule includes two-factor authentication by November 20, 2026 for members
and outside collaborators.

From December 4, changes to the default branch go through pull requests, including the owner's work.
Only the owner merges. Owners may merge their own pull requests once required checks pass; a second
GitHub approval is not generally required. Scientific review below is a separate responsibility.
Direct pushes, force pushes, and deletion of the default branch are prohibited under the proposed
policy. Repository-specific enforcement is activated during migration after verification with the
owner.

New organization repositories use the repository request form and project templates. Repositories
are public by default unless their owner identifies a reason for privacy, such as personal data,
unpublished results, sensitive locations, or partner restrictions. Existing private repositories
require owner confirmation and a review of their full history for secrets before becoming public. A
successful secret scan alone does not establish that publication is appropriate.

## Contributions and checks

Follow the repository README for setup, dependencies, and test commands. Start a branch from the
current default branch, make the change, and submit a pull request to the original repository.
Include tests for changed behavior and update affected documentation. Describe the problem, the
resulting behavior, and the evidence used to validate it.

Retain the applicable labels in the pull request template. The check reads these fields:

- `Dependencies:` names each added package and its purpose.
- `Docs added` lists new Markdown files outside docs/ and their purpose. README files and the
  standard root files listed in the check reference are exempt.
- `Tests removed or skipped` identifies affected tests and explains the reason.
- `No test because` explains a source change submitted without a test change.

Leave inapplicable fields empty. An explanation records an exception for review; it does not disable
other checks. Tests that require unavailable hardware or services must declare what they need using
the project's supported test markers, rather than silently skipping.

Continuous integration (CI) runs formatting, static analysis, tests, coverage where supported,
secret detection, and organization rules. Failed checks link to logs with the findings. Correct
failures on the same branch and push to rerun the checks. Warnings do not block merging. Report
incorrect findings or requirements that prevent valid work through the feedback process below.

Tests should demonstrate the behavior affected by a change, including consequential calculations,
data preservation, and relevant failure cases. Expected results need an independent basis, and tests
must fail when the behavior is wrong. The owner and reviewer identify testing criteria based on
intended use, consequences of errors, and the existing test suite. Record these criteria and the
commands or procedures used to evaluate them in the repository.

Coverage reports identify untested lines. Numeric targets are set per repository when justified by
its testing needs; coverage otherwise reports without a percentage gate. Failed tests still block
merging. Any targets and their rationale are reviewed in the standards repository and take effect
when the project adopts that release. Test the intended pass/fail behavior before enabling required
checks. The
[coverage policy reference](https://github.com/savannainstitute/standards/blob/main/overrides/README.md#coverage-targets)
describes configuration and missing-report handling. Scientific validation requires the evidence and
review described below, regardless of the coverage percentage.

Local checks are optional for contributors and required by the shared coding-agent instructions. Run
the repository's configured pre-commit hooks to find problems before submission:

```sh
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

Local hooks use the revision configured in the repository. Hosted checks determine whether a pull
request can merge. The owner reviews the change and its validation evidence before merging.

## Scientific validation

The owner identifies changes that could affect scientific interpretation or data integrity. Examples
include calculations, model assumptions, filtering, units, missing-value handling, specimen
identity, and data import or export. Pure formatting changes do not require a new scientific review.

For a consequential change, the contributor provides the following in the pull request or linked
repository documentation:

1. The intended method, assumptions, units, valid input range, and treatment of missing or invalid
   values, with a source or rationale for the method.
2. Small reference inputs with expected outputs derived independently of the implementation. State
   how each expected value was obtained and any numerical tolerance. Include relevant edge cases,
   such as zero versus missing values, unit conversion, and records that must retain their identity.
3. A reproducible command or application procedure, the actual output, and its comparison with the
   expected output. Use synthetic or appropriately deidentified data where necessary.
4. The scientific reviewer, review outcome, and remaining limitations. Keep this review record in
   the pull request; project documentation records the method and limitations.

The owner arranges review by someone with relevant scientific expertise, preferably someone other
than the author. That reviewer can assess the method, reference cases, and outputs without reading
the implementation language. Technical review may require a different person. If suitable review is
unavailable, record that limitation and resolve it before relying on affected results for research
or operational decisions.

Automate the reference comparisons where practical. A deliberately wrong result must fail the
comparison, and a correct reference case must pass. An agent's output or a previous program's output
alone is not an independent expected result. Changes to reference values or tolerances need the same
scientific justification and review as the method. For data-collection software, test preservation
of records, identifiers, units, and missing values through storage and export as applicable.

This proposed human review procedure adds no automated approval gate. Its usefulness and workload
will be assessed in the pilot. The distinction between scientific and technical expertise is
consistent with
[Ten simple rules for scientific code review](https://doi.org/10.1371/journal.pcbi.1012375).

## Writing consistency and coding agents

Use American English and the shared formatting conventions in project-authored prose. Coding agents
must read the repository instructions, apply the configured formatters, review changed prose for
consistency, and rerun checks after corrections. Contributors remain responsible for the result.

Preserve external API names, identifiers required by file formats, data values, quotations, and
reference titles. A spelling correction must not change a public interface or scientific meaning.
Review the diff after an agent's correction pass; a second formatting pass should leave it
unchanged.

The spelling check excludes inline backtick literals and Markdown block quotations. It detects a
limited set of patterns, and other false positives remain possible. Findings are advisory. Report
these false positives with the affected rule and context; do not change a required literal merely to
remove a warning. The existing tools do not provide a verified automatic correction process across
all supported coding agents.

## Repository structure, data, and deployments

Use lowercase, hyphenated repository names and the project-appropriate template layout. Include a
README, repository description, and .gitignore. Public repositories require a license; MIT is the
organization's default, subject to third-party obligations. Versions cited in publications use a
protected `published/<name>` tag identifying the code used.

Small text datasets may be tracked in Git. Binary data uses Git LFS; large or growing collections
belong in suitable external storage with their locations documented. Record sources, dates,
licenses, units, and input or output status in the data README. Do not commit credentials,
third-party installers, or software distributions. Coordinate historical data cleanup and any
history rewrite with the owner and affected contributors, including instructions for refreshing
existing clones.

Services the organization relies on use organization-owned hosting accounts with more than one
administrator and deploy from the default branch through the hosting integration. Review existing
deployments individually. If a service cannot support that arrangement, document the alternative,
responsible maintainer, access recovery, and deployment procedure with the owner. Record who can
maintain the service and recover access.

## Standards updates and compute

Use the
[scientific review record](https://github.com/savannainstitute/standards/blob/main/docs/scientific-review.md)
to document method checks and expected results. The
[adoption and recovery procedure](https://github.com/savannainstitute/standards/blob/main/docs/adoption-review.md)
provides the installation, pilot, rollback, compute, and backup-administration records. These
records make the proposed process reviewable before project migration; they do not certify existing
work.

Under the proposed update process, repositories adopt a tested standards version. An update pull
request changes the workflow commit reference, local hooks, and agent instructions together. The
standards maintainer tests representative Python, R, and application projects, checks that later
central changes leave earlier versions unaffected, and verifies rollback before recommending an
update. Owners review the effect on their project before merging; a failed update leaves the
previous version in place. Rollback restores the complete previous bundle and reruns the checks.

Existing installations may follow the standards main branch with separately selected local hook
revisions. The release adoption tool updates workflow and hook references together with agent files.
The hosted check verifies that they match the executing release, and repository creation installs
the selected bundle. Coordinate release validation and migration before use. GitHub supports
[commit references for reusable workflows](https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows#calling-a-reusable-workflow).

Routine checks will use hosted Linux runners and small representative datasets. Cancel superseded
runs, set timeouts, cache dependencies, and limit artifact retention. Assess long analyses,
training, specialized hardware, and platform tests separately with the owner. A self-hosted runner
requires an identified maintainer and an isolation and recovery plan.

Use existing billing and repository activity to establish the compute baseline, then measure the
additional cost of pilot checks. Review usage by repository and workflow; distinguish compute from
storage, and usage before discounts from actual charges. No workflow activity does not establish
that a repository is inactive. Disabled workflows can make recent usage unrepresentative.

The compute budget is shared across the organization. Before setting a spending limit, identify the
billing administrator and backup, notification recipients, spending authority, and recovery
procedure. Review measured usage and pilot costs to select the amount. GitHub
[budget alerts and stop-usage controls](https://docs.github.com/en/billing/how-tos/set-up-budgets)
are different settings; a spending stop can prevent required checks from running. The reporting job
records usage and repository drift. Validate its planned report and state writes in a dry run and
assign responsibility for reviewing reports before enabling the schedule.

## Migration and maintenance

Initial feedback closes November 13. Revise the proposal and communicate material changes before
migration begins December 4. Start with representative Python, R, and application projects. For each
repository, the owner and coordinator identify required cleanup, scientific reference cases where
applicable, compute needs, and any access or deployment constraints.

Install the tested checks and instructions, resolve blocking findings or document reviewed
exceptions, and run a real pull request. Activate required checks only after they work and the owner
can complete the contribution process. A pilot succeeds when the owner can make a normal change,
interpret the results, and merge without Zack troubleshooting. Record friction and support time
before extending the approach to more repositories.

Current rules check the whole repository unless their scope explicitly limits them to changed files.
Staging does not exempt old files automatically. Coordinate renaming, restructuring, data
relocation, history cleanup, and hosting changes separately within the migration schedule. Record a
temporary exception's scope, reason, responsible owner, and review date; test any check
configuration needed to implement it. Raise deadline risks early. The target for active repositories
is March 5, 2027; inactive repositories may be archived, with compliance required before work
resumes.

The standards coordinator maintains the shared checks and operating instructions. Identify a backup
administrator during migration. Review recurring failures and contributor feedback periodically;
responses may include clearer instructions, a template change, correcting or removing a check, or
adding a tested rule. Publish material requirements changes and provide an adoption period.

## Feedback on the standards

Submit initial feedback by November 13, 2026 through a
[standards issue](https://github.com/savannainstitute/standards/issues/new) or contact Zack
directly. Continue reporting problems during migration and after March 5, 2027.

Identify the requirement or rule ID, the work affected, and the practical effect. Include
requirements worth retaining, unclear instructions, unnecessary effort, incorrect findings, and
steps that block research or collaboration. Give an example and a suggested alternative where
possible. State whether work is blocked and any relevant deadline. Send sensitive examples directly
rather than posting them in a public issue. The coordinator records the disposition and communicates
resulting changes.
