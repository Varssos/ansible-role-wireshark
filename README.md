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

## Manual setup (without Ansible)

This enables packet capture for members of the `wireshark` group; only add
users who should have that access:

```bash
echo 'wireshark-common wireshark-common/install-setuid boolean true' | sudo debconf-set-selections
sudo apt install wireshark libcap2-bin
sudo dpkg-reconfigure -f noninteractive wireshark-common
sudo groupadd -f wireshark
sudo usermod -aG wireshark "$(id -un)"
sudo setcap 'cap_net_raw,cap_net_admin+eip' /usr/bin/dumpcap
```

Log out and back in before running Wireshark as your normal user.

## License

MIT

## Author

Varssos