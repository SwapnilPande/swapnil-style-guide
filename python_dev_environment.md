# Python Style Guide
The following document outlines my style guide for Python development. The core of this style is the Google Style Guide for Python. However, this extends the Google guide to include a standard for package managers, source control, testing, and more. 

One of the key tenets of this style guide is to minimize the friction of the development environment. Obviously, this means standardizing syntax using auto-formatters, linting code, auto-generating docs, etc. However, this also means minimizing the effort of spinning up a new project. Often times, powerful solutions such as CI/CD environments that handle auto-formatting and testing are overkill for small-to-medium sized projects. Without standards defined for these, I often find myself neglecting good practices completely, resulting in untested and unstable code. ***The complexity of the development environment should scale with the complexity of the project***

## Syntax
I fully adopt the [Google Style Guide](https://google.github.io/styleguide/pyguide.html) for syntax style. 

According to the style guide, I use the [Black](https://github.com/psf/black) auto-formatter for syntax formatting. 

## Package Managers
I use conda for my package manager. General guidelines:
* Where possible, install drivers WITHIN a conda environment. For example, Nvidia drivers needed for torch should always be installed within the conda enviroment
* Always commit the yaml file associated with a project to the source control

***Self-Check Trigger*** : Using a Conda environment within a docker container
***Why is this a trigger***: While this is not explicitly problematic, nesting these two environment management tools often indicate that I am being lazy or taking some shortcut.
***What to do***: Step back and ask what is the reason for doing this. Again, this is not an explicitly bad thing to do, but it should not be done without reason. If there is a strong justification, continue. Else, either eliminate either docker or conda from the workflow.

### Small and Medium Projects
It is often not necessary to create a conda environment specific to a small project. I maintain a couple of base environments that include necessary packages for most projects, simply use one of these.

### Medium and Large Projects
Larger projects should maintain a separate environment to isolate its own dependencies. Create a conda environment from scratch and only install the minimum set of dependencies. Avoid, when possible, copying an existing environment and adding additional dependencies to reduce bloat from unnecessary dependencies.


## Logging


## Handling Arguments
I use [Click](https://click.palletsprojects.com/en/8.1.x/) for command line arguments


## Testing Code
While I want to say that all code should be tested, it is unrealistic to enforce that. Often, trying to enforce code leads to inertia in starting that effort, often leading to _no_ code being tested. Therefore, my philosophy on testing is:
* Any testing is better than no testing
* Whenever code feels hard to write, it should be tested
* Almost all code for large projects should be tested

That being said, testing in Python is especially critical due to the error prone nature of Python's typing. Numpy, for example, will automatically broadcast dimensions of matrices (a powerful tool), which can also lead to silent runtime errors that are challenging to diagnose. 


### Small Projects
For small projects, almost all testing should be manual. Extensive testing frameworks will often only slow down projects. Adhere to the following guidelines:
* Use assert statements where possible to check dimensions, types, logic, etc.
* In files for class and library definitions, write a small main (guarded by `if __name__ == __main__`), for unit tests
* ***Do not delete tests after validating code***

### Medium Projects

### Large Projects

## Debuggers

## Text Editor/IDE
I develop in VSCode. Below is a link to all of the extensions I use for Python development.

## Configuring this environment

## Other Notes
* Use type hints everywhere possible
