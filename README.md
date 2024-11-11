# Ansible Role linux_it87_driver

[![Build Status][build_badge]][build_link]
[![Ansible Galaxy][galaxy_badge]][galaxy_link]

Install, update, or uninstall the `it87` kernel driver for IT86 & IT87 Super I/O chips via DKMS.

Install the role: `ansible-galaxy role install tigattack.linux_it87_driver`

See [frankcrawford/it87](https://github.com/frankcrawford/it87) for an up-to-date list of supported chips.

> [!WARNING]
> Breakage is always possible when altering kernel modules. Use at your own risk.
> This role works great for me, but no guarantees are made.

See [Example Playbooks](#example-playbooks) below.

## Prerequisites

* DKMS
* [community.general](https://galaxy.ansible.com/ui/repo/published/community/general/) >= 0.1.1 Ansible collection. See [requirements.yml](requirements.yml).

> [!WARNING]
> This has been tested on Debian 12. I cannot guarantee the result on other versions or distributions.

## Role Variables

### `linux_it87_driver_state`

| Type   | Default   |
|--------|-----------|
| string | `present` |

State of the `it87` kernel driver.

Must be one of:
* `present`
* `latest`
* `absent`

### `linux_it87_driver_version`

| Type   | Default |
|--------|---------|
| string | `HEAD`  |

Version of the `it87` kernel driver.

This can be the literal string `HEAD`, a branch name, or a tag name from [frankcrawford/it87](https://github.com/frankcrawford/it87).

## Example Playbooks

**Install:**

```yml
- name: Install Linux IT87 driver
  hosts: all
  become: true
  roles:
    - role: linux_it87_driver
```

> [!TIP]
> To always update to latest, set `linux_it87_driver_state` to `latest`.
> However, note that this requires uninstalling & reinstalling the driver every time as the module does not provide a real version number.

**Uninstall:**

```yml
- name: Uninstall Linux IT87 driver
  hosts: all
  become: true
  roles:
    - role: linux_it87_driver
      vars:
        linux_it87_driver_state: absent
```

## License

MIT

## Sources

* <https://www.reddit.com/r/BeelinkOfficial/comments/15m8yms/eq12_s12_pro_read_fan_speeds_in_linux_cpu_and/>
* <https://github.com/frankcrawford/it87>

[build_badge]:  https://img.shields.io/github/actions/workflow/status/tigattack/ansible-role-linux-it87-driver/test.yml?branch=main&label=Lint%20%26%20Test
[build_link]:   https://github.com/tigattack/ansible-role-linux-it87-driver/actions?query=workflow:Test
[galaxy_badge]: https://img.shields.io/ansible/role/d/tigattack/linux_it87_driver
[galaxy_link]:  https://galaxy.ansible.com/ui/standalone/roles/tigattack/linux_it87_driver/
