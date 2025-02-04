## Kubernetes Commands

- **View current namespace**:
  ```bash
  > kubectl config view --minify --output 'jsonpath={..namespace}'
  ```
- **Get all common resources (pods, replicaset, deployment, configmap, volume, secret service, virtualserver, certificaterequest)**:
  ```bash
  > kubectl get all
  > kubectl get <resource-type>
  ```
- **Get details information of the resources**:
  ```bash
  > kubectl describe <resource-name> <resource-type>
  ```
- **Create configmap from a local yml file (for non-senstive data)**:
  ```bash
  > kubectl create configmap <configmap-name> --from-file=/file/path/<file-name>.yml
  ```
- **Create secret from .env (for sensitive data)**:
  ```bash
  > kubectl create secret generic <secret-name> --from-env-file=.env
  ```
- **First time deployment or update deployment yml settings**:
  ```bash
  > kubectl apply -f <deployment-folder>
  ```
- **Delete specificed resource**:
  ```bash
  > kubectl delete <resource-name> <resource-type>
  ```
- **Scale a replicaset to 3**:
  ```bash
  > kubectl scale --replicas=3 rs/<resource-name>
  ```
- **Delete all instances of a deployment (Useful to temporary disable the pods)**:
  ```bash
  > kubectl scale deployment <deployment-name> --replicas 0
  ```
- **Horizontal pod autoscaling when cpu hits 90% usage**:
  ```bash
  > kubectl autoscale deployment/<deployment-name> --min=2 --max=3 --cpu-percent=90
  ```
- **Restart a deployment (Can be used to deploy a new version when docker image got updated)**:
  ```bash
  > kubectl rollout restart deployment <deployment-name>
  ```
- **Check logs with timestamps on a specific pod**:
  ```bash
  > kubectl logs <pod-name> --timestamps
  ```
- **Continuously display the latest 100 lines of logs on all pods of same deployment**:
  ```bash
  > kubectl logs -l app=<deployment-name> --tail=100 --follow
  ```