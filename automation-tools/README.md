# Automation Tools

It follows the sub-projects

## run-command-by-cronjob

This sub-project aims is how to get access to cluster objects from a POD by running a command:

1. copy on local path and edit the file below, adjusting as needed: ```https://github.com/dedalus-enterprise-architect/ea-k8s-resources/blob/main/automation-tools/run-command-by-cronjob.yaml```

1. before doing anythings, you must customize the following placeholders by your settings:
    * replace the "_@namespace@_" by the namespace where the objects will be stored in.
    * replace the "_@application_name@_" by the _application_name_ which you are working on.
    * adjust the script section: "spec.jobTemplate.spec.template.spec.containers.['run-command']" to fit your needs
    * check the warning on the manifest and do the action required

1. create the object in the cluster applying the yaml file just created, but before proceed set the correct namespace inline:

        kubectl apply -f https://raw.githubusercontent.com/dedalus-enterprise-architect/ea-k8s-resources/main/automation-tools/run-command-by-cronjob.yaml -n @namespace@

1. run manually the cron by the following command:

        kubectl create job --from=cronjob/type_here_you-cronjob-name type_here_you-cronjob-name-manual-001 -n @namespace@

but before runs, the command must be adjusted the placeholders by your own settings.
