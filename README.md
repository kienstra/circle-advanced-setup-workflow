# Path filtering on CircleCI

Forked from [circle-makotom/circle-advanced-setup-workflow](https://github.com/circle-makotom/circle-advanced-setup-workflow).

[Makoto Mizukami](https://github.com/circle-makotom) gets all of the credit for the CircleCI® configs, and the entire concept of this repo.

The main change is making the module directories organized by language, like `js/` and `php/`, and adding very basic examples in them.

This is similar to how WordPress plugins can look.

The great thing about Makoto's idea here is that jobs only run when there's a certain diff.

For example, if there's no `.php` file in the diff, the PHPUnit tests won't run.

And if the PR only changes the `README.md`, no dynamic jobs will run.

This repository demonstrates an advanced use case of setup workflow feature on CircleCI. For instance, it implements both path filtering and config splitting.

## How does it work?

1. CircleCI triggers the setup job `Create dynamic jobs`, defined in [.circleci/config.yml](.circleci/config.yml).
2. That job finds which file types were changed in the current branch versus the [main](https://github.com/kienstra/circle-advanced-setup-workflow/tree/main) branch.
3. It emits those changed file types as pipeline parameters.
4. [.circleci/workflow.yml](.circleci/workflow.yml) receives those pipeline parameters.
5. Those determine whether to run the jobs for [php/](php/), [js/](js/), and [e2e/](e2e/).
