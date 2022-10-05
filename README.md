## Welcome to Oferta Maker

[![Tests](https://github.com/access55/oferta_maker/workflows/tests/badge.svg)](https://github.com/access55/oferta_maker/actions)
[![Python](https://img.shields.io/badge/python-3.8-green)](https://www.python.org)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![localstack](https://img.shields.io/badge/localstack-0.12.6.1-yellow)](https://github.com/localstack/localstack)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)

Oferta Maker

### Project Requirements

* [Python3.8](https://www.python.org)
* [Docker](https://www.docker.com)
* [Poetry](https://python-poetry.org/)

### Pre-Requisites

```shell
# Install pre-requisites (this command works on Ubuntu 20.04, please check for another OS)
$ sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git

# Pyenv (optional, but recommended)
$ curl https://pyenv.run | bash
# Open .bashrc file and add the 3 lines below. Then restart terminal:
    export PATH="/home/$USER/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
$ pyenv install 3.8.7 # if you do not have python installed yet.
$ pyenv global 3.8.7

# Poetry
$ curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
$ source $HOME/.poetry/env

# Docker
# New installation
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
$ sudo usermod -aG docker $USER # then restart bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
# On older installations, please make sure you have the latest version (20+)
# as per https://docs.docker.com/engine/install/ubuntu/
```

### Configure

This project organizes your settings in this way:

* Project **settings** (all non-sensible information) is stored in
  `pyproject.toml`
* Project **credentials** (all sensible info) is stored in `.env` file.

Please copy (do not rename) `.env.credentials` to `.env` file:

```shell
$ cd /path/to/oferta_maker
$ cp .env.credentials .env
```

### Build

Use the following commands to install or reinstall Project.

##### Build in VSCode:

* [https://code.visualstudio.com/docs/remote/containers](https://code.visualstudio.com/docs/remote/containers)

1. Please install the following VS Code extensions:

* Remote Development
* Python
* Docker
* Django

2. On HOST Terminal, run

```bash
$ cd /path/to/oferta_maker
$ make install
$ docker-compose build
```

3. On command-palette select "**Remote-Containers: Rebuild and Reopen in
   Container**"

### Migrate

##### Migrating Database in VSCode:

* [https://code.visualstudio.com/docs/remote/containers#_opening-a-terminal](https://code.visualstudio.com/docs/remote/containers#_opening-a-terminal)

1. On menu Terminal, click "New Terminal"
2. Type command `make migrate` or `python manage.py migrate` (both are
   equal)

##### Populate Database with necessary data to sistem proper function
* [DB_QUICKSTART.md](.documentation/DB_QUICKSTART.md)


### Test

##### Testing in VSCode:

* [https://code.visualstudio.com/docs/python/testing#_enable-a-test-framework](https://code.visualstudio.com/docs/python/testing#_enable-a-test-framework)

1. On command-palette select "**Python: Configure Tests**" .
2. Select framework **Pytest** and base folder **client_manager**
3. Click "**Run Tests**"


### Run Application

##### Running in VSCode:

* [https://code.visualstudio.com/docs/editor/debugging#_launch-configurations](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations)

1. On *Activity Bar*, click the "**Run**" button.
2. To run **Django**, please select "Python:Django" and click Play.
3. To run **Celery**, please select "Python:Celery" and click Play.

### Project Links

The links below works when you're running the App via docker. For Django
based authentication, please define your local superuser using the
[createsuperuser](https://docs.djangoproject.com/en/2.2/intro/tutorial02/)
command.

| Page                | Address                                                                          | Use                         | Authenticated  |
|:--------------------|:---------------------------------------------------------------------------------|:----------------------------|:---------------|
| Swagger UI          | [http://localhost:8001/swagger](http://localhost:8001/api/swagger)           | API Documentation (Swagger) | Yes (Django)   |
| Redoc UI            | [http://localhost:8001/redoc](http://localhost:8001/api/redoc)               | API Documentation (Redoc)   | Yes (Django)   |
| DRF Browser Example | [http://localhost:8001/api/health](http://localhost:8001/api/health)             | DRF Documentation           | No             |
| Django Admin        | [http://localhost:8001/admin](http://localhost:8001/admin)                       | Django Admin                | Yes (Django)   |


### Lint and Format Code

This Project is linted using [Pre-Commit](https://pre-commit.com/)
configured with the following packages:

* [Bandit](https://bandit.readthedocs.io/en/latest/)
* [Black](https://black.readthedocs.io/en/stable/?badge=stable)
* [iSort](https://github.com/PyCQA/isort)
* [Pylint](https://www.pylint.org/)

When possible we are using the default options for these tools. Per
based project exceptions are handled in `pyproject.toml` and
`.pylintrc` files.

Make sure you have resolved all *Bandit*, *Pylint*, *iSort* and *Black*
issues before upload code to Github. The CI/CD process will check all.
To run the tools:

1. Open *VSCode Terminal* and type `make pre-commit`

##### Linting and Format in VSCode:

* [https://marcobelo.medium.com/setting-up-python-black-on-visual-studio-code-5318eba4cd00](https://marcobelo.medium.com/setting-up-python-black-on-visual-studio-code-5318eba4cd00)
* [https://code.visualstudio.com/docs/python/linting](https://code.visualstudio.com/docs/python/linting)

1. Use the Console "Problems" tab to see Pylint issues
2. Run "Open Settings (UI)" and search for "Format on Save". Mark the
   "Editor: Format on Save" option.
3. Search for "Python Formatting Provider" and in "Python > Formatting:
   Provider" select "black".

### Open a Shell (Terminal)

##### Open VSCode Terminal:

* [https://code.visualstudio.com/docs/remote/containers#_opening-a-terminal](https://code.visualstudio.com/docs/remote/containers#_opening-a-terminal)

1. On menu Terminal, click "New Terminal"

##### Terminal Commands available inside Container:

```shell
$ make update       # update poetry.lock
$ make test         # run pytest
$ make lint         # run pre-commit, unit tests and coverage
$ make format       # run Black
$ make bandit       # run Bandit
$ make pylint       # run Pylint
$ make pre-commit   # run Pre-Commit
$ make migrate      # run python manage.py migrate
$ make migrations   # run python manage.py makemigrations
```

### Add/Removing Dependencies

To add or remove project dependencies:

1. Modify the `pyproject.toml` file with the dependency alterations
2. Open *VSCode terminal* and type `make migrate`
   (it's an alias for the `poetry update` command). This command will
   update the `poetry.lock` file.
3. On VSCode select the "**Rebuild Container**" command. On HOST
   terminal, type `docker-compose build`. Make sure the `poetry.lock` is
   updated before running this command.

#### Example

Open the `pyproject.toml` file to add *my_awesome_lib* dependency:

```toml
[tool.poetry.dependencies]
my_awesome_lib = "*"
```

Always select the latest version, using `"*"`. But if you need to pin a
version, please add a comment with the reason:

```toml
[tool.poetry.dependencies]
my_awesome_lib = "<1.2.3"  # reason: Because github issue #123
```

After edit `pyproject.toml` open your Terminal and type:

```shell
# Alias for "poetry update", this command will work too.
$ make update
```

This command will update the `poetry.lock`, pinning the latest
compatible version for this dependency.

After that, on **VSCode**, select the command "**Rebuild Container**" or
in *HOST Terminal*, type `docker-compose build`


### Docker without VSCode

If you don`t have access to an *VSCode terminal*, you need to use your
*HOST terminal* to run docker commands. The commands below are the
docker equivalent for the operations above. Do not use this commands on
*VSCode terminal*, they will not work inside container.

```shell
# Install Project (docker)
$ docker-compose build

# Migrate inside container
$ docker-compose -f docker-compose.yml -f docker-compose.ops.yml up migrate

# Run App in docker
$ docker-compose up -d

# Running tests in docker
$ docker-compose -f docker-compose.yml -f docker-compose.ops.yml up --build test

# Run Lint in docker
$ docker-compose -f docker-compose.yml -f docker-compose.ops.yml up --build lint

# Open terminal in docker
$ docker-compose run --rm --entrypoint "" api sh
```

### Using Virtualenv

If you need to run a virtualenv environment for this project, you can
use the following helper commands:

```shell
# The .env file described above configure the postgres inside docker-compose.
# If you want to use another database, make sure your .env configuration
# points to a ready database (host, port, user, password, etc...)

# Install Project (virtualenv)
$ cd /path/to/client_manager
$ make install

# Migrating in virtualenv
# DB_NAME=postgres
# DB_USER=postgres
# DB_PASSWORD=postgres
# DB_HOST=localhost
# DB_PORT=5433
$ docker-compose up -d db
$ make migrate

# Running tests in virtualenv
$ make vtest

# Running all CI tests in virtualenv
$ make vlint

# Run App in virtualenv
$ make develop

# Open terminal in virtualenv (.env loaded)
$ make shell
```

### Project documentation/diagrams
* Precification Workflow Sequence Diagram: [PRECIFICATION_WORKFLOW_SEQUENCE_DIAGRAM.MD](.documentation\PRECIFICATION_WORKFLOW_SEQUENCE_DIAGRAM.MD)
* Offer Class Diagram: [OFFER_CLASSES_CLASS_DIAGRAM.MD](.documentation\OFFER_CLASSES_CLASS_DIAGRAM.MD)
* PricerMachine Class Diagram: [PRICER_MACHINE_CLASS_DIAGRAM.MD](.documentation\PRICER_MACHINE_CLASS_DIAGRAM.MD)
* ClientValidator Class Diagram: [CLIENT_VALIDATOR_CLASS_DIAGRAM.MD](.documentation\CLIENT_VALIDATOR_CLASS_DIAGRAM.MD)
