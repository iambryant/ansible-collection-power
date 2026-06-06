# Ansible Role: VIOS

This role creates, configures, and installs VIOS logical partitions on IBM Power.

## Requirements

None.

## Role Variables

    vios_instances: []

A list of dictionaries containing individual VIOS configuration definitions.

| Parameter         | Type       | Required | Description                                                                    |
| :---              | :---       | :---:    | :---                                                                           |
| `name`            | String     | **Yes** | The name of the VIOS logical partition.                                        |
| `system_name`     | String     | **Yes** | The name of the managed Power system to install the VIOS logical partition to. |
| `settings`        | Dictionary | **Yes** | Refer to `settings`.                                                           |
| `image_dir`       | String     | **Yes** | The directory on the HMC where the VIOS image is stored.                               |
| `vios_iso`        | String     | **Yes** | The filename of the VIOS image that the VIOS logical partition will use.               |
| `vios_ip`         | String     | **Yes** | The IP address that will be assigned to the VIOS logical partition.                    |
| `vios_gateway`    | String     | **Yes** | The gateway that the VIOS logical partition will use.                                  |
| `vios_subnetmask` | String     | **Yes** | The subnet mask that the VIOS logical partition will use.                              |
| `network_macaddr` | String     | **Yes** | The MAC address of the physical network port that the VIOS logical partition will use. |

### settings

| Parameter       | Type    | Required? | Description |
| :---            | :---    | :---      | :---        |
| `proc_mode`     | String  | **Yes** | The processor allocation mode that the VIOS logical partition will use (`ded` or `shared`). |
| `min_procs`     | Integer | **Yes** | The minimum processor allocation for the VIOS logical partition. |
| `desired_procs` | Integer | **Yes** | The desired processor allocation for the VIOS logical partition. |
| `max_procs`     | Integer | **Yes** | The maximum processor allocation for the VIOS logical partition. |
| `min_mem`       | Integer | **Yes** | The minimum memory allocation in megabytes. |
| `desired_mem`   | Integer | **Yes** | The desired memory allocation in megabytes. |
| `max_mem`       | Integer | **Yes** | The maximum memory allocation in megabytes. |
| `io_slots`      | String  | **Yes** | The physical I/O slots that will be assigned to the VIOS logical partition. |

# Add image explaining why network_macaddr is required even though the module says it isn't
Additional parameters such as auto_start, time_ref, etc. can also be specified under `settings`.

Please refer to https://galaxy.ansible.com/ui/repo/published/ibm/power_hmc/content/module/vios/ for all supported parameters.

## Dependencies

None.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

     hosts: servers
      roles:
        - { role: username.rolename, x: 42 }

## License

MIT
