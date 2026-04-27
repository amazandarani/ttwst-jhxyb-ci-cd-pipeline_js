Step 4: Start a PipelineRun

Now it is time to call the event listener and start a PipelineRun. You can do this locally using the curl command to test that it works.

For this last step, you will need two terminal sessions.

Terminal 1

In one of the sessions, you need to run the kubectl port-forward command to forward the port for the event listener so that you can call it on localhost.

Use the kubectl port-forward command to forward port 8090 to 8080.

bash

kubectl port-forward service/el-cd-listener  8090:8080
Run
You will see the following output, but you will not get your cursor back.

plaintext

Forwarding from 127.0.0.1:8090 -> 8080
Forwarding from [::1]:8090 -> 8080
Terminal 2

Now you are ready to trigger the event listener by posting to the endpoint that it is listening on. You will need to open a second terminal shell to issue commands.

Open a new Terminal shell wtih the menu item Terminal > New Terminal.

Use the curl command to send a payload to the event listener service.

bash

curl -X POST http://localhost:8090 \
  -H 'Content-Type: application/json' \
  -d '{"ref":"main","repository":{"url":"https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js"}}'
Run
This should start a PipelineRun. You can check on the status with this command:

bash

tkn pipelinerun ls
Run
You should see something like this come back:

plaintext

NAME                    STARTED          DURATION   STATUS
cd-pipeline-run-lzxth   25 seconds ago   ---        Running
You can also examine the PipelineRun logs using this command (the -L means "last" so that you do not have to look up the name for the last run):

bash

tkn pipelinerun logs --last
Run
You should see:

plaintext

[clone : checkout] Cloning into 'ttwst-jhxyb-ci-cd-pipeline_js'...

[lint : echo-message] Calling ESLint linter...

[tests : echo-message] Running unit tests with Jest...

[build : echo-message] Building image for https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js ...

[deploy : echo-message] Deploying main branch of https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js ...
