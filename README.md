# Task

Two python applications have conflicting dependencies and should be installed in a way that:

* the locked dependencies are used per application
* a global command is available for running each application

# Solution

Each application is installed by `poetry install`. This makes sure:

* locked dependencies are used
* each application is isolated in its own virtual environment

Each application must provide a scripts entrypoint as described in https://python-poetry.org/docs/pyproject/#scripts

During `poetry install` this script entrypoint is placed into the `bin` folder of the virtual environment.

In general there are multiple ways to run these entrypoints.

* activate the venv (`poetry shell` or `source /path/to/venv/bin/activate`) and call the entrypoint
* use `poetry run app1`
* call the generated script in the `bin` folder by full path e.g. `/path/to/venv/bin/app1`

The last way shows us an opportunity for the second requirement of the task: making the command global available

By adding the full path to the `PATH` environment variable, we extend the search path for an executable.

`export PATH=$PATH:/path/to/app1/venv/bin:/path/to/app2/venv/bin`

(Replace `/path/to/app1/venv/bin` and `/path/to/app2/venv/bin` with the correct pathes)

Now we can call `app1` or `app2` from everywhere.