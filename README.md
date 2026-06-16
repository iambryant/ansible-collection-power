# Ansible Collection: IBM Power

[![CI](https://github.com/iambryant/ansible-collection-power/actions/workflows/ci.yml/badge.svg)](https://github.com/iambryant/ansible-collection-power/actions/workflows/ci.yml)

This collection includes roles for automating common tasks on IBM Power. 

> **Note:** This collection was designed around the limitations of my environment and may not be applicable to yours. Please check my
> [power-dev-playbook](https://github.com/iambryant/power-dev-playbook) for more info.

## Installation

You can include this collection in your `requirements.yml` like this:

```
collections:
  - name: iambryant.power
    source: https://github.com/iambryant/ansible-collection-power
    type: git
```

## Requirements

None.

## Included Roles

  - `iambryant.power.lpar` ([documentation](https://github.com/iambryant/ansible-collection-power/blob/main/roles/lpar/README.md))
  - `iambryant.power.vios` ([documentation](https://github.com/iambryant/ansible-collection-power/blob/main/roles/vios/README.md))

## Usage

To see an example of this collection's usage, see: https://github.com/iambryant/power-dev-playbook.

## License

MIT
