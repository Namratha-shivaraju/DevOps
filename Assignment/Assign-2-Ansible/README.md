# ANSIBLE GIT EXAMPLE

## Referred article: https://www.middlewareinventory.com/blog/ansible-git-example/

### NOTE - Generate a personal access token

## STEP 1-

Install Ansible 

Installation guide: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## STEP 2-

Create a simple nodejs app and upload it in a private repository on Github.

## STEP 3-

Store the github username and token in a file using ansible-vault.

Run command `ansible-vault create secrets.yml` to create a vault password.

After the creation, secrets.yml file will open, enter the below lines-

`gituser: [username]`

`gitpass: [personal access token]`

## STEP 4-

Create EC2 instance 

ICMP, HTTP, HTTPS, Custom TCP must be included while creating instance.

## STEP 5-

Create ansible_hosts

In the working directory, run `touch ansible_hosts` to create a file.

Open the text editor and type the follwing lines-

`[nodeserver]`

`PUBLIC IP ADDRESS HERE ansible_user=ec2-user ansible_port=22 ansible_ssh_private_key_file=`

`[nodeserver:vars]`

`ansible_ssh_common_args="-o StrictHostKeyChecking=no"`

## STEP 6-

Create an ansible playbook - gitexample.yml

Make the following changes mentioned below-

In the "Change the ownership of the directory part"- change owner to ec2-user (or name of your ec2 instance)

In "validating the port is open" - change the port number to node.js port number

In "Download the NodeJs..." - change the path to your github private repo.

## STEP 7-

Run the below commands to connect and run the playbook

`ansible nodeserver -m ping -i ansible_hosts`

`ansible-playbook gitexample.yml --ask-vault-pass`

## STEP 8-

After successful compilation, open the browser -

`http://<Public ip address>:<portnumber>`
