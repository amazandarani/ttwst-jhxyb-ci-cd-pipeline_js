Step 1: Add the git-clone task

You start by finding a task to replace the checkout task you initially created. While it was OK as a learning exercise, it needs a lot more capabilities to be more robust, and it makes sense to use the community-supplied task instead.

You can browse the Tekton Catalog, find the git-clone yaml file, copy the URL to the yaml file, and use kubectl to apply it manually.

The git-clone task is part of the Tekton Catalog and is indexed on Artifact Hub for discovery. You can install the task using either of the following options.

Option 1: Discover via Artifact Hub and apply the raw manifest

bash

kubectl apply -f https://github.com/tektoncd/catalog/raw/main/task/git-clone/0.10/git-clone.yaml
Run
Option 2: Install directly from the Tekton Catalog

Artifact Hub indexes tasks from the official Tekton Catalog hosted on GitHub. You can install the same task directly from the source repository:

bash

kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.9/git-clone.yaml
Run
Both options install the git-clone task into your cluster under the currently active namespace.

Verify the installation

After installation, confirm that the task is available:

bash

kubectl get task git-clone
Run
You should see the git-clone task listed in the output.