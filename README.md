# Instalalation of AWX

rpm -q centos-release
centos-release-7-7.1908.0.el7.centos.x86_64

systemctl stop firewalld; systemctl disable firewalld

yum -y install epel-release

yum -y install git gcc gcc-c++ lvm2 bzip2 gettext nodejs device-mapper-persistent-data python-pip yum-utils ansible vim yum net-tools

yum-config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

yum install -y docker-ce

systemctl start docker
systemctl enable docker

pip install docker-compose



# Links

  http://yallalabs.com/devops/how-to-install-ansible-awx-without-docker-centos-7-rhel-7/

  https://medium.com/swlh/ansible-awx-installation-5861b115455a

  https://ahmermansoor.blogspot.com/2019/09/install-ansible-awx-with-docker-compose-on-centos-7.html

  https://www.howtoforge.com/tutorial/how-to-install-ansible-awx-with-docker-on-centos/

  https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

  https://gist.github.com/dasgoll/7073664f0f7f73f4aa3e7cf8c95a8dbc

  https://mybrainimage.wordpress.com/2017/02/05/docker-change-port-mapping-for-an-existing-container/

  https://www.unixarena.com/2018/10/ansible-how-to-install-and-configure-awx.html/
