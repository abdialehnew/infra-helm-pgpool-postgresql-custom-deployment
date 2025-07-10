# Steps to Deploy PostgreSQL HA with Helm

## Prerequisites
- Helm is already installed on your computer.
- You are logged in to the target Kubernetes cluster.
- The `database` namespace has been created in your Kubernetes cluster (if not, create it with: `kubectl create namespace database`).
- The `values.yaml` file has been customized as needed.

## Deploy PostgreSQL HA (Install)
Run the following command to perform the initial installation:
```sh
kubectl apply -f configMaps-postgresql.yaml -f configMaps-initdbscript.yaml
```
```sh
helm install postgresql-ha \
    --set postgresql.password=password \
    --set postgresql.repmgrPassword=password \
    --set postgresql.repmgrUsername=repmgr \
    --set postgresql.repmgrDatabase=repmgr \
    bitnami/postgresql-ha -f values.yaml --namespace database
```

## Upgrade PostgreSQL HA (If Already Installed)
If you have already installed and want to update the configuration, use the following command:

```sh
helm upgrade postgresql-ha \
    --set postgresql.password=password \
    --set postgresql.repmgrPassword=password \
    --set postgresql.repmgrUsername=repmgr \
    --set postgresql.repmgrDatabase=repmgr \
    bitnami/postgresql-ha -f values.yaml --namespace database
```

## Notes
- Change the passwords and other configurations as needed for your security and environment.
- Make sure the `bitnami/postgresql-ha` chart is available in your Helm repo. If not, add it with:
  ```sh
  helm repo add bitnami https://charts.bitnami.com/bitnami
  helm repo update
  ```
