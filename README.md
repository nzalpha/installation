# installation

useradd ansible
passwd ansible

# useradd does not create home directory

# Check if the user exists
getent passwd ansible

# If the user does not exist, create the user with a home directory
sudo adduser ansible

# If the user exists but doesn't have a home directory, create it
sudo mkdir /home/ansible
sudo chown ansible:ansible /home/ansible
sudo chmod 755 /home/ansible

# Copy skeleton files to the new home directory (optional)
sudo cp -r /etc/skel/. /home/ansible/
sudo chown -R ansible:ansible /home/ansible

# Switch to the user
su - ansible


# We need to make the necessary entrys in to sudo file, so ansible user can go with sudo and also with password less access.
visudo
ansible         ALL=(ALL)       NOPASSWD: ALL

# Next, by default these machines cant be logged in using the password. So make sure the password based authentication is enabled
vi /etc/ssh/sshd_config and set PasswordAuthentication yes


# Generate the SSH key in the Ansible Server, this generates public key in jump machine
ssh-keygen

# Copy the public key in .ssh of jump machine and copy to authorized keys in Target machine 

mkdir ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
Copy content of pub key to ~/.ssh/authorized_keys



# Restart the sshd service
service sshd restart

#ssh
ssh ansible@<private ip>
