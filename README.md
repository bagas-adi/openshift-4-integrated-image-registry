# Configuring Integrated Image Registry in Openshift 4.x using Operator

##
Based on documentation : <a href="https://docs.openshift.com/container-platform/4.1/registry/configuring-registry-operator.html"> Configuring Registry Operator</a>

1. Use namespace openshift-image-registry
2. Edit the Operator Configs
```
$ oc edit configs.imageregistry.operator.openshift.io/cluster

```
Change ManagementState to Managed
Change DefaultRoute to true
Change storage into this :
```
storage:
  pvc:
    claim:
```
After this operator will create PVC and deploy image-registry pod
3. Create PV
In this example I use NFS with size 30 Gi.
Default size of image-registry PVC will claim is 100 Gi. To change that, delete the PVC and create a new one.
Make sure the PV is bounded by the PVC.
Make sure the image-registry pod is mount the NFS path from PV.
```
$ oc rsh image-registry-xxx
sh4.2 # df -h 
```
4. Create pull-secrets to pull image from redhat image repository
5. Check if it configured, start s2i from Openshift Console