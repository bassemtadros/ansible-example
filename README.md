# VMware vCenter Management Script

This Ansible script performs several tasks to interact with a VMware vCenter server. The script retrieves a password for the vCenter server from Vault, and then uses this password to connect to the vCenter server using the `vmware_vm_shell` module.

## Getting Started

Before you begin, you will need to have the following:
- Ansible installed on your local machine
- A valid token for the Vault server where the vCenter server password is stored
- vCenter server details, including the server address, username, and datacenter and cluster name

## Usage

1. Enter your Vault token when prompted.
2. Update the `vcenter_server`, `vcenter_user`, `datacenter_name`, and `cluster_name` variables with your vCenter server details.
3. Run the script with the following command: `ansible-playbook -i localhost, -c local vm_management.yml`

## Script Walkthrough

1. The script retrieves the vCenter server password from Vault using the `shell` module.
2. It then uses the `vmware_vm_shell` module to connect to the vCenter server.
3. The `vmware_cluster_info` module is used to retrieve information about the specified cluster.
4. The `vmware_vm_info` module is used to retrieve a list of powered-off virtual machines in the cluster.
5. The script sorts the list of virtual machines based on their disk size.
6. It then uses the `vmware_vm_logging` and `vmware_vm_power` modules to enable logging and power on the 5 VMs with the smallest disk size.
7. Finally, it uses the `vmware_vm_shell` module again to disconnect from the vCenter server.

**IMPORTANT:** Please be aware that in this script, `validate_certs` is set to `no`, which means it is not validating the SSL certificate of the vCenter Server. This is a security risk, in a production environment it is recommended to use a valid certificate and set `validate_certs` to `true`.

## Conclusion

This script demonstrates how to use Ansible to interact with a VMware vCenter server in order to retrieve information about a specific cluster and its virtual machines, sort the VMs based on their disk size, enable logging and power on some VMs. With some adjustments, this script can be used for automating day to day tasks in VMware vCenter management.
