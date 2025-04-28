# web-sample

# Description
The goal of this project is to provide a simple demo of working with pipeline and gitops.

# Steps to deploy pipelinewe
## Deploy the tasks
oc apply -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/01_pipeline/01_apply_manifest_task.yaml<br>
oc apply -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/01_pipeline/02_update_deployment_task.yaml<br>
## Deploy the pipeline
oc apply -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/01_pipeline/04_pipeline.yaml<br>
 <br>

## tart a pipeline to build and deploy 
tkn pipeline start build-and-deploy \
    --prefix-name build-deploy-api-pipelinerun \
    -w name=shared-workspace,volumeClaimTemplateFile=https://raw.githubusercontent.com/ebeaudoi/pipelines-tutorial/refs/heads/master/01_pipeline/03_persistent_volume_claim.yaml \
    -p deployment-name=webserver \
    -p git-url=https://github.com/ebeaudoi/web-sample.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/pipelines-tutorial/webcolor \
    --use-param-defaults
