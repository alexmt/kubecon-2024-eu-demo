The repositor demonstrates how configure [Helmfile](https://helmfile.readthedocs.io) as a manifest generation tool
in Argo CD using CMP v2 feature.

Steps:

1. Install Argo CD
    ```
    kubectl create ns argocd
    kustomize build . | kubectl apply -n argocd -f -
    kubectl get secret argocd-initial-admin-secret -o=json | jq -r '.data.password' | base64 --decode
    kubectl port-forward svc/argocd-server 8080:443 -n argocd
    ```
2. Create the [Helmfile](https://helmfile.readthedocs.io) based application:
    Open the [Argo CD UI](https://localhost:8080/applications?new=%7B%22apiVersion%22%3A%22argoproj.io%2Fv1alpha1%22%2C%22kind%22%3A%22Application%22%2C%22metadata%22%3A%7B%22name%22%3A%22example%22%7D%2C%22spec%22%3A%7B%22destination%22%3A%7B%22name%22%3A%22%22%2C%22namespace%22%3A%22default%22%2C%22server%22%3A%22https%3A%2F%2Fkubernetes.default.svc%22%7D%2C%22source%22%3A%7B%22path%22%3A%22examples%2Fdeployments%2Fdev%22%2C%22repoURL%22%3A%22https%3A%2F%2Fgithub.com%2Fhelmfile%2Fhelmfile%22%2C%22targetRevision%22%3A%22HEAD%22%7D%2C%22sources%22%3A%5B%5D%2C%22project%22%3A%22default%22%7D%7D)
    and create a new application with the following details:

    * Project: default
    * Application Name: example
    * Repository URL: https://github.com/helmfile/helmfile
    * Path: examples/deployments/dev
    * Cluster URL: https://kubernetes.default.svc
    * Namespace: default


    

