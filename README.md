# Multiple vllm replicas with Podman Compose

Motivation: There are numerous scenarios under which we cannot run a kubernetes distribution and would still need multiple replicas.

## Requirements

- podman
- podman-compose
    - Setup with pip install podman-compose

## Setup

1. Run 
```
bash prep_env.sh
```

2. Run
```
podman-compose up
```
Note: Untested with "podman compose"

### Known Issues

1. "depends-on" in podman-compose currently does not honor the condition field [Issue: #866](https://github.com/containers/podman-compose/issues/866). For example, in the following config:
```
depends_on:
      vllm:
        condition: service_healthy
```
podman-compose would launch the dependant service as soon as the required service is started.
Workaround: Run init-model service alone first to setup the model. 
<!-- TODO: Potentially move init-model into its own compose.yaml -->
2. Currently tested only on Nvidia GPUs
