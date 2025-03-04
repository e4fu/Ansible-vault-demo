# Ansible Vault Demo

## About This Repository
This repository provides a **demonstration of Ansible Vault**, a feature in Ansible used to encrypt and manage sensitive data securely. It walks through setting up a project where **secrets such as API keys and database passwords** are stored in an encrypted format and used within Ansible playbooks. Additionally, it covers best practices, troubleshooting, and GitHub integration for managing encrypted files effectively.

## Project Setup
### 1. Initialize Git Repository
```sh
mkdir ansible-vault-demo
cd ansible-vault-demo
git init
git remote add origin https://github.com/e4fu/ansible-vault-demo.git
```

### 2. Create Inventory File
```ini
[local]
localhost ansible_connection=local
```

### 3. Encrypt Sensitive Data
```sh
mkdir -p group_vars/all
ansible-vault create group_vars/all/vault.yml
```
Add secrets:
```yaml
vault_api_key: "super-secret-api-key"
vault_db_password: "database-password-123"
```

### 4. Define Variables
```yaml
api_key: "{{ vault_api_key }}"
db_password: "{{ vault_db_password }}"
```

### 5. Create Playbook
```yaml
---
- hosts: local
  gather_facts: no
  tasks:
    - name: Display encrypted values
      debug:
        msg: 
          - "API Key: {{ api_key }}"
          - "DB Password: {{ db_password }}"
```

### 6. Run Playbook
```sh
ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass
```

## GitHub Integration
```sh
git add .
git commit -m "Ansible Vault Demo"
git push origin main
```


## Best Practices
- Never store plaintext secrets in Git.
- Use different vault passwords for different environments.
- Restrict access: `chmod 600 group_vars/all/vault.yml`.
- Regularly rotate secrets.

## Troubleshooting
**Decryption Failed:** Verify the correct vault password.  
**Push Rejected:** Sync changes: `git pull origin main --rebase`.

## Conclusion
This repository demonstrates how **Ansible Vault** can be used to **securely manage secrets in automation workflows**. By encrypting sensitive data and following best practices, users can protect credentials while integrating them into version-controlled Ansible projects.

## References
- [Ansible Vault Docs](https://docs.ansible.com/ansible/latest/user_guide/vault.html)
- [GitHub Best Practices](https://docs.github.com/en/get-started)

