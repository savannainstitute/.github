# Contributing to a Savanna Institute repository

This page is for someone who has never opened a pull request. It says how a change gets into one of
the organization's repositories, step by step, and what the words mean.

## The words

- A repository is one project's files and their whole history.
- The owner is the person named as the repository's owner. The owner decides who may work inside the
  repository, and the owner is the only person who merges changes into it.
- A contributor is someone the owner has named. A contributor works on branches inside the
  repository.
- A branch is a separate line of work. The main branch, called `main` in most repositories, holds
  the version everyone relies on. Nobody changes `main` directly, the owner included.
- A fork is your own copy of a repository under your own account. Anyone can make one.
- A pull request is a request to bring the changes on a branch into `main`. It shows every changed
  line, runs the organization's checks, and holds the conversation about the change.
- The check is the set of tests the organization runs on every pull request. A pull request can be
  merged only when the check passes.

## Branch or fork: which one you use

If you own the repository, or the owner has named you a contributor, you work on a branch inside the
repository. Otherwise you work on a fork.

To tell which you are, open the repository on GitHub. If you can see a Settings tab, you are the
owner. If not, ask the owner whether you are a contributor, or try to push a branch: a push that is
refused means you work on a fork. Nothing breaks when you try.

To make a fork, open the repository on GitHub and press Fork. GitHub makes the copy under your
account. Clone that copy to your computer, not the original.

## Making the change

1. Clone the repository, or your fork of it, to your computer.
2. Make a branch named for the change, for example `fix-plot-labels`:

   ```text
   git checkout -b fix-plot-labels
   ```

3. Make the change and commit it, in as many commits as you like. Each commit message says what the
   commit does.
4. Push the branch:

   ```text
   git push -u origin fix-plot-labels
   ```

## Opening the pull request

GitHub prints a link after the push; open it, or go to the repository's page and press Compare and
pull request. On a fork, the pull request goes from your fork's branch to the original repository's
`main`.

The description starts from a template. Write what the change does and why in a few sentences, then
fill in the headings that apply:

- Dependencies: each package the change adds, and what it is for.
- Docs added: each new document outside the `docs` folder, and why it exists.
- Tests removed or skipped: each test removed or skipped, and the reason.
- A change to code with no new test needs a line starting with the words "No test because".

Leave a heading alone when it does not apply. The check reads these headings, so a package added
without a line under Dependencies fails the check.

## Reading the check

A minute or two after the pull request opens, the check reports at the bottom of the page. A green
mark means it passed. A red mark means it found something: press Details, and read the lines that
name a file, a line number and what to change. Each line says what to do.

Fix each finding on your branch, commit, and push again. The check runs again on its own; nothing
else is needed. If you work with a coding agent such as Claude Code, Codex or Gemini, paste the
check's output to it and ask it to fix the findings; the repository carries instructions that tell
the agent the rules.

A finding marked warning does not stop the merge. It is there for you and the owner to read.

## Merging

The owner merges the pull request once the check passes. If you are the owner, you merge your own
pull request; nobody else has to approve it. The branch is deleted when it merges, and the change is
on `main`.

## Running the checks before you push

This is optional. Each repository carries a file that lets the same checks run on your computer
every time you commit, so the pull request passes on the first try. Install the tool once:

```text
pip install pre-commit
pre-commit install
```

The repository's `README.md` says more. The files for coding agents work the same way: they are a
convenience for your own computer, and the check on the pull request is what counts.
