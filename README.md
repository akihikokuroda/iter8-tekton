# iter8-tekton

## Files:

- init.yaml: create demo(kabanero) namespace and the service for the demo project
- auth.yaml: create github and dockerhub credential secret

- eventlistener.yaml: event listener executes simple-pipeline on the github pull request.

- simple-pipeline.yaml: pipeline executes build, test and deploy.

- build-task.yaml: task builds the project and push the image to the repository.
- deploy-task.yaml task deplpys the project deployment
- create-experiment.yaml: task creates the experiment resource for A/B testing
- generate-load.yaml: task generates loads to the testing target
- wait-experiment.yaml: task waits the completion of the A/B testing and generates the results
- notify.yaml: task sends the result event to the post process event listener

- dispatch-event.yaml: event listener and pipeline execute the post process tasks

## Tasks from tektond/catalog

- https://github.com/tektoncd/catalog/tree/master/github
- https://github.com/tektoncd/catalog/tree/master/mail
- https://github.com/tektoncd/catalog/tree/master/slackmessage

## Sample demo project

- https://github.com/akihikokuroda/iter8-demo

## Front demo project

- https://github.com/akihikokuroda/iter8-front

## pre-condition:

1. Tekton pipeline, triggers installed
1. Istio installed
1. Iter8 installed
1. Namespace with Istio proxy auto injection enabled created (init.yaml)
1. One version of the project installed.
1. Service for the project created (init.yaml)
1. The front application that sends the requst to the demo porject installed (https://github.com/akihikokuroda/iter8-front)
1. Tekton resources for this demo (task, pipeline, eventlistener, triggerbindings, triggertemplates) installed
1. Hooks in the demo github repository created.

## Step:

### Manual step:

1. update the app to respond slowly
1. create a pull request

### Event listener execute a pipeline:

1. pipeline - build/ push app (existing task -pipeline hotel)
1. pipeline - deploy app (existing task - pipeline hotel)
1. pipeline - create iter8 experiment (new catalog task)
1. wait for experiment completion (new catalog task)

### Experiment fails:

1. delete the new deployment (new catalog/sample task)
1. add comment and change the pull request status (existing catalog task)
1. send a slack message (existing catalog task)
1. send an email

### Manual:

1. update the app to respond faster
1. push the update

### Event listener execute a pipeline:
(same as above)

### Experiment success:

1. change the pull request status (existing catalog task)
1. delete the original deployment (new catalog/sample task)
1. send a slack message (existing catalog task)
1. send an email