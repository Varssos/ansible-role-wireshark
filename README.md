# wireshark

Ansible role to install [Wireshark](https://www.wireshark.org/) and configure non-root packet capture on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)
- `community.general` collection (for `capabilities` module)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `wireshark_package_name` | `wireshark` | Package name to install via apt |
| `wireshark_group` | `wireshark` | Group granting non-root capture access |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: wireshark
```

## License

MIT

## Author

Varssos