# awx-17.1.0 up to instalation only
Old interface up to **awx-15.0.1**
New Interface from **awx-16.0** 

*Tested:  Rocky Linux 8.5*

`dnf install epel-release`
`dnf install git gcc gcc-c++ ansible nodejs gettext device-mapper-persistent-data lvm2 bzip2 wget` 

If you need Docker, uninstall `runc` and its dependencies, if you need podman, disable the docker-CE repo "yum-config-manager --disable Docker-CE"
 `yum autoremove  runc`   or  `dnf remove @container-tools`
 
Install Docker:
```shell
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
dnf install docker-ce
systemctl start docker && systemctl enable docker
sudo usermod -aG docker $USER
alternatives --set python /usr/bin/python3
```

Download AWX packages:
```shell
wget https://github.com/ansible/awx/archive/refs/tags/17.1.0.tar.gz
tar xvf 17.1.0.tar.gz
wget https://github.com/ansible/awx/releases/tag/15.0.1.tar.gz
tar xvf 15.0.1.tar.gz
```

Update configiration:
```shell
openssl rand -base64 30   # Generate secret key 

```

```
cd awx/installer
vim inventory
secret_key=               # Add secret key
admin_password=password
awx_alternate_dns_servers="1.1.1.1,1.0.0.1"
# for better security change default passwords
pg_password=some_database_password             
rabbitmq_password=a_messaging_password

mkdir /var/lib/pgdocker
ansible-playbook -i inventory install.yml
```


Disable SELinux
```shell
vim  /etc/sysconfig/selinux
SELINUX=disabled
```

Configure firewalld:
```shell
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```



# awx-18.0.0 from version
**Kubernetis** TODO
https://www.rogerperkin.co.uk/network-automation/ansible/how-to-install-ansible-awx/