# Changes for v1.1

## October 28, 2022

* ODF improvements: Kiosk VMs now explicitly request ceph storage from ODF by in order to be live-migratable, in situations with multiple virt-capable workers. Storage types can be customized per-VM using the `storageClassName`, `volumeMode`, and `accessMode` attributes of a specific VM type, or by setting the `defaultStorageClass`, `defultAccessMode`, and `defaultAccessMode` values in the chart. The settings are `coalesce`'d in the chart template so you can mix and match as desired.

* edge-gitops-vms wait: edge-gitops-vms now waits until there is at least one metal node "ready" before creating the VM-related resources. This prevents the application from being marked as in "error" state due to potential repeated failures due to the kubevirt.io API not being available. This can be turned off by using the `.Values.waitForMetalNode` toggle in the `edge-gitops-vms` chart.

* More comprehensive use of (Hashicorp) Vault secrets: All secrets are now stored in Vault and published in the `aap-config` application so that playbooks can retrieve them and provide them to AAP.

* More declarative configuration: AAP configuration now runs as part of the imperative framework, so that changes to the `ansible_configure_controller.yml` playbook will be applied on future runs of the imperative job.

* Fix Out-of-Sync conditions: Fixed cosmetic issues in both the ODF (OpenShift Data Foundations) and CNV (OpenShift Virtualization/Container Native Virtualization) spaces that would make those applications show as out-of-sync. These issues caused our internal CI to fail and we judged it better to fix those issues than to "live" with the out-of-syncs.
