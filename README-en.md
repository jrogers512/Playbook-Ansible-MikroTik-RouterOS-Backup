RouterOS MikroTik Router Backup Playbook

Automating the Mikrotik router backup process with Ansible playbooks and Linux Cron.

The coolest part of this playbook is that at the end of the playbook, the last Ansible task calls a script that commits/pushes the backup configuration files, where they can now be copied to a Git repository.

So that at push time, Git uses the private key to authenticate to the repository, configure the following configuration:

A hint!! First of all, create the repository and then clone it on the server.
----------
1. Generate the ssh keys
```bash
$ ssh-keygen -t rsa -b 2048 -C "kessix@example.com"
```
2. The keys are stored inside the logged in user's home directory:
```bash
~/.ssh/id_rsa (private)
~/.ssh/id_rsa.pub (public)
```
3. Create the ~/.ssh/config file
The configuration may change depending on your repository.
Add the content below and change the parameters according to your repository:
```bash
# GitRepo
host gitrepo.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/gitrepo_com_rsa #(this line should point to the private key)
 ```
4. Tell the SSH client to point to the private key:
```bash
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa #(private)
```
5. Add the public key to your repository platform.
- Consult the repository documentation and see how to do this procedure.

6. Test the communication between the ssh agent and the repository
```bash
$ ssh -Tvvv git@gitrepo.com
```
