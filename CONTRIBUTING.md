
# Contributing to Tech-FAQs

The following is a set of guidelines for contributing to Tech-FAQs.
These are mostly guidelines, not rules. Use your best judgment, and feel free to propose changes to this document in a pull request.

#### Table Of Contents

[Code of Conduct](#code-of-conduct)

[How Can I Contribute?](#how-can-i-contribute)
* [Want to add a new Tech-FAQ](#want-to-add-a-new-tech-faq)
* [Want to contribute to an already existing Tech-FAQ](#contribute-to-an-already-existing-tech-faq)
* [Want to add usefull link you found for a technologie (eg Cheatsheets ...)](#want-to-add-usefull-link-you-found-for-a-technologie-eg-cheatsheets)

[Styleguides](#styleguides)
* [Git Commit Messages](#git-commit-messages)


## Code of Conduct

This project and everyone participating in it is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to [animenon@mail.com](mailto:animenon@mail.com).

## How Can I Contribute?

> ## For Beginners:
>
> Instructions-
>
> 1. Fork this Repository (using the button at the top-right side)
> 2. Clone your forked repository to your desktop/laptop (i.e. `git clone <git-repo-https_or_ssh-link>`)
> 3. Create a new branch for your modifications (i.e. `git branch new-branch-name` and check it out `git checkout new-branch-name`)
> 4. Add your files (git add -A), commit (git commit -m "my first commit") and push (git push origin new-user)
> 5. Create a pull request (*You have raised your first PR!*)
> 6. Star this repository (optional)


Please send a [GitHub Pull Request](https://github.com/animenon/Tech-FAQs/pull/new/master) with a clear list of what you've done (read more about [pull requests](http://help.github.com/pull-requests/)). Please make sure all of your commits are atomic (one feature per commit).

Always write a clear log message for your commits and add the number of the Issue (if your commit is for an Issue). One-line messages are fine for small changes, but bigger changes should look like this:

    $ git commit -m "A brief summary of the commit
    > 
    > A paragraph describing what changed and its impact."

### Want to add a new Tech-FAQ?

* Create a new folder for your technologie
* Use [Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)-files to add the information you think is relevant (eg commands, usefull hints...)
  * maybe structure the information in different, meaningful files

### Want to contribute to an already existing Tech-FAQ?

* Create a new file or extend an existing one in the regarding technologie-folder
* Use [Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)  to add the information you think is relevant (eg commands, usefull hints...)

### Want to add usefull link you found for a technologie (eg Cheatsheets ...)

* Add our link in the regarding file in the [tech-docs](tech-docs) folder

## Styleguides

### Git Commit Messages

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line to 72 characters or less
* Reference issues and pull requests liberally after the first line
