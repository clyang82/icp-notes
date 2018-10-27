## How to work with Istio in IBM Cloud private without a cluster admin user
### Problem
> Istio creates a number of customer resources that are not bound with the pre-defined roles in IBM Cloud private (Administrator, Operator, Editor, Viewer, Auditor)
> Developers, who don't have `Cluster Administrator` role, cannnot create Istio resources such as Gateways, VirtualServices, Destination rules
### Solution
> Assign developers as administrator to a namespace
> Update the `clusterroles/icp-admin-aggregate`
```
kubectl edit clusterroles/icp-admin-aggregate
```
> Add the following to the bottom of the cluster-role yaml
```
- apiGroups:
  - networking.istio.io
  resources:
  - gateways
  - virtualservices
  - destinationrules
  verbs:
  - create
  - delete
  - get
  - patch
  - update
  - list
```
> Type colon wq to save (as of vim)
> Try to create an Istio resource