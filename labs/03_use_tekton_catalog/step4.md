Step 4: Run the pipeline

You can now use the Tekton CLI (tkn) to create PipelineRun to run the pipeline.

Use the following command to run the pipeline, passing in the URL of the repository, the branch to clone, the workspace name, and the persistent volume claim name.

bash

tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git" \
	-p branch="main" \
    -w name=pipeline-workspace,claimName=pipelinerun-pvc \
    --showlog
Run
You should see output similar to this:

text

$ tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git" \
    -p branch="main" \
    -w name=pipeline-workspace,claimName=pipelinerun-pvc \
    --showlog
PipelineRun started: cd-pipeline-run-62q4r
Waiting for logs to be available...
Eventually, you should see the output from the logs.

text

[clone : clone] + '[' false '=' true ]
[clone : clone] + '[' false '=' true ]
[clone : clone] + '[' false '=' true ]
[clone : clone] + CHECKOUT_DIR=/workspace/output/
[clone : clone] + '[' true '=' true ]
[clone : clone] + cleandir
[clone : clone] + '[' -d /workspace/output/ ]
[clone : clone] + rm -rf '/workspace/output//*'
[clone : clone] + rm -rf '/workspace/output//.[!.]*'
[clone : clone] + rm -rf '/workspace/output//..?*'
[clone : clone] + test -z 
[clone : clone] + test -z 
[clone : clone] + test -z 
[clone : clone] + /ko-app/git-init '-url=https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git' '-revision=main' '-refspec=' '-path=/workspace/output/' '-sslVerify=true' '-submodules=true' '-depth=1' '-sparseCheckoutDirectories='
[clone : clone] {"level":"info","ts":1748365778.2729099,"caller":"git/git.go:170","msg":"Successfully cloned https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git @ 0105207455eb050399ed19499fecb5cad4d88db9 (grafted, HEAD, origin/main) in path /workspace/output/"}
[clone : clone] {"level":"info","ts":1748365778.334829,"caller":"git/git.go:208","msg":"Successfully initialized and updated submodules in path /workspace/output/"}
[clone : clone] + cd /workspace/output/
[clone : clone] + git rev-parse HEAD
[clone : clone] + RESULT_SHA=0105207455eb050399ed19499fecb5cad4d88db9
[clone : clone] + EXIT_CODE=0
[clone : clone] + '[' 0 '!=' 0 ]
[clone : clone] + printf '%s' 0105207455eb050399ed19499fecb5cad4d88db9
[clone : clone] + printf '%s' https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git

[lint : echo-message] Calling ESLint linter...

[tests : echo-message] Running unit tests with Jest...

[build : echo-message] Building image for https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git ...

[deploy : echo-message] Deploying main branch of https://github.com/ibm-developer-skills-network/ttwst-jhxyb-ci-cd-pipeline_js.git ...
You can always see the pipeline run status by listing PipelineRuns with:

bash

tkn pipelinerun ls
Run
You should see:

plaintext

NAME                    STARTED        DURATION   STATUS
cd-pipeline-run-62q4r   1 minute ago   32s        Succeeded
You can check the logs of the last run with:

bash

tkn pipelinerun logs --last
Run
