# Requirements
1. AWS instances with CLI credentials

2. Ansible version 2.16.3
- Install:  sudo apt install ansible

2. AWS ansible collection
- Install: ansible-galaxy collection install amazon.aws

3. Python version 3.12
- Should be preinstalled
- If not run: sudo apt install python3-full

4. Python boto3 library
- install: sudo apt install python3-boto3


# Broad overview of the different steps/stages of the pipeline
1. Install EC2 Infrastructure Playbook
    1. Logs into AWS using the credentials in ~/.aws/credentials
    2. Generates a SSH Key, then saves it for use later
    3. Creates a security group, that allows SSH from only the person who ran the script
        - Allows connection to anyone on 25565 port
    4. Creates the EC2 instance
    5. Allocates a ellastic IP
2. Deploy Minecraft Server Playbook
    1. SSHs into the server with the SSH key
    2. Installs all dependencies needed
    3. Downloads a minecraft jar file, from specified URL in all.yml
    4. Creates the minecraft service
    5. Enables it on boot


# Tutorial to run the code/scripts/provisioning/configuration on your local or from a VM (up to you, mostly mentioning it for Windows users out there)
1. Use some variety of Ubuntu. This was written and test using WSL Ubuntu, but other options will most likely work.
2. Install all the packages in the requirement section.
3. Copy and paste your aws cli crentials into ~/.aws/credentials. Make sure the encoding is UTF-8 
4. Edit, all.yml configuration file.
    - Edit ram min & max
    - Edit minecraft_version_url: With prefered version's jar file. Link to a repository with server jars is in the resources page. 
5. Run, ansible-playbook 1.InstallEC2Infrastructure.yml
6. Run, ansible-playbook -i hosts 2.DeployMinecraftServer.yml
    - It will prompt you for authenticating a key, enter yes.
7. The playbook ran on step 6, should print out a server IP. Copy and paste this into minecrafts server browser, to play minecraft.

# Resources/Sources used
    - AWS ansible modules docs: https://docs.ansible.com/projects/ansible/latest/collections/amazon/aws/ 
    - Ansible documentation: https://docs.ansible.com/
    - Minecraft, creating server tutorial: https://help.minecraft.net/hc/en-us/articles/360058525452-How-to-Setup-a-Minecraft-Java-Edition-Server
    - Minecraft.wiki: Settingup java server: https://minecraft.wiki/w/Tutorial:Setting_up_a_Java_Edition_server 
    - Repository of server jar downloads: https://gist.github.com/cliffano/77a982a7503669c3e1acb0a0cf6127e9?permalink_comment_id=5104349