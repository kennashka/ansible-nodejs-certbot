# Ansible Nodejs Certbot
Using Ansible to install a stand alone Nodejs Server SSL Cert (Only for Ubuntu Systems)


### Version

1.1.0

## Required: Ansible Install for Ubuntu and Forever JS

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install ansible

```
```bash
sudo npm install forever -g
```

## Role Installation 

```bash
ansible-galaxy install 

```

## Configure Hosts File (Optional Way to Give Permissions for Accessing Server)

1. Replace (12.345.678.90) with your target server ip/domain address in hosts file 
2. Add the file location to ssh pem key in hosts file (ex. ansible_ssh_private_key_file= directory/location/to/your/pem/key/file)


## Configure "tasks/certbot.yml" File:
 Replace File Variables With Targeted Host Machine, Default User (root permission is needed to run certain tasks), Your Web Domain Info, Nodejs App Folder Name, and Email
 
```yml
- hosts: addyourhost
  remote_user: ubuntu
  become: yes
```
```yml
  vars:
    domain_name: 'yoursite.com'
    domain_name2: 'www.yoursite.com'
    app_folder: 'nodeappfoldername'
    letsencrypt_email: 'mail@yoursite.com'
 ```   
## Verify:
1. This ansible role is assuming you have an app.js file(if not you need to replace the name in the file) 
2. Port 80 or 4443 needs to be available (Certbot Requires port 80 or 443 to be available)
3. Default location path for app and remote user
4. App is running for Certbot challenge (/.well-known/acme-challenge)


## Run
```bash
ansible-playbook -i ./hosts tasks/certbot.yml
```
