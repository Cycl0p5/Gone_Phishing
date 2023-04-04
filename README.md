# Gone_Phishing
Infrastructure as code to set up a phishing campaign

# Authors and acknowladgments
Written by Cycl0p5
Inspired by Black Hills Information Security Ralph May and his youtube video

BHIS | How to Build a Phishing Engagement - Coding TTP's - Ralph May

https://www.youtube.com/watch?v=VglCgoIjztE

https://github.com/ralphte/build_a_phish

## Overview
Build a Phish consist of a Ansible playbook to deploy a phishing engagement in the cloud. The Playbook combines both Terraform & Ansible to deploy and configure virtual machines for different use cases. This playbook is highly customizable and includes operational security out of box. The design of this playbook is much more than automation. This playbook implements real world TTP’s to improve OPSEC, lower operational cost and speedup deployment time. This project is the real-world demonstration from the Black Hills Information Security Webcast “How to Build a Phishing Engagement - Coding TTP's”

## Features
Pure Ansible playbook with low dependencies and easy modification.
Security from the ground up
Docker containers for each application.
Designed around a phishing engagment

## Containers

Logo	Service	Image
	Evilginx2	warhorse/evilginx2
	Gophish	gophish/gophish
	Nginx	nginx
	Mitmproxy	mitmproxy

## Supported Cloud Providers

Logo	Provider	Services
	Digital Ocean	Droplet,DNS
	Azure	CDN

## Requirements

  - Managment Domain
  - Linux or MacOs
  - Ansible
  - Terraform
  - (optional) Secrets Provider cli
  -   - lpass (lastpass)
  -   - op (onpassword)
  -   - bw (Bitwarden)

## Setup

### DNS records
You will need a managment domain. This domain can be the same domain used for phishing emails. After you buy a domain set the name server records to Digital Ocean.

Im going to make a docker for all of this eventually and just run it without a vm or wsl

### 1. Install Ansible, Terraform, Docker, & git
#### Ansible (can be in virtural machine or native on windows under kali app, must be in linux)
  
  >sudo apt update
  
  >sudo apt install ansible
  
#### Terraform
- Best to download the binary and unzip and follow manually install
- https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
 
>sudo apt-get install unzip

>unzip terraform_1.4.4_linux_amd64.zip

>sudo mv terraform /usr/local/bin/

>terraform 
 
 #### Docker
  https://bughacking.com/how-to-install-docker-on-kali-linux-wsl2/

  >sudo mkdir -m 0755 -p /etc/apt/keyrings
  
  >curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

  >echo \
  >"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  >"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  >sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  >sudo apt-get update
  
  >sudo apt-get install docker
  
  >sudo docker run hello-world
  
  #### Git
  
  >sudo apt-get install git
  
  ### 2. Install Ansible General Modules
  
  >ansible-galaxy collection install community.general
  
  ### 3. Git clone repo
  
  >git clone https://github.com/ralphte/build_a_phish
  
  ### 4. Customize the variables inside the vars folder.
  
  ### 5. Create API Keys for VM providers
  
## Usage

### Create

'ansible-playbook deploy.yml --tags phish'

### Destroy

'ansible-playbook destroy.yml --tags phish'

### Secrets

You have three choices

1. Hard code (Don't do this)
2. Use a Secrets CLI https://docs.ansible.com/ansible/latest/collections/community/general/lastpass_lookup.html
3. Use Ansible Vaults https://docs.ansible.com/ansible/latest/user_guide/vault.html

### Evilginx2
If you would like to modify the phishlet or change lures, please edit the following files.

'roles\evilginx2-docker\templates\config.yaml.j2'

'roles\evilginx2-docker\templates\o365.yaml.j2'

You can check the evilginx logs for session data with the following command.

>docker logs evilginx2

### Gophish

You can access gophish via the hostname set for "gophish_admin_hostname"

To get the password on first login check the docker logs

>docker logs gophish

### Mitmproxy

You can access Mitmproxy via the hostname set for "mitmproxy_hostname"

The mitmproxy web interface allows you to see the RAW traffic between evilginx2 and your target server. You can use this to check for problems and remove any IOC's. Mitmproxy is a dignostic tool to inspect https traffic.

## Development

Does none of this work for you? Submit a issue and I will see what the problem is.

Want to add a cool new feature shoot me that sweet pull request.

## Acknowledgements

Gophish https://getgophish.com/

Evilginx https://github.com/kgretzky/evilginx2

Mitmproxy https://github.com/mitmproxy/mitmproxy

Ansible roles from https://github.com/geerlingguy
  
