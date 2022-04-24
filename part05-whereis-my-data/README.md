# Where Is My Data?
In kubernetes world the data and storage is not persistent by default, and this means that once a pod dies all dta dies with it.

In order to save our data, we need some where to keep our data, and that is **Persistent Volumes**

## Types Of Persistent Volumes
There are 2 ways that we can provision storage to our cluster.
- Static
- Dynamic

NOTE: When we are in local Kubernetes Cluster (No Clouds...) We are doomed to use static provisioning and that means, the administrator must first create the PV and then feed it to the cluster (Pods).

😎 Good News: Fortunately we have two sloutions to do this dynamically.
- NFS Dynamic Provisioning
- Glusterfs

PersistentVolume types are implemented as plugins. Kubernetes currently supports the following plugins:

📌 [awsElasticBlockStore](https://kubernetes.io/docs/concepts/storage/volumes/#awselasticblockstore) - AWS Elastic Block Store (EBS)

📌 [azureDisk](https://kubernetes.io/docs/concepts/storage/volumes/#azuredisk) - Azure Disk

📌 [azureFile](https://kubernetes.io/docs/concepts/storage/volumes/#azurefile) - Azure File

📌 [cephfs](https://kubernetes.io/docs/concepts/storage/volumes/#cephfs) - CephFS volume

📌 [csi](https://kubernetes.io/docs/concepts/storage/volumes/#csi) - Container Storage Interface (CSI)

📌 [fc](https://kubernetes.io/docs/concepts/storage/volumes/#fc) - Fibre Channel (FC) storage

📌 [gcePersistentDisk](https://kubernetes.io/docs/concepts/storage/volumes/#gcepersistentdisk) - GCE Persistent Disk

📌 [glusterfs](https://kubernetes.io/docs/concepts/storage/volumes/#glusterfs) - Glusterfs volume

📌 [hostPath](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) - HostPath volume (for single node testing only; WILL NOT WORK in a multi-node cluster; consider using local volume instead)

📌 [iscsi](https://kubernetes.io/docs/concepts/storage/volumes/#iscsi) - iSCSI (SCSI over IP) storage

📌 [local](https://kubernetes.io/docs/concepts/storage/volumes/#local) - local storage devices mounted on nodes.

📌 [nfs](https://kubernetes.io/docs/concepts/storage/volumes/#nfs) - Network File System (NFS) storage

📌 [portworxVolume](https://kubernetes.io/docs/concepts/storage/volumes/#portworxvolume) - Portworx volume

📌 [rbd](https://kubernetes.io/docs/concepts/storage/volumes/#rbd) - Rados Block Device (RBD) volume

📌 [vsphereVolume](https://kubernetes.io/docs/concepts/storage/volumes/#vspherevolume) - vSphere VMDK volume



