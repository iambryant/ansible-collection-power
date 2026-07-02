# Ansible Role: VIOS

This role creates, configures, and installs VIOS logical partitions on IBM Power.

## Requirements

None.

## Role Variables

    vios_instances: []

The list of of VIOS logical partitions to be created and installed. Supports the following parameters:

| Parameter         | Type       | Required | Description                                                     |
| :---              | :---       | :---:    | :---                                                            |
| `system_name`     | String     | **Yes**  | The name of the managed system to install the VIOS on.          |
| `name`            | String     | **Yes**  | The name of the VIOS.                                           |
| `image_dir`       | String     | **Yes**  | The directory on the HMC where the VIOS image is stored.        |
| `vios_iso`        | String     | **Yes**  | The filename of the VIOS image the VIOS will use.               |
| `vios_ip`         | String     | **Yes**  | The IP address the VIOS will use.                               |
| `vios_gateway`    | String     | **Yes**  | The gateway the VIOS will use.                                  |
| `vios_subnetmask` | String     | **Yes**  | The subnet mask the VIOS will use.                              |
| `settings`        | Dictionary | **Yes**  | Refer to `settings`.                                            |

### settings

| Parameter       | Type    | Required | Description                                                         |
| :---            | :---    | :---      | :---                                                               |
| `proc_mode`     | String  | **Yes** | The processor allocation mode the VIOS will use (`ded` or `shared`). |
| `min_procs`     | Integer | **Yes** | The minimum processor allocation for the VIOS.                       |
| `desired_procs` | Integer | **Yes** | The desired processor allocation for the VIOS.                       |
| `max_procs`     | Integer | **Yes** | The maximum processor allocation for the VIOS.                       |
| `min_mem`       | Integer | **Yes** | The minimum memory allocation for the VIOS (in megabytes).           |
| `desired_mem`   | Integer | **Yes** | The desired memory allocation for the VIOS (in megabytes).           |
| `max_mem`       | Integer | **Yes** | The maximum memory allocation for the VIOS (in megabytes).           |
| `io_slots`      | String  | **Yes** | The physical I/O slots the VIOS will use.                            |

Additional parameters such as auto_start, time_ref, etc. can also be specified under `settings`.

Please refer to https://galaxy.ansible.com/ui/repo/published/ibm/power_hmc/content/module/vios/ for all supported parameters.

## Dependencies

None.

## Example Playbook

    - hosts: all
      gather_facts: false
      roles:
        - iambryant.power.vios

## License

MIT
