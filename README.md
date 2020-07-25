# Ansible-Kubernetes-Mysql
Ansible Playbooks use to deploy kubernetes infrastructure with mysql containers. This has been verified on Centos 7.6 64 bit operating systems.

Preapre Two VMs using centos iso file with atleast 2GB Ram, 2 processors and HDD depending on the needs.

Once VM is ready, login into it with root & given password during setup and update with "yum update -y"

After update complete, make and entry of each hosts( Master and Worker Node) in /etc/hosts file for name resolution.
"vi /etc/hosts"

After making the entries, create passwordless ssh for Ansible in between master node and worker node.

At master node:
$ ssh-keygen  [Keep all the values as default]

Now copy the generated key in all the node's .ssh/known_host for local passwordless acess:
$ ssh-copy-id root@<master_node_IP>   [Execute this with all the master node's IPs)
$ ssh-copy-id root@<worker_node_IP>   [Execute this with all the worker node's IPs)

After passwordless ssh is done clone the ansible script as below:
Clone this repository : https://github.com/shailendra-singh93/Ansible-Kubernetes-Mysql.git
$ git clone https://github.com/shailendra-singh93/Ansible-Kubernetes-Mysql.git

Update Ansible hosts file and make entries for all the Master node in Master group & worker node in Worker group.
$cd Ansible-Kubernetes
$ vi hosts

After adding all the Node details in hosts, Now execute the Ansible command to deploy the kubernetes cluster:
$ ansible-playbook -i hosts /root/Ansible-kubernetes/deploy-cluster.yml

After cluster is created on master node, Join the worker nodes in cluster with below ansible command and script:
$ ansible-playbook -i hosts /root/Ansible-kubernetes/join-workers.yml

These will create the kubernets cluster on Master nodes and join the worker nodes.

To reset the cluster and remove all the pakcages, execute the below script with ansible command:
$ ansible-playbook -i hosts /root/Ansible-kubernetes/quick-uninstall.yml

ADDED Feature wiith this repository ( Bonus):

We can execute below script to create containers for our cluster as per our requirement for different projects [We will need to modify Containers/Dockerfile & app.yaml file]:
$ $ ansible-playbook -i hosts /root/Ansible-kubernetes/create-containers.yml

This will create containers on worker nodes after downloading the required image from docker hub public registry.

Thanks Guys.
For any more details or any issue please create an issue and i will reply ASAP.
See you soon,
Bye




