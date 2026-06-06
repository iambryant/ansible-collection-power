# Ansible Collection: IBM Power

[![CI](https://github.com/LPARS/ansible-collection-power/actions/workflows/ci.yml/badge.svg)](https://github.com/LPARS/ansible-collection-power/actions/workflows/ci.yml)

This collection includes roles for automating common tasks on IBM Power. Note that this collection was designed around the limitations
of my environment and may not be applicable to yours. Please check my ([power-dev-playbook](https://github.com/LPARS/power-dev-playbook))
for more info.

## Installation

You can include this collection in your `requirements.yml` like this:

```
collections:
  - name: lpars.power
    source: https://github.com/LPARS/ansible-collection-power
    type: git
```

## Requirements

None.

## Included Roles

  - lpars.power.lpar_install ([documentation](https://github.com/lpars/ansible-collection-power/blob/main/roles/lpar_install/README.md))
  - lpars.power.vios_install ([documentation](https://github.com/lpars/ansible-collection-power/blob/main/roles/vios_install/README.md))

## Usage

To see an example of this collection's usage, see: https://github.com/LPARS/power-dev-playbook.

## License

MIT
