# ansible-centos-static-server
- setups a simple web server using Centos & Nginx
- creates user and sets up firewall

## Get Started
- Edit hosts file for server ip addresses
- Add public key to "./files/authorized_keys" file
- Edit Test Site: "./files/index.html"
- Rule Ansible: ```ansible-playbook provision.yml```

## Test
- test with Vagrant

### TODO
- setup SSL
  - self signed
  - let's encrypt
