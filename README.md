# flake8-github-action
A Github Action that runs a [flake8](https://flake8.pycqa.org/en/latest/index.html) check on a pull request and leaves a comment on your pull request.

## Example

Create `.github/workflows/flake8.yml`:
```
on: [pull_request]
name: Python Flake8 Check
jobs:
  flake8:
    name: flake8
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: flake8
      uses: konciergeMD/flake8-github-action@main
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        #PRECOMMAND_MESSAGE: You have style errors. See them below.
        #FLAKE8_CONFIG: ./.github/workflows/flake8_config  # Optional flake8 config file.
        #FLAKE8_OPTS: "-v"  # additional flake8 options
```
* `PRECOMMAND_MESSAGE` - if you set it, it will print before
the code errors. For example, this is helpful if you want to print a message to refer the user
to any tools you have for managing style errors.
* `FLAKE8_CONFIG` - path to the [flake8](https://flake8.pycqa.org/en/latest/user/configuration.html) compatible configuration file. Flake8 uses `.flake8` in
  the root of your repository by default, good start is to use:
```
[flake8]
ignore = E501,W503
exclude = .git,__pycache__
```
* `FLAKE8_OPTS` - in case you don't want to use the `flake8` configuration file, use this variable to set additional `flake8` options, like `--verbose`, etc.

