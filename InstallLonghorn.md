# Install Longhorn
## Index
- [Evaluation Environment](#evaluation-environment)
- [Prerequisite](#prerequisite)
- [Install Longhorn](#install-longhorn)

## Evaluation Environment
- The cluster has one control plane and three nodes to deploy Longhorn.
  ```
  +-----------------------+
  | Windows Server        | 
  | - Hyper-V             |
  | +-------------------+ |
  | | Control Plane     | |
  | | Ubuntu 20.04 LTS  | |
  | | kubernetes 1.18.3 | |
  | | Docker 19.03.10   | |
  | +------+------------+ |
  |        |              |
  | +------+------------+ |
  | | Node #1, #2, #3   | |
  | | Ubuntu 20.04 LTS  | |
  | | kubernetes 1.18.3 | |
  | | Docker 19.03.10   | |
  | +-------------------+ |
  +-----------------------+
  ```

## Prerequisite
- Check the hardware reqirements.
  - https://longhorn.io/docs/1.0.0/best-practices/#minimum-recommended-hardware
- Install iSCSI packages on nodes.
  - https://longhorn.io/docs/1.0.0/deploy/install/#installation-requirements
- Install Helm on the control plane.
  - https://github.com/EXPRESSCLUSTER/Helm/blob/master/InstallHelm.md
- Install Git on the control plane.

## Install Longhorn
1. Clone the repository.
   ```sh
   $ git clone https://github.com/longhorn/longhorn
   ```
1. Create a namespace and install Longhorn.
   ```sh
   $ kubectl create namespace longhorn-system
   $ helm install longhorn ./longhorn/chart/ --namespace longhorn-system
   ```
1. Check the all pods are running.
   ```sh
   $ kubectl get pod -n longhorn-system
   NAME                                       READY   STATUS    RESTARTS   AGE
   csi-attacher-5cc849c8dd-6gwbq              1/1     Running   3          28h
   csi-attacher-5cc849c8dd-bx72d              1/1     Running   2          24h
   csi-attacher-5cc849c8dd-pvv8f              1/1     Running   3          28h
   csi-provisioner-74557755-cf7q9             1/1     Running   4          28h
   csi-provisioner-74557755-mzfwb             1/1     Running   4          28h
   csi-provisioner-74557755-qxzmm             1/1     Running   2          24h
   csi-resizer-686bd4b6d7-ff9sf               1/1     Running   4          28h
   csi-resizer-686bd4b6d7-hkc7f               1/1     Running   2          24h
   csi-resizer-686bd4b6d7-tjh9d               1/1     Running   3          28h
   engine-image-ei-eee5f438-lnd28             1/1     Running   2          28h
   engine-image-ei-eee5f438-q6g7d             1/1     Running   2          28h
   engine-image-ei-eee5f438-s48tr             1/1     Running   2          28h
   instance-manager-e-1d376d2c                1/1     Running   0          3h8m
   instance-manager-e-31871846                1/1     Running   0          3h6m
   instance-manager-e-955bf30c                1/1     Running   0          3h7m
   instance-manager-r-019c5412                1/1     Running   0          3h6m
   instance-manager-r-a0f20648                1/1     Running   0          3h7m
   instance-manager-r-cc563307                1/1     Running   0          3h8m
   longhorn-csi-plugin-nc864                  2/2     Running   8          28h
   longhorn-csi-plugin-rhqjm                  2/2     Running   6          28h
   longhorn-csi-plugin-s7n48                  2/2     Running   8          28h
   longhorn-driver-deployer-cd74cb75b-47jms   1/1     Running   2          28h
   longhorn-manager-2xljv                     1/1     Running   2          28h
   longhorn-manager-92jcm                     1/1     Running   2          28h
   longhorn-manager-tb4kg                     1/1     Running   2          28h
   longhorn-ui-8486987944-jt5fb               1/1     Running   3          24h   
   ```   