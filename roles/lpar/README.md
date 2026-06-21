# Ansible Role: LPAR

This role installs logical partitions on IBM Power.

Before running the role, create an LPAR with:

- A network adapter attached to the target network
- A disk attached for operating system installation

This role will then:

1. Configure TFTP and HTTP services on the provisioning host.
2. Generate cloud-init data for the LPAR.
3. Network boot the LPAR into a live Linux environment.
4. Write a Debian 13 cloud image to the target disk.
   > **Note:** AIX provisioning is currently a work in progress.
5. Configure the LPAR to retrieve cloud-init data over HTTP on first boot.

## Requirements

None.

## Role Variables

    lpar_os_version: "almalinux8"

The operating system version to target for installation. Defaults to `"almalinux8"`.

    lpar_mirror_url: "https://repo.almalinux.org/almalinux/8/BaseOS/ppc64le/os/"

The base URL for the repository mirror containing the installation files.

    lpar_web_root: "/var/www/html"

The local root directory of the provisioning server hosting deployment media. Defaults to `/var/www/html`.

    lpar_tftp_root: "/var/lib/tftpboot"

The local root directory of the provisioning server for network booting. Defaults to `/var/lib/tftpboot`.

    lpar_cloud_images: "{{ lpar_web_root }}/cloud-images"

The path where cloud images are stored. Defaults to `{{ lpar_web_root }}/cloud-images`.

    lpar_seed_files: "{{ lpar_web_root }}/seed-files"

The path where cloud-init files are stored. Defaults to `{{ lpar_web_root }}/seed-files`.

    lpar_kickstart_files: "{{ lpar_web_root }}/kickstarts"

The path where Kickstart configuration files are stored. Defaults to `{{ lpar_web_root }}/kickstarts`.

    lpar_instances: []

The list of logical partitions to be installed. Supports the following parameters:

| Parameter      | Type    | Required | Description                                                              |
| :------------- | :------ | :------- | :----------------------------------------------------------------------- |
| `system_name`  | String  | **Yes**  | The name of the managed system the LPAR was created on.                  |
| `vm_name`      | String  | **Yes**  | The name of the LPAR.                                                    |
| `os_type`      | String  | **Yes**  | The operating system type the LPAR will use (e.g. `"aix"` or `"linux"`). |
| `network_name` | String  | **Yes**  | The virtual network the LPAR will use.                                   |
| `hostname`     | String  | **Yes**  | The hostname the LPAR will use.                                          |
| `domain`       | String  | **Yes**  | The domain name the LPAR will use.                                       |
| `vm_ip`        | String  | **Yes**  | The IP address the LPAR will use.                                        |
| `subnetmask`   | String  | **Yes**  | The subnet mask the LPAR will use.                                       |
| `gateway`      | String  | **Yes**  | The gateway the LPAR will use.                                           |
| `nameservers`  | List    | **Yes**  | The DNS servers the LPAR will use.                                       |
| `timeout`      | Integer | No       | The timeout to set for the installation of the LPAR (in minutes).        |

## Dependencies

You will need an role to configure your base subnet definitions in `/etc/dhcp/dhcpd.conf`. I recommend
[berrtv.dhcp](https://galaxy.ansible.com/ui/standalone/roles/berrtv/dhcp/).

## Example Playbook

    - hosts: all
      gather_facts: false
      roles:
        - iambryant.power.lpar

## License

MIT
