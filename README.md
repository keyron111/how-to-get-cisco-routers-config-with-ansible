# how-to-get-cisco-routers-config-with-ansible
 - name: getting info about network
   hosts: hq-rtr, br-rtr
   gather_facts: no
   tasks:
    - name: getting command sho run
      ios_command:
        commands: show running-config
      register: config
    - name: saving config into a new file on server
      copy:
        content: "{{ config.stdout[0] }}"
        dest: "./{{ inventory_hostname }}.backup"
      
