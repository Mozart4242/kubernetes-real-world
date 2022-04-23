# NFS Dynamic Provisioning

📌 An nfs volume allows an existing NFS (Network File System) share to be mounted into a Pod. Unlike emptyDir, which is erased when a Pod is removed, the contents of an nfs volume are preserved and the volume is merely unmounted. This means that an NFS volume can be pre-populated with data, and that data can be shared between pods. NFS can be mounted by multiple writers simultaneously.

## How Does This Work ?
1- A NFS client provisioner pod will get created

2- Persistent Volumes will get created by this pod through PVC. (This PVC is also bound to a Storage Class)

3- when your app runs, it will ask for a PV through PVC.

4- The PV will get created at last.


## Lets Get Started
📌 in this section im going to show how you can automatically provision a NFS volume (based on pvc) for your pods without creating the PV statically.
📌 When the pvc is deleted, the pv associated with it will also get deleted.

### Step1 : Install NFS Server
My nfs server is 10.132.132.104

```
$ sudo apt install nfs-server

$ mkdir /opt/nfs/kubedata -p
$ echo "/opt/nfs/kubedata	*(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure)" >> /etc/exports
$ sudo exportfs -rav
```
### Step2: 
Lets create [nfs-subdir-external-provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner/).

```
$ kubectl apply -f rbac.yml -f deployment.yml -f class.yml
$ kubectl get all
```

### Step3: Test
If you want to test this deployment, you can use the myapp.yml manifest.

```
$ kubectl apply -f nfs-pvc.yml -f myapp.yml
```
