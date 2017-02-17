## This is an example of using Packer and Ansible to create a LEMP stack AMI.

### A note on Ansible Vault

This example uses Ansible Vault to decrypt the `secrets.yml` vars file in the web role. This allows you to store sensitive information (RSA keys, etc) in version control without worry.

It does this by copying `ansible.vault.password.txt` to the build server, then calling ansible-playbook with the `--vault-password-file` flag. Once Ansible has finished running the playbook, the `remove_vault_password.sh` provisioner removes the vault password file from the server, before the AMI snapshot is created.

The `ansible.vault.password.txt` file is kept in this example's version control, so that everything works out of the box. **HOWEVER**, in a real use case you would not do this.

In a real use case, you would add the vault password file to the `.gitignore`. You would store the vault password elsewhere, then create the vault password file anytime you need to setup the project.

An alternate workflow would be to commit an Ansible Vault password **script** to version control. This script would obtain the password from an external service. See the [Ansible Vault documentation](http://docs.ansible.com/ansible/playbooks_vault.html) for more information.
