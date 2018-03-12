# vpn-ansible
Ansible Playbook for deploying Open VPN on Ubuntu and Arch Host

### Requirements
- Ansible >= 2.4

### Roles (in order of Execution)
- openvpn
  - Installs OpenVPN and adds server configuration file
- easy-rsa -
  - Generates Certificate Authority
  - Diffie-Hellman (DH) parameters key
  - Server certificate and Private key
  - Hash-based Message Authentication Code (HMAC) key
- network
  - Enables NAT forwarding
  - Starts OpenVPN network/client
- client  
  - Generates intial client cert and key

### Execution
- Update your global variables at `group_vars/all` with your *server*, *client*, *certs* information
- Execute the playbook

  `ansible-playbook [options] vpn.yaml`

- Find your intial client info:

  - `{client_name}.crt` - {certpath}/pki/issued/{client_name.cert}

  - `{client_name}.key` - {certpath}/pki/private/{client_name.key}

- Fill in `template.ovpn` with info or use ovpn generators to generate `ovpn` profiles.

###### Notes
- Currently works on remote hosts running os-families:
  - Debian: Ubuntu
  - ArchLinux: Arch Linux

### TODO
- Generate ovpn profiles
- Handle more OS families
- Copy client config from server to client
- Handle `update-systemd-resolved` for unix clients
