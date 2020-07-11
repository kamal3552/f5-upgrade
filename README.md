# F5 Upgrader

## Requirements

The F5 Ansible collection is required. 

To install the most recent version run `ansible-galaxy collection install f5networks.f5_modules`

See https://clouddocs.f5.com/products/orchestration/ansible/devel/usage/getting_started.html for details.

## Configuration

Configuration (as provided) is done in the hosts.ini file.

Each host needs a "reboot group" variable. This allows for clusters to be upgraded one at a time for a rolling upgrade.

Adjust the image name and location to suit.

## Usage

`ansible-playbook -i hosts.ini upgrade.yaml`

## Error Conditions

The playbook will exit on any failure in the softwware activation tasks. This is to avoid taking out both members of a cluster.

Investigate any hosts that have reported a problem, and re-run the playbook to continue. It will move quickly through tasks that were already done and proceed with remaining upgrades.

I have found an issue where the `bigip_software_install` tasks can fail while waiting for the management interface to be available after a reboot. Increasing the timeout in the provider did not resolve this.