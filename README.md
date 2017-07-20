# Launching VMR via Ansible

This project contains ansible scripts to automate the launching of Solace VMR.

The ansible playbook launches a VMR, perform a 'show redundancy' using SEMPv1 and 'create queue' using SEMPv2.

## Prerequisite
1. Configure an AWS Security Group which allows inbound traffic to ports 80,8080,22,2222,55555 within the VPC that the VMR is to be launched
2. (Optional) Launch a vanilla Solace VMR manually and create an admin CLI user, plus other resources as appropriate. Take a snapshot of the VMR instance. Record the AMI ID.

## Steps
1. Install Ansible
    - For example in Ubuntu distribution:
        - <code>sudo apt-get install ansible</code>
2. Set up the AWS access and secret keys in the environment settings; 
    - E.g. run the following from shell
        - export AWS_ACCESS_KEY_ID="your access key id"
        - export AWS_SECRET_ACCESS_KEY="your secret access key"
    
3. Modify vmr-vars/vmr.yml
    - update all the ec2_* values accordingly, specifically
    - Update the ec2_image to the AMI ID of the VMR to be launched, can be vanilla VMR or AMI from Prerequisite #2
    - Update the ec2_keypair to the keypair to be used
4. Launch
    - <code>ansible-playbook -vv -i localhost, -e "type=vmr" provision-vmr.yml</code>

## Note
The example of launching SEMPv1 and SEMPv2 commands via ansible is in roles/provision-vmr/tasks/main.yml.
