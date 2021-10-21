# MASTER image - used to create the master container to manage hosts

#Base image created with ansible installed over centos
FROM aernesto24/centos_ansible:latest

#Install some required packages, iputils is aprt of the base image
RUN dnf update -y
RUN dnf install net-tools -y
RUN dnf install man vim openssh-server python3 -y

# ensure that required directories are created
RUN mkdir /var/ansible
RUN mkdir /var/run/sshd
RUN mkdir /root/.ssh
RUN /usr/bin/ssh-keygen -A

# copy content of ansible directory from local disk to file system inside Docker image
COPY ./ansible_files /var/ansible/

# change working directory
WORKDIR /var/ansible

# generate RSA key pair to allow master to communicate with managed nodes
# default private key passphrase is '12345' (not a good idea for production environment ;)
RUN /usr/bin/ssh-keygen -t rsa -C "master key" -f master_key