"# lastnotes.in" 
# kubernets-dashboard
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
    4  kubectl get pods -n kubernetes-dashboard
    5  kubectl get all -n kubernetes-dashboard
    6  kubectl edit service/kubernetes-dashboard -n kubernetes-dashboard
    Change the type to NodePort from ClusterIP
    7  kubectl get all -n kubernetes-dashboard

----
Below the sa.yml file is given
     
     cat sa.yml 


    apiVersion: v1
    kind: ServiceAccount
    metadata:
      labels:
        k8s-app: kubernetes-dashboard
      name: viewuser1
      namespace: kubernetes-dashboard  

---
     
    kubectl create -f sa.yml 
  
     sudo kubectl get serviceaccount -n kubernetes-dashboard
  
    cat cb.yml 
    apiVersion: rbac.authorization.k8s.io/v1beta1
    kind: ClusterRoleBinding
    metadata:
      name: kubernetes-view
      labels:
        k8s-app: kubernetes-dashboard
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: view
    subjects:
    - kind: ServiceAccount
      name: viewuser1
      namespace: kubernetes-dashboard

    296  sudo kubectl create -f cb.yml 
    
    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep viewuser1 | awk '{print $1}')
