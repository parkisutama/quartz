---
title: "Effective Python Developer Tooling in December 2024"
link: "https://pydevtools.com/blog/effective-python-developer-tooling-in-december-2024/"
author:
published: 2024-12-21
created: 2024-12-30T00:00
description: "I have been writing Python for 14 years next month. When I started, people were still using easy_install to install egg-based packages for Python 2.7 and nobody had heard about Conda yet, much less uv. Needless to say, the Python tool ecosystem has changed and developed since. Many people are rightfully confused by the fragmentation in the ecosystem; at the same time, we unequivocally have better tooling for Python today than we’ve ever had before."
tags: ["clippings"]
updated: 2024-12-31T05:48
publish: true
---

I have been writing Python for 14 years next month. When I started, people were still using easy\_install to install egg-based packages for Python 2.7 and nobody had heard about Conda yet, much less uv. Needless to say, the Python tool ecosystem has changed and developed since. Many people are rightfully confused by the [fragmentation](https://xkcd.com/1987/) in the ecosystem; at the same time, we unequivocally have better tooling for Python today than we’ve ever had before.

A friend recently invited me to give a talk to his team about Python tooling. In the presentation, I shared some principles of Python tooling and developer efficiency, some anti-patterns I’ve observed, recommended practices, and an opinionated list of tools I like in December 2024. What follows is a summary of that talk.

## Principles

1. **Python is a great programming language.** I love Python and am privileged to work with it every day. It’s expressive, readable, and powerful. The open-source community has built a wealth of libraries and tools that make Python an excellent choice for many tasks (as many have observed, Python is the second-best language for everything).
2. **Python doesn’t enforce (or necessarily encourage) good practices.** It is a language that allows you to write bad code quickly. It’s easy to write code that works but is hard to read, maintain, and test. I think this goes hand in hand with the beautiful simplicity that makes Python easy to get started with.
3. **Many of us came to Python without software engineering experience.** Particularly through the data science revolution, many folks have come to Python from math, physics, and other sciences and have not been exposed to the lessons of software engineering learned over the last 50 years.
4. **The Python developer tooling ecosystem is fragmented.** Many tools are available for managing Python packages, formatting code, linting code, testing code, and more. This fragmentation can be confusing and frustrating.
5. **Python developer experience can get better.** Python developers and teams can be more productive and happier with the right tools and practices.
6. **Python standards have moved forward.** The Python community has made progress on standards, especially around packaging (e.g., [PEP 723](https://peps.python.org/pep-0723/)).
7. **Automation and consistency will make us happier and more productive.** Automating repetitive tasks and enforcing consistency will make us happier and more productive. It will make our codebases more maintainable and our processes more reliable.
8. **The things people complain about (e.g. installing Python and packaging) are mostly solved problems.** Some edge cases are still hard, but for most people, installing Python and managing packages can be easier than ever. The hard part is knowing what tools to use.

## Anti-Patterns

I’ve observed these anti-patterns in Python code bases, especially those that can be improved by adopting better tools and practices.

1. **Code cruft:** For example, dead code, commented out code, and unused imports. These slow down development and can slow down code execution.
2. **Dumb team arguments:** For example, arguing about `f` strings vs `.format`. This is a minor point and a waste of time for your team to debate. Pick one and move on.
3. **Inconsistent code style:** Inconsistent style makes code harder to read and maintain.
4. **Unnecessary complexity:** Unnecessary complexity makes code harder to read and maintain.
5. **Ignoring Python standards:** Despite the tooling fragmentation, standards like use of pyproject.toml files for configuration and dependency management are becoming more common. Don’t neglect these.
6. **Lack of consistency:** Consistency is key to maintainability. Particularly when a team has multiple Python projects, seek consistency around building, testing, deploying, and organizing code.
7. **Lack of automation:** Automation is key to productivity. Automate (especially with your continuous integration system) repetitive tasks like formatting, linting, testing, and building.
8. **Lack of internal packages:** Many companies lack the infrastructure to build and share internal Python packages. This leads to copy-and-paste, sharing code via S3 or other blob storage, and other inefficiencies.
9. **Lack of reproducibility:** Developers should be able to check out a project and run it without needing to ask questions.

## Some “Best” Practices

I dislike the term best practice but use of the term seems to be a best practice. In any case, here are some practices that I recommend:

1. **Make it easy to make packages (and make them):** Packaging is a solved problem. Make it easy to create packages and share them on an internal repository.
2. **Auto format your code:** Use [ruff](https://astral.sh/ruff) to automatically format your code. This will (usually) make your code more readable and maintainable, and it will remove cognative load from your team in writing and reading code.
3. **Lint your code:** Use [ruff](https://astral.sh/ruff) to lint your code. This will help you catch errors and syntax issues before they become bugs. Review the Ruff rules and adopt a list that makes sense for your organization; don’t bikeshed further.
4. **Set up your editor for formatting and linting:** Enable editor integration for automatic formatting and linting. This will make it easy for your team to write code that conforms to your standards.
5. **Automate your checks:** Use continuous integration to automate your checks (linters, type checkers, etc). This will ensure that your shared code is consistently formatted, linted, and tested.
6. **Make Python projects consistent:** Use a project template like [Cookiecutter](https://cookiecutter.readthedocs.io/) to standardize your project structure.
7. **Make it easy to write tests (and write them):** Use [pytest](https://pytest.org/) to write tests. Organize your projects so that tests are easily added and can be run with a call to `pytest`.
8. **Make it easy to write docs (and write them):** Build documentation generation and publishing into your project template. Write documentation as you go.

## What Developer Tooling Can’t Do

1. **Tell you what to build:** [The hardest part of building software is figuring out what to build](https://tdhopper.com/blog/no-silver-bullet/) and developer tooling can’t solve this.
2. **Improve overall architecture of your code:** Developer tooling can help you write better code, but it mostly can’t help you design better systems.
3. **Guarantee a better product:** Developer tooling can help you catch bugs and write better code, but it can’t guarantee that your product will be successful. A great product doesn’t *require* a great codebase.
4. **Replace foundational knowledge and common sense:** I *think* even LLMs don’t replace these. `ruff` and `mypy` definitely don’t!

## Python Tools I Like in December 2024

Here is a list of tools I like in December 2024. This list is opinionated, personal, and not exhaustive.

A remarkable thing about what follows is how different it is from a list one or two years ago. The team at [Astral](https://astral.sh/) has been doing groundbreaking work in the Python tooling space with the release of [uv](https://docs.astral.sh/uv/) and [ruff](https://docs.astral.sh/ruff/). These tools have made my Python development experience better, and I’m sincerely excited about them.

### uv

[uv](https://docs.astral.sh/uv/) is a Python package and project manager that replaces pip, pip-tools, pipx, poetry, pyenv, twine, and virtualenv (at least). It is blazing fast, doesn’t depend on Python to be installed, and is rapidly getting new features. I use it to manage dependencies, build packages, and run scripts. Because uv can be installed *without* Python, it is going to be a game-changer for folks getting started with Python or just running a one-off script.

### Ruff

[Ruff](https://docs.astral.sh/ruff) is a linter and formatter that replaces black, flake8 (mostly), isort. It is also blazing fast and can automatically fix many linter issues (with the `--fix` flag). I recommend enabling editor integration for automatic formatting and using CI to enforce conformity.

### Mypy

[Mypy](https://mypy.readthedocs.io/) is a static type checker for Python. It helps catch type-related errors before runtime, improves code quality and documentation, and enhances IDE support and code completion.

Mypy can be slow for large projects and difficult to configure, especially with 3rd party libraries. Like many others, I am eagerly looking forward to an alternative type checker from Astral in the near future.

### Pytest

[Pytest](https://pytest.org/) is a testing framework that is easy to get started with (you just need a file and function prefixed with `test_`). With parameterized testing, fixtures, and plugins, Pytest enables robust testing of your code.

### Cookiecutter and Cruft

[Cookiecutter](https://cookiecutter.readthedocs.io/) is a project templating tool that generates new Python projects quickly and standardizes project structure. I love using it to automate project setup and ensure that my projects have CI integration, package building and deployment, a Makefile for common commands, pre-commit hooks, documentation generation, and linter configurations.

[Cruft](https://cruft.github.io/cruft/) is a tool that wraps Cookiecutter and allows updating existing projects with a modifications to the template.

Building and maintaining a robust template requires considerable effort. Evaluate your team’s return on investment.

### IPython

[IPython](https://ipython.org/) is an interactive Python shell that has rich features for development and exploration. Most Python developers have used it, but many only at a basic level. Take some time to read the documentation and learn its command line arguments, magic commands, and other features.

### VS Code

[VS Code](https://code.visualstudio.com/) is a powerful Python IDE with an extensive extension ecosystem. I recommend using it for Python development.

### pre-commit

[pre-commit](https://pre-commit.com/) is a tool that manages git pre-commit hooks. I recommend using it to automate code quality checks. At a minimum, I recommend running ruff and [yamllint](https://github.com/adrienverge/yamllint/blob/master/.pre-commit-hooks.yaml) (if your project has yaml, which of course it does).

### direnv

[direnv](https://direnv.net/) is a tool that automatically activates and deactivates project environments, including Python virtualenvs. It handles environment variables and project-specific settings. I recommend using it to manage your project environments. It does not yet have native support for uv, but I’m [hopeful that it will soon](https://github.com/direnv/direnv/pull/1329).

## Some Conclusions

1. Python tooling is improving rapidly. Although fragmentation can be frustrating, it points to the desire and effort of many to improve Python development.
2. Teams need to agree on tools and practices. Automation and consistency are key to team productivity and happiness.
3. Read the docs and learn your tools.
4. Don’t be afraid to try new tools.