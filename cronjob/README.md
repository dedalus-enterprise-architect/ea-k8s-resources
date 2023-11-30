# CronJobs

It follows a collection of some uses cases.

## 01_manage-cluster-resources

This use's case aims is how to get access to cluster resources by running commands from inside a POD:

1. copy on local filesystem and make changes that fit your needs: ```https://github.com/dedalus-enterprise-architect/ea-k8s-resources/blob/main/automation-tools/01_manage-cluster-resources.yaml```

1. before doing anythings, you must customize the following placeholders by your settings:
    * replace the "_@namespace@_" by the namespace where the objects will be stored in.
    * replace the "_@application\_name@_" by the application n ame you want work on.
    * adjust the script section: "spec.jobTemplate.spec.template.spec.containers.['sa-@application_name@-run-command']" to fit your needs
    * look for the comments labeled with: "::: WARNING :::" inside the manifest and if any, configure the directives as you want

1. create the object in the cluster applying the yaml file just created, but set the correct namespace before execute the following command:

        kubectl apply -f https://raw.githubusercontent.com/dedalus-enterprise-architect/ea-k8s-resources/main/automation-tools/01_manage-cluster-resources.yaml -n @namespace@

1. you can trigger manually the cron job but replace all the placeholders before execute the following command:

        kubectl create job --from=cronjob/sa-@application_name@-utility-cronjob @application_name@-utility-cronjob-manual-001 -n @namespace@

## 02_run-command-vs-pvc

This use's case aims is how to get access to cluster resources by running commands from inside a POD:

1. copy on local filesystem and make changes that fit your needs: ```https://github.com/dedalus-enterprise-architect/ea-k8s-resources/blob/main/automation-tools/02_run-command-vs-pvc```

1. before doing anythings, you must customize the following placeholders by your settings:
    * replace the "_@application\_name@_" by the application name you want work on.
    * replace the "_@type\_here\_pvc\_name@_" by the name of the PVC you want access to.
    * replace the "_@type\_here\_pvc\_claim\_name@_" by the name of the PVC claim you want access to.
    * adjust the script section: "spec.jobTemplate.spec.template.spec.containers.['@application_name@-run-command']" to fit your needs
    * look for the comments labeled with: "::: WARNING :::" inside the manifest and if any, configure the directives as you want

1. create the object in the cluster applying the yaml file just created, but set the correct namespace before execute the following command:

        kubectl apply -f https://raw.githubusercontent.com/dedalus-enterprise-architect/ea-k8s-resources/main/automation-tools/02_run-command-vs-pvc -n @namespace@

1. you can trigger manually the cron job but replace all the placeholders before execute the following command:

        kubectl create job --from=cronjob/@application_name@-utility-cronjob @application_name@-utility-cronjob-manual-001 -n @namespace@