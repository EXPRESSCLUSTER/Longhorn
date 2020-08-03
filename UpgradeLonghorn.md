# Upgrade Longhorn
## Index
- [Upgrade from v1.0.0 to v1.0.1](#upgrade-from-v100-to-v101)

## Upgrade from v1.0.0 to v1.0.1
- Official Documentation
  - https://longhorn.io/docs/1.0.1/deploy/upgrade/
  - Upgrading Longhorn Manager
    - https://longhorn.io/docs/1.0.1/deploy/upgrade/longhorn-manager/
  - Upgrading Longhorn Engin
    - https://longhorn.io/docs/1.0.1/deploy/upgrade/upgrade-engine/

### Upgrade Manager
1. Login a node you can run git and helm command.
1. Check name space.
   ```sh
   $ helm list --all-namespaces
   NAME           NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
   longhorn        longhorn-system 1               2020-06-25 22:04:41.747101092 +0900 JST deployed        longhorn-1.0.0  v1.0.0
   ```
1. Download the latest repository.
   ```sh
   $ cd <some directory>/longhorn
   $ git pull
   remote: Enumerating objects: 127, done.
   remote: Counting objects: 100% (127/127), done.
   remote: Compressing objects: 100% (17/17), done.
   remote: Total 244 (delta 112), reused 119 (delta 110), pack-reused 117
   Receiving objects: 100% (244/244), 44.74 KiB | 254.00 KiB/s, done.
   Resolving deltas: 100% (163/163), completed with 30 local objects.
   From https://github.com/longhorn/longhorn
      809578d..f176517  master     -> origin/master
    * [new branch]      v1.0.1     -> origin/v1.0.1
    * [new branch]      v1.0.2     -> origin/v1.0.2
    :
   (snip)   
    :
    38 files changed, 1043 insertions(+), 63 deletions(-)
    create mode 100644 .gitignore
    create mode 100644 deploy/longhorn-images.txt
    create mode 100644 deploy/release-images.txt
    create mode 100644 dev/scale-test/.gitignore
    create mode 100644 dev/scale-test/README.md
    create mode 100755 dev/scale-test/sample.sh
    create mode 100644 dev/scale-test/scale-test.py
    create mode 100644 dev/scale-test/statefulset.yaml
    create mode 100755 dev/scripts/update-image-pull-policy.sh
    create mode 100644 enhancements/20200625-volume-deletion-flows.md
    create mode 100644 enhancements/20200701-backupstore-file-locks.md
    create mode 100644 examples/rwx/01-security.yaml
    create mode 100644 examples/rwx/02-longhorn-nfs-provisioner.yaml
    create mode 100644 examples/rwx/03-rwx-test.yaml
    create mode 100755 scripts/load-images.sh
    create mode 100755 scripts/save-images.sh
   ```
1. Upgrade Longhorn.
   ```sh
   $ helm upgrade longhorn ./chart -n longhorn-system
   Release "longhorn" has been upgraded. Happy Helming!
   NAME: longhorn
   LAST DEPLOYED: Mon Aug  3 11:06:32 2020
   NAMESPACE: longhorn-system
   STATUS: deployed
   REVISION: 2
   TEST SUITE: None
   NOTES:
   Longhorn is now installed on the cluster!
   
   Please wait a few minutes for other Longhorn components such as CSI deployments, Engine Images, and Instance Managers to be initialized.
   
   Visit our documentation at https://longhorn.io/docs/   
   ```
1. Check the version.
   ```sh
   $ helm list -n longhorn-system
   NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
   longhorn        longhorn-system 2               2020-08-03 11:06:32.860447985 +0900 JST deployed        longhorn-1.0.1  v1.0.1
   ```