# Deploy MLX Prow Bot on IBM Cloud

The MLX Prow Bot deployment is a modified version based on the [Prow s3 starter](https://github.com/kubernetes/test-infra/blob/master/config/prow/cluster/starter-s3.yaml) for IBM Cloud. Please follow the below instrctions to deploy/update the MLX Bot.

1. Update the credentials under the `prow-parameters` section in [kustomize/kustomization.yaml](kustomize/kustomization.yaml). The Bot credentials are located within the internal team's MLX folder.

2. Once the credentials are updated, modify any configuration within [kustomize/prow-ibm-cloud.yaml](kustomize/prow-ibm-cloud.yaml) if necessary. Then, run the following commands to deploy the MLX Prow Bot on an IBM Cloud Kubernetes Cluster.
```shell
kubectl apply -k kustomize
```

3. As the MLX admin, please update the [MLX Github Webhook](https://github.com/organizations/machine-learning-exchange/settings/hooks) to the following
```
Payload URL: https://$(prow-ingress)/hook
Content type: application/json

Secret: $(hmac-token) in manifests

SSL verification: Enable
Which events would you like to trigger this webhook?: Send me everything.
```
