# Server Configuration:
Set up three servers: one as the master server and the other two as nodes. 

## ANSIBLE Master SERVER:
change settings --> behavior(ansible) --> connection (time -10)
```
sudo su
sudo yum update
sudo amazon-linux-extras install epel -y
sudo yum --enablerepo epel install ansible -y
ansible --version
python --version
```
### Create a user
```
useradd ansible
passwd ansible
```
Enter New password

Now In visudo(root to run)
`ansible    ALL=(ALL)    NOPASSWD: ALL`
```
cd /etc/ansible
```
Do ```ls``` to see all directories inside the ansible dir 
```
vi hosts
```

**create group using**
Ex. [devops]--> here, devops is a group name.
Then mention private ip address of 1st, 2nd , nth node in next line
   
```
vi ansible.cfg
```
**Uncomment** ```inventory``` and ```sudo_user```
switch to ansible user
```
su ansible
cd /home/ansible
```
create a key in master
```
ssh-keygen
```
change config settings
```
sudo su
vi /etc/ssh/sshd_config
```
```password authentication``` yes```
```
systemctl restart sshd
```
switch back to su ansible
copy key to 1st node
```
ssh-copy-id ansible@private_ip(node1)
```
Try to login node1
```
ssh ansible@private_ip(node1)
```
exit
```
ssh-copy-id ansible@private_ip(node2)
```
try to login node2
```
ssh -p 22 ansible@private_ip(node2)
```
exit

## NODE 1:
change settings --> behavior(NODE2) --> connection (time -10)
```
sudo su
visudo
```
Root to run
```ansible    ALL=(ALL)    NOPASSWD: ALL```
```
vi /etc/ssh/sshd_config
```
```permission login``` and ```password authentication``` ```yes```
```
service sshd restart
```
create ansible user
```
useradd ansible
passwd ansible
```
Enter a password then switch to ansible user
```
su ansible
cd /home/ansible
```
After installing software from ansible server check here using its name --version

## NODE 2:
change settings --> behavior(NODE2) --> connection (time -10)
```
sudo su
visudo
```
Root to run
```ansible    ALL=(ALL)    NOPASSWD: ALL```
```
vi /etc/ssh/sshd_config
```
```permission login``` and ```password authentication``` ```yes```
```
service sshd restart
```
create ansible user
```
useradd ansible
```
Enter a password and switch to ansible user
```
su ansible
cd /home/ansible
```
After installing software from ansible server check here using its name --version


