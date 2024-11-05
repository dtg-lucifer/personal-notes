
# *This playbook is for distributing the ssh key files to the remote servers so that password less connection and sudo access can be provided to the further tasks which ansible will do*


```yml
---
- name: Distribute SSH keys and configure sudo access
  hosts: all
  become: yes
  vars:
    ansible_become_password: "bosepiush"
    ansible_ssh_private_key_file: ~/.ssh/id_rsa
    public_key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
  tasks:
    - name: Ensure .ssh directory exists
      file:
        path: /home/{{ ansible_user }}/.ssh
        state: directory
        mode: '0700'
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"

    - name: Copy SSH public key to authorized_keys
      authorized_key:
        user: "{{ ansible_user }}"
        state: present
        key: "{{ public_key }}"

    - name: Configure sudoers file for passwordless sudo
      lineinfile:
        path: /etc/sudoers
        state: present
        regexp: '^{{ ansible_user }} ALL=\(ALL\) NOPASSWD: ALL'
        line: '{{ ansible_user }} ALL=(ALL) NOPASSWD: ALL'
        validate: 'visudo -cf %s'
```
