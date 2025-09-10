# Ansible Playbook: Configure Initial IPA (IdM) Server

This playbook configures the **initial IPA server** using the  
[`redhat.rhel_idm`](https://galaxy.ansible.com/redhat/rhel_idm) collection.

---

## Playbook

```yaml
---
- name: Playbook to configure Initial IPA server
  hosts: ipaserver
  become: true

  roles:
    - role: redhat.rhel_idm.ipaserver
      ipaadmin_password: SomeADMINpassword
      idm_domain: server.lab
      idm_realm: SERVER.LAB
      idm_hostname: idm.server.lab
      state: present
      # state: absent
```

---

## Sample Inventory

```ini
[ipaserver]
idm.server.lab ansible_host=192.168.56.10 ansible_user=admin ansible_ssh_private_key_file=~/.ssh/id_rsa
```

- Replace `192.168.56.10` with your IPA server’s IP.  
- Ensure your SSH key or password is configured for Ansible connectivity.  

---

## Setup Steps

1. **Install required Ansible Collection**:

   ```bash
   ansible-galaxy collection install redhat.rhel_idm
   ```

2. **Run the playbook**:

   ```bash
   ansible-playbook -i inventory.ini ipaserver.yml
   ```

   *where `inventory.ini` lists your IPA server under `[ipaserver]`.*

---

## Notes

- `ipaadmin_password`: Password for the IPA admin account (required).  
- `idm_domain`: The IdM DNS domain (e.g., `server.lab`).  
- `idm_realm`: The Kerberos realm (must be UPPERCASE, e.g., `SERVER.LAB`).  
- `idm_hostname`: Fully Qualified Domain Name of the IdM server.  
- `state`: Use `present` to configure and initialize, `absent` to remove.  
- `become: true` ensures playbook runs with root privileges.

---
