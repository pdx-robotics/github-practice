# Git gud with pdx-robotics!

[GitHub flow](https://guides.github.com/introduction/flow/) is the most common git workflow for open-source projects.

<details>
<summary>Links used in this document</summary>

- [GitHub flow](https://guides.github.com/introduction/flow/)
- [GitHub Desktop](https://desktop.github.com/)
- [Visual Studio](https://visualstudio.microsoft.com/vs/) 
- [Issues page](https://github.com/pdx-robotics/github-practice/issues)
- [Pull requests page](https://github.com/pdx-robotics/github-practice/pulls)

</details>

# Table of contents

- [Git gud with pdx-robotics!](#git-gud-with-pdx-robotics-)
- [Table of contents](#table-of-contents)
- [The steps](#the-steps)
  - [Clone this repository](#clone-this-repository)
  - [Find an issue](#find-an-issue)
  - [Branch](#branch)
  - [Open a pull request](#open-a-pull-request)
  - [Request reviews](#request-reviews)
  - [Merge](#merge)

# The steps

## Clone this repository

If you have [GitHub Desktop](https://desktop.github.com/) or [Visual Studio](https://visualstudio.microsoft.com/vs/) installed, simply click the green **Clone or download** button above and you'll see the option to **Open in Desktop** or **Open in Visual Studio** respectively.

Alternatively, use this command:\
`git clone https://github.com/pdx-robotics/github-practice.git`

## Find an issue

The [issues page](https://github.com/pdx-robotics/github-practice/issues) is where you'll find tasks that are looking for help. Issues labeled `good first issue` are more suitable for newcomers.

Feel free to open a new issue if you found a bug or want to request a new feature. To do this, on the [issues page](https://github.com/pdx-robotics/github-practice/issues), click the green button **New issue**.

Once you've found an issue you'd like to work on, let others know by leaving a comment.

## Branch

In [GitHub Desktop](https://desktop.github.com/), click **Branch > New branch** (Ctrl + Shift + N). 

Alternatively, use this command:\
`git checkout -b <branch>`

## Open a pull request

At anytime after branching, even before you start working, you can open a pull request (PR). To do this, go to the [pull requests page](https://github.com/pdx-robotics/github-practice/pulls) and click the green button **New pull request**. Select the base branch (usually it's `master`), and select your branch to compare with base. Then click **Create pull request**.

If your branch is not yet ready to merge, put a `[WIP]` at the begining of the title. Then click **Create pull request** one more time.

## Request reviews

When your branch is ready to merge, remove `[WIP]` from the title and start the discussion by requesting reviews. In the right sidebar under **Reviewers** there should be some people suggested. Simply click **Request** and wait. To request someone not suggested, click the gear icon and select their username.

You may now contact your reviewers by email, Discord, or talk to them in person.

Your reviewers will then leave comments, approve your PR, or request changes. _Read all feedback carefully, even if your PR has already been approved._

## Merge

With enough approvals, an admin or someone with write permissions will merge your PR. If you were working on an issue, you can now leave a comment and close the issue.
