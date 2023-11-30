# CronJobs

Here is a collection of some use cases.

## 01_manage-cluster-resources

This use case shows how to get access to cluster resources by running commands from inside a POD:

1. copy on local filesystem and make changes to fit your needs: ```https://github.com/dedalus-enterprise-architect/ea-k8s-resources/blob/main/cronjob/01_manage-cluster-resources.yaml```

2. before doing anything, you must customize the following placeholders:
    * replace the "_@namespace@_" with the namespace where the objects will be stored into
    * replace the "_@application\_name@_" with the target application name
    * modify the script section: "spec.jobTemplate.spec.template.spec.containers.['sa-@application_name@-run-command']" to fit your needs
    * look for the comments labelled with: "::: WARNING :::" inside the manifest and configure the directives where needed

3. create the object in the cluster with the following command adding the correct namespace as a parameter:

        kubectl apply -f 01_manage-cluster-resources.yaml -n @namespace@

4. you can trigger manually the cron job with the following command after replacing all the placeholders:

        kubectl create job --from=cronjob/sa-@application_name@-utility-cronjob @application_name@-utility-cronjob-manual-001 -n @namespace@

## 02_run-command-vs-pvc

This use case show how to get access to cluster resources by running commands from inside a POD:

1. copy on local filesystem and make changes to fit your needs: ```https://github.com/dedalus-enterprise-architect/ea-k8s-resources/blob/main/cronjob/02_run-command-vs-pvc.yaml```

2. before doing anything, you must customize the following placeholders:
    * replace the "_@application\_name@_" with the target application name
    * replace the "_@type\_here\_pvc\_name@_" with the PVC name you want access to
    * replace the "_@type\_here\_pvc\_claim\_name@_" with the name of the PVC claim you want access to
    * modify the script section: "spec.jobTemplate.spec.template.spec.containers.['@application_name@-run-command']" to fit your needs
    * look for the comments labelled with: "::: WARNING :::" inside the manifest and configure the directives where needed

3. create the object in the cluster with the following command adding the correct namespace as a parameter:

        kubectl apply -f 02_run-command-vs-pvc.yaml -n @namespace@

4. you can trigger manually the cron job with the following command after replacing all the placeholders:

        kubectl create job --from=cronjob/@application_name@-utility-cronjob @application_name@-utility-cronjob-manual-001 -n @namespace@