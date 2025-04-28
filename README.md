# web-sample
This is base on the Red Hat tutorial: https://github.com/openshift/pipelines-tutorial<br>

# Description
The goal of this project is to provide a simple demo of working with pipeline and gitops.<br>

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
    --use-param-defaults<br>

## Enable triggers
### References
- Configure webhook
https://github.com/ebeaudoi/pipelines-tutorial#:~:text=Configure%20webhook%20manually

### Create the trigger template, bindind, the trigger and the eventlistener
- apply Triggertemplate<br>
oc create -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/03_triggers/02_template.yaml<br>

- apply TriggerBinding<br>
oc create -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/03_triggers/01_binding.yaml<br>

- apply Trigger<br>
oc create -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/03_triggers/03_trigger.yaml<br>

- create EventListener<br>
oc create -f https://raw.githubusercontent.com/ebeaudoi/web-sample/refs/heads/main/03_triggers/04_event_listener.yaml<br>

- Run the below command to expose the EventListener service as a route<br>
oc expose svc el-webserver<br>

