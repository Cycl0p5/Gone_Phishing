# Gone_Phishing
Infrastructure as code to set up a phishing campaign

# Authors and acknowladgments
Written by Cycl0p5
Inspired by Black Hills Information Security Ralph May and his youtube video

BHIS | How to Build a Phishing Engagement - Coding TTP's - Ralph May https://www.youtube.com/watch?v=VglCgoIjztE
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
### 1. Install Ansible & Terraform
#### Ansible (can be in virtural machine or native on windows under kali app, must be in linux)
  sudo apt update
  sudo apt install ansible
  
#### Terraform
 Best to download the binary and unzip and follow manually install
 https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
 sudo apt-get install unzip
 unzip terraform_1.4.4_linux_amd64.zip
 sudo mv terraform /usr/local/bin/
 terraform (to test install)
 
 #### Docker
  https://bughacking.com/how-to-install-docker-on-kali-linux-wsl2/

  sudo mkdir -m 0755 -p /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

  echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  sudo apt-get update
  

