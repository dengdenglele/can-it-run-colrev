# Issue 1: "docker run hello-world" breaks pytest
- this prevents pytest to run correctly
- "pytest tests/1_env/docker_manager_test.py" fails
- The "docker_manager_test.py" file is causing issues and should be rewritten/corrected

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

## fix the issue gracefully

``` bash
docker ps -a
docker rm <id of hello-world container> 
# there might be multiple container of hello-world
# all of them must be deleted, before pytest can run successfully
```   

```bash
# each time 
docker run hello-world
# ... was executed, a new container will be created!
# all hello-world container must be deleted
# list all hello-world containers
docker ps -a -q --filter "ancestor=hello-world"
# delete all hello-world containers
docker rm $(docker ps -a -q --filter "ancestor=hello-world")
```

# Issue 2: "docker ps -a" gets clumped up
- also due to pytest
- each time pytest after a pytest run, a new container for will be created (deb23f81edc8)
- python with tag 3.9 and image ID deb23f81edc8
- what is docker repository "Python 3.9" used for?

``` bash
# how to cleanup
docker rm $(docker ps -a -q --filter "ancestor=deb23f81edc8")
# delete the python 3.9 image
docker rmi <image-id> 
``` 



