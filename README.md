Steps to install Kubernetes dashboard in local
Install Mozilla Firefox

1. kubectl apply -f  https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
2. Create users and roles for the dashboard
   Create admin-user-service-account.yaml file with below content
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: admin-user
     namespace: kubernetes-dashboard
   Create admin-user-cluster-role-binding.yaml file with below content
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: admin-user
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: cluster-admin
    subjects:
    - kind: ServiceAccount
      name: admin-user
      namespace: kubernetes-dashboard

4. kubectl apply -f admin-user-service-account.yaml -f admin-user-cluster-role-binding.yaml
5. Create Token for user
kubectl -n kubernetes-dashboard create token admin-user
output : eyJhbGciOiJSUzI1NiIsImtpZCI6ImpvN1FxYmE5UTVReTVlUEMxNXUxVjJzQ3lyT3ZuYVZ3VnpQxxxxx
6. kubectl port-forward -n kubernetes-dashboard service/kubernetes-dashboard 8080:443

![image](https://github.com/srss-pocs/kubernetes-installation-local/assets/145287517/0f909ec6-6710-43cc-af48-893056cda662)
