Ansible playbooks are YAML files that define a series of tasks to be executed on remote machines. They are used to automate configuration management, application deployment, and many other IT tasks. Playbooks are highly readable and can be reused and shared easily.

### Basic Structure of an Ansible Playbook

An Ansible playbook consists of one or more “plays.” Each play targets a group of hosts and defines tasks to be executed on those hosts. Here’s a basic structure:

```yaml
---
- name: Playbook Name
  hosts: target_hosts
  become: yes
  tasks:
    - name: Task description
      module_name:
        parameter1: value1
        parameter2: value2
```

### Example: Basic Playbook to Install Nginx

Here’s a simple playbook to install and start Nginx on a remote server:

1. **Create the playbook file**: Save the following content in a file named `install-nginx.yml`.

```yaml
---
- name: Install and start Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes
```

2. **Create an inventory file**: Save the following content in a file named `hosts.ini`.

```ini
[webservers]
your_server_ip ansible_user=your_user
```

Replace `your_server_ip` with the IP address of your server and `your_user` with the username you use to connect to the server.

3. **Run the playbook**: Execute the playbook with the following command:

```bash
ansible-playbook -i hosts.ini install-nginx.yml
```

### Explanation of the Playbook

- **name**: A descriptive name for the playbook.
- **hosts**: The target hosts or groups defined in the inventory file.
- **become**: Indicates whether to escalate privileges (use sudo).
- **tasks**: A list of tasks to be executed.
    - **name**: A description of the task.
    - **apt**: The Ansible module used to manage packages on Debian-based systems.
    - **service**: The Ansible module used to manage services.

This playbook will:

- Update the apt cache.
- Install Nginx.
- Start and enable the Nginx service.