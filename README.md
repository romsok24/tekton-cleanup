## Goal
The code wiil let you delete not used Tekton pipelinerun CRD kubernetes objects in the given namespace
## Usage
 - just to list Tekton pipelineruns:
```
docker run -it --rm -it -v ~/.kube/config:/config:ro --network host tkn:0.1 pipelinerun list --kubeconfig /config -n <the_NS-with_yourpipelineruns> 
```
 - to schedule a k8s cronjob that will automatically run and deleten the Tekton pipelinerun objects:

```
docker build -t <your_local_tag> .
docker tag <your_local_tag> <your_docker_reg_tag>
kubectl -f apply tekton-cleanup.yaml
```
  This will keep deleting all objects older than *n* weeks, where *n* can be defined in ```tekton-cleanup.yaml``` file. Default value of *n* is 5. The deletion process will reoocur at the schedule defined also in the ```tekton-cleanup.yaml``` file.
