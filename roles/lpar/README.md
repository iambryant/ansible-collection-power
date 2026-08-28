# Ansible Role: LPAR

This role installs logical partitions on IBM Power.

Before running the role, create an LPAR with:

- A network adapter attached to the target network
- A disk attached for operating system installation

> [!NOTE]
> Make sure to allocate at least 4 GiB of RAM to the LPAR so that the live environment can fit into memory.
> For more details, see: https://access.redhat.com/articles/rhel-limits#minimum-required-memory-3.

This role will then:

1. Configure TFTP and HTTP services on the provisioning host.
2. Generate cloud-init data for the LPAR.
3. Network boot the LPAR into a live Linux environment.
4. Write a Debian 13 cloud image to the target disk.

> [!NOTE]
> AIX provisioning is currently a work in progress.

5. Configure the LPAR to retrieve cloud-init data over HTTP on first boot.

## Requirements

None.

## Role Variables

    lpar_live_os_version: "almalinux8"

The live environment operating system version to use for writing cloud images to LPAR disks. Defaults to `"almalinux8"`.

    lpar_live_url: "https://repo.almalinux.org/almalinux/8/BaseOS/ppc64le/os/"

The base URL to use for downloading the boot files for the live environment.

    lpar_web_root: "/var/www/html"

The directory to use on the netboot server for hosting files served over HTTP. Defaults to `/var/www/html`.

    lpar_tftp_root: "/var/lib/tftpboot"

The directory to use on the netboot server for hosting files served over TFTP. Defaults to `/var/lib/tftpboot`.

    lpar_cloud_images: "{{ lpar_web_root }}/cloud-images"

The directory within the web root to store cloud images. Defaults to `{{ lpar_web_root }}/cloud-images`.

    lpar_seed_files: "{{ lpar_web_root }}/seed-files"

The directory within the web root to store cloud-init files. Defaults to `{{ lpar_web_root }}/seed-files`.

    lpar_kickstart_files: "{{ lpar_web_root }}/kickstarts"

The directory within the web root to store kickstart files. Defaults to `{{ lpar_web_root }}/kickstarts`.

    lpar_instances: []

The list of logical partitions to be installed. Supports the following parameters:

| Parameter      | Type    | Required | Description                                                              |
| :---           | :---    | :---     | :---                                                                     |
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
