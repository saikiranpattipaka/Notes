### Ansible
Ansible is an open-source automation tool used for:
- Configuration Management
- Application Deployment
- Orchestration
- Provisioning
- Continuous Delivery (CD)
Ansible uses a simple syntax written in **YAML**, called Playbooks.

### ✅ Key Features
- Agentless: No need to install any software/agent on client machines.
- Push-based: Executes commands over SSH (Linux) or WinRM (Windows).
- Simple YAML syntax.
- Idempotent: Running the same script multiple times won’t change the system if it’s already in the desired state.
- Modules: Built-in units of work (e.g., `yum`, `apt`, `copy`, `service`).

### 🔧 Ansible Architecture
- Control Node: The machine where Ansible is installed.
- Managed Node: The servers Ansible manages (also called hosts).
- Inventory: A list of managed nodes (can be static or dynamic).
- Modules: Units of work like `yum`, `service`, `copy`.
- Playbook: A YAML file describing automation instructions.
- Task: A single unit of work in a playbook.
- Role: A reusable component containing tasks, vars, files, templates, etc.

#### Install Ansible:
[Ansible Doc](https://docs.ansible.com/)
```
sudo apt install ansible       # Debian/Ubuntu  
sudo dnf install ansible       # RHEL/CentOS/Fedora
```
#### Inventory File:
Default location: `/etc/ansible/hosts`
Extension `.ini`
```
[webservers]
ubuntu@192.168.1.10
web1 ansible_host=192.168.56.101 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/web_key.pem

[dbservers]
db1 ansible_host=192.168.56.110 ansible_user=dbadmin ansible_ssh_private_key_file=~/.ssh/db_key.pem ansible_port=2222 ansible_python_interpreter=/usr/bin/python3
db2.example.com
```
#### Test connectivity:
```
ansible all -m ping
```

### 🔐 Ansible Passwordless Authentication
Ansible uses SSH to connect to remote hosts. Passwordless authentication makes automation seamless by removing the need to enter a password every time a connection is made.
- The most common and secure method is **SSH Key-based Authentication**

#### Using Public Key
```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```
- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile ": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@: This is the username (ubuntu) and the IP address of the remote server you want to access.

#### Using Password
- Go to the file `sudo vim/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`
- Login `ssh-copy-id ubuntu@<INSTANCE-PUBLIC-IP>`

### Ad Hoc Commands
Ansible ad hoc commands are one-liner shell commands used to perform quick tasks across multiple managed nodes without writing a playbook.They are used for
- Quick system checks
- Small configuration changes
- File manipulation
- Service management
- Package installation

#### 🧱 Basic Syntax
```
ansible <host-pattern> -m <module-name> -a "<module-arguments>"
```
Example
```
ansible all -m ping #Check connectivity
```

#### ⚙️ Components Breakdown
|Part	                   |Description                                                 |
|--------------------------|------------------------------------------------------------|
|`ansible`	               |The Ansible command-line tool                               |
|`<host-pattern>`	       |The group/host from inventory (e.g., all, web, 192.168.1.5) |
|`-m`	                   |Specifies the module to use                                 |
|`-a`	                   |Arguments to pass to the module                             |
|`-i`	                   |Optional: specify an inventory file                         |
|`-u`	                   |Optional: specify remote user                               |
|`--become or -b`	       |Optional: run command with privilege escalation (sudo)      |

#### ✅ Commonly Used Ad Hoc Commands
1. Check connectivity
```
ansible all -m ping
```
- Uses the `ping` module.
- Tests connection, not ICMP ping—it's a Python call.

2. Run shell commands
```
ansible all -m shell -a "uptime"
```
- Runs the command via shell (interprets pipes, redirection, etc.)
```
ansible all -m command -a "ls /tmp"
```
- Safer than `shell`, doesn’t process pipes or environment variables.

3. Manage packages
- Install `httpd` (Apache):
```
ansible web -m yum -a "name=httpd state=present"
```
- Remove package:
```
ansible web -m apt -a "name=nginx state=absent" -b
```
4. Manage services
- Start a service:
```
ansible web -m service -a "name=httpd state=started" -b
```
- Stop or restart:
```
ansible web -m service -a "name=httpd state=restarted" -b
```
5. Copy files
```
ansible web -m copy -a "src=/etc/hosts dest=/tmp/hosts_copy" -b
```
6. Fetch files from remote to local
```
ansible web -m fetch -a "src=/var/log/messages dest=/tmp/logs/ flat=yes"
```
7. Create or delete users
- Add a user:
```
ansible all -m user -a "name=testuser state=present" -b
```
- Delete a user:
```
ansible all -m user -a "name=testuser state=absent" -b
```
8. Set file permissions
```
ansible all -m file -a "path=/tmp/testfile mode=0644 owner=root group=root state=touch" -b
```
9. Reboot a machine
```
ansible all -m reboot -a "test_command=uptime" -b
```
[Ad-hoc Commands Ref](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html)

