Role Name
=========
create-user-by-prompt-name

About this role: 
------------
This role is used to a custom create user

You have to enter you username and Password

Supporting libary install on your control mode
-----------------
```
pip install passlib
```

Define the interpreter
-------------
In Var file I have define

Initilize the repo
---------------
ansible-playbook role init create-user-by-prompt-name

Run the Repo
--------------------
Ansible-playbook create-user-by-prompt-name/create-user.yaml