# *This is a playbook to install and restart the nginx web server into multiple servers*

```yml
---
- name: Install and configure Nginx
  hosts: azurevm
  become: yes
  vars:
    nginx_conf: |
      server {
          listen 80;
          server_name localhost;

          location / {
              root /var/www/html;
              index index.html index.htm;
          }
      }
    ansible_become_password: "bosepiush"
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Create Nginx configuration file
      copy:
        content: "{{ nginx_conf }}"
        dest: /etc/nginx/sites-available/default
        owner: root
        group: root
        mode: '0644'

    - name: Remove default symlink in sites-enabled
      file:
        path: /etc/nginx/sites-enabled/default
        state: absent

    - name: Create symlink for Nginx configuration
      file:
        src: /etc/nginx/sites-available/default
        dest: /etc/nginx/sites-enabled/default
        state: link

    - name: Ensure Nginx is running
      service:
        name: nginx
        state: started
        enabled: yes


```