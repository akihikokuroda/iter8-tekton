# iter8-tekton

##pre-condition:

1.One version of the app installed.
1. Istio gateway for the app is setup

##Step:

###Manual step:

1.update the app to respond slowly
1.create a pull request

###Event listener execute a pipeline:

1.pipeline - build/ push app (existing task -pipeline hotel)
1.pipeline - deploy app (existing task - pipeline hotel)
1.pipeline - create iter8 experiment (new catalog task)
1.wait for experiment completion (new catalog task)

###Experiment fails:

1.delete the new deployment (new catalog/sample task)
1.add comment and change the pull request status (existing catalog task)
1.send a slack message (existing catalog task)

###Manual:

1.update the app to respond faster
1.push the update

###Event listener execute a pipeline:
(same as above)

###Experiment success:

1.change the pull request status (existing catalog task)
1.merge the pull request (existing catalog task)
1.delete the original deployment (new catalog/sample task)
1.send a slack message (existing catalog task)