# prefect-google-trends
A data workflow fetching and creating google trends reports based on keywords. This workflow is automated by Prefect

## Prerquisites
See `requirments.txt`
Running
```bash
pip install -r requirements.txt
```

## Setup Prefect cloud API in the local environment
Prefect API needs to be setup in the local environment to communicate and interact with the Prefect cloud from the local environment
- Go to [Prefect cloud](https://app.prefect.cloud/) and create an account
- Create an API key in the Prefect Cloud
- Create a workspace in the Prefect Cloud (e.g. datacollection)
- In the local enviroment:
Use the ```prefect cloud login`` command to log into Prefect Cloud from the local environment, using the API key generated previously
```bash
prefect cloud login --key xxx_xxxxxxxxx
```
## Executing
-Create a Docker block named google-trends for executing the flow run on the Docker environment
-In the local environment:
```bash
# Building a deployment for a flow executed on the docker environment:
prefect deployment build src/main.py:create_pytrends_report -n google-trends -ib docker-container/google-trends -o prefect-docker-deployment -q test
# Applying  the created deployment file
prefect deployment apply prefect-docker-deployment.yaml
# Start an agent to pcikup a deployed flow run and execute
prefect agent start -q 'test'
```
