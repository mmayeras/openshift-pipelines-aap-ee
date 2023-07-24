# gitops-demo
Gitops Configuration



### GitOps installation

`$ oc apply -k 0-init/0-gitops`

**Check if pods are running in openshift-gitops :**  
`$ oc get pods -n openshift-gitops`

**Get GitOps console route:**  
`$ CONSOLE_URL=$(oc get route openshift-gitops-server -n openshift-gitops -o jsonpath="{'https://'}{.spec.host}{'\n'}")`

_Optional: Patch argocd instance for reencrypt route_  
`oc -n openshift-gitops patch argocd/openshift-gitops --type=merge -p='{"spec":{"server":{"route":{"enabled":true,"tls":{"insecureEdgeTerminationPolicy":"Redirect","termination":"reencrypt"}}}}}'`


### ACM installation

`$ oc apply -k 0-init/1-acm`




Deploy:
oc apply -k XaC/0-gitops
oc apply -k gitOpsApplications
oc get route -n openshift-gitops openshift-gitops-server -o 'jsonpath={@.spec.host}'

