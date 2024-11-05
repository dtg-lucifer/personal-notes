In Ansible, **handlers** are special tasks that are triggered by other tasks using the `notify` directive. Handlers are typically used to perform actions like restarting services, reloading configurations, or any other task that should only be executed when a change occurs.

### Key Points about Handlers:

- **Triggered by Notify**: Handlers only run when they are notified by other tasks.
- **Run Once**: Even if multiple tasks notify the same handler, it will only run once at the end of the play.
- **Order of Execution**: Handlers are executed in the order they are defined in the handlers section, not in the order they are notified.

### Basic Syntax of Handlers

Here’s a simple example to illustrate how handlers work:

1. **Playbook with Handlers**:

```yaml
---
- name: Install and configure Apache
  hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
      notify:
        - Restart Apache

    - name: Copy Apache config file
      template:
        src: /path/to/apache.conf.j2
        dest: /etc/apache2/apache2.conf
      notify:
        - Restart Apache

  handlers:
    - name: Restart Apache
      service:
        name: apache2
        state: restarted
```

### Explanation:

- **Tasks Section**:
    
    - **Install Apache**: Installs the Apache package and notifies the `Restart Apache` handler.
    - **Copy Apache config file**: Copies a configuration file and notifies the `Restart Apache` handler.
- **Handlers Section**:
    
    - **Restart Apache**: This handler restarts the Apache service. It will only run if one of the tasks that notify it has made a change.

### Running the Playbook

1. **Create an Inventory File**: Save the following content in a file named `hosts.ini`.
    
    ```
    [webservers]
    your_server_ip ansible_user=your_user
    ```
    
2. **Run the Playbook**: Execute the playbook with the following command:
    
    ```bash
    ansible-playbook -i hosts.ini your_playbook.yml
    ```
    

[By using handlers, you can ensure that certain actions (like restarting a service) are only performed when necessary, which can help avoid unnecessary disruptions and improve the efficiency of your automation scripts](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html)[1](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html)[2](https://ostechnix.com/use-handlers-in-ansible-playbooks/)[3](https://www.cherryservers.com/blog/how-to-define-and-use-handlers-in-ansible-playbooks).