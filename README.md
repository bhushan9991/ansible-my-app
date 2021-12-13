# Ansible code to create remote user, group, clone repository from bitbucket using the private key and set up the project

>Ansible version = ansible 2.9.6

**Ansible code**
- In this project, we are going to connect a remote machine using ansible aws dynamic inventory and create a user, group, and clone the application codebase from bitbucket using a private key. Also, installation of required packages to set up the application.
- This project contains playbook.yaml in which all the steps have been written, inventory files that contain remote server details, and some keys.
 
- Let's check the code structure!

```
~/dev/my_app$
.
├── aws_ec2.yaml
├── files
│   └── id_rsa.github
├── group_vars
│   └── linux.yaml
└── playbook.yaml

2 directories, 4 files
```

**Important things you should do before running this project:**

  - Update your aws region in which your remote sever is hosted in aws_ec2.yaml file.
  - There are two ways to use your private key in this project.
      1. Set a path of your existing .ssh private key in playbook.yaml under vars.source_key
          - e.g. /home/bhushan/.ssh/id_rsa.github
      2. Copy your existing private key and encrypt it.
          - Copy it under /my_app/files/ and name it as id.rsa.github. - i.e. /my_app/files/id_rsa.github
          - IMPORTANT: To encrypted a private key use ansible-vault.
              - Ansible-vault Command: ansible-vault encrypt /my_app/files/id_rsa.github

  - Add .pem file (provided by aws to connect your remote server) under /my_app/ directory and update the name in /my_app/group_vars/linux.yaml
      - e.g. /my_app/aws_dev.pem
-----------------------------------------------------------------------------------------------------
Use following command to execute ansible playbook under /my_app/ directory:

  **ansible-playbook -i aws_ec2.yaml playbook.yaml --extra-vars "git_branch=test" --ask-vault-pass**
  - In this command, we are passing the git branch name (e.g. test) as an user provided input in **--extra-vars**
>Note: **--ask-vault-pass** in execution command is used only if encrypted private key is provided.
    
