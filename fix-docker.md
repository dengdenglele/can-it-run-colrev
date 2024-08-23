# "pytest tests/1_env/docker_manager_test.py" fails

The "docker_manager_test.py" file is causing issues and should be rewritten/corrected

## Issue

When any docker container is running and/or docker image is installed, "pytest tests/1_env/docker_manager_test.py" will fail

## Systems where the issue occured

- Ubuntu 24.04 on bare metal, Python 3.12, Pip 24
- Debian 12 on bare metal, Python 3.11, Pip 23

## Reproduce the problem

Assuming colrev is running correctly in a venv and "pip install -e .[dev,docs]" was executed successfully

```bash
docker run hello-world
# inside colrev directory (with venv) run
pytest tests/1_env/docker_manager_test.py 
```

## The following is a temporary solution ("eliminating symptoms" but does not address the cause)

Use cautiously!!! The following actions cannot be undone.

``` bash
# stop all containers
docker stop $(docker ps -aq)
# remove all containers
docker rm $(docker ps -aq)
# force remove all docker images
docker rmi -f $(docker images -q)
```

## Run "pytest tests/1_env/docker_manager_test.py" again and check for errors

```bash
# inside colrev directory (with venv) run
pytest tests/1_env/docker_manager_test.py 
```
