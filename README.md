# ansible_playbook1

<p>
Wrote an ansible playbook called winconfig.yml that will:

created local user named User1 on the windows machine
created a windows group named Group1 and add User1 to it
created a directory called c:\Shared on the windows machine and give Group1 full access
Share c:\Shared out with only Group1 having access to it.
Test by using smbclient on the linux machine to attach to the share. 
</p>


```

#configMgmt4
#20232405
#create local user, group, directoy and share the c drive shared.


#create a play book
- name: create playbook
  hosts: windows1
  tasks:



#add group
    - name: create group
      ansible.windows.win_group:
        name: Group1
        description: deploy Group1
        state: present

# add user
    - name: create user 
      ansible.windows.win_user:
        name: User1
        password: ***
        state: present
        groups:
         - Group1 # create
        home_directory: c:\Shared  # create


#Create Path
    - name: Touch file
      ansible.windows.win_file:
        path: C:\Shared        # group1 needs access
        state: directory
        owner: User1
        group: Group1


# # Set OWNERSHIP of file
#     - name: Set ownership
#       ansible.windows.win_owner:
#         path: C:\Shared
#         user: User1


  

```
