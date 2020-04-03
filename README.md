# Installation of AWX

## Linux version

rpm -q centos-release

centos-release-7-7.1908.0.el7.centos.x86_64

## Install packages

systemctl stop firewalld; systemctl disable firewalld

yum -y install epel-release

yum -y install git gcc gcc-c++ lvm2 bzip2 gettext nodejs device-mapper-persistent-data python-pip yum-utils ansible vim yum net-tools

yum-config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

yum install -y docker-ce

systemctl start docker
systemctl enable docker

pip install docker-compose

## Install AWX

git clone https://github.com/ansible/awx.git

git clone https://github.com/ansible/awx-logos.git

cd awx/

sed -i "s|^dockerhub_base=ansible|#dockerhub_base=ansible|g" installer/inventory

sed -i -E "s|^#([[:space:]]?)awx_official=false|awx_official=true|g" installer/inventory

mkdir -p /opt/awx-psql-data

sed -i "s|^postgres_data_dir.*|postgres_data_dir=/opt/awx-psql-data|g" installer/inventory

mkdir -p /opt/awx-projects

sed -i -E "s|^#([[:space:]]?)project_data_dir=/var/lib/awx/projects|project_data_dir=/opt/awx-projects|g" installer/inventory

openssl rand -base64 10
ed8tTyhLY6HfLAxy

sed -i 's/^admin_password=.*/admin_password=ed8tTyhLY6HfLAxy/g' installer/inventory

openssl rand -base64 30
AmySdn4MTc1Z15rxHiBitP52n2M1UJmBMQjgH09x

sed -i 's|secret_key=.*|secret_key=AmySdn4MTc1Z15rxHiBitP52n2M1UJmBMQjgH09x|g' installer/inventory

mkdir -p /opt/awx-ssl/

openssl req -subj '/CN=ansible-lab.sinog.si/O=SINOG/C=SI' \
	-new -newkey rsa:2048 \
	-sha256 -days 1365 \
	-nodes -x509 \
	-keyout /opt/awx-ssl/awx.key \
	-out /opt/awx-ssl/awx.crt

cat /opt/awx-ssl/awx.key /opt/awx-ssl/awx.crt > /opt/awx-ssl/awxweb.pem

sed -i -E "s|^#([[:space:]]?)ssl_certificate=|ssl_certificate=/opt/awx-ssl/awxweb.pem|g" installer/inventory

grep -v '^#' installer/inventory | grep -v '^$'

ansible-playbook -i installer/inventory installer/install.yml

# Links

  http://yallalabs.com/devops/how-to-install-ansible-awx-without-docker-centos-7-rhel-7/

  https://medium.com/swlh/ansible-awx-installation-5861b115455a

  https://ahmermansoor.blogspot.com/2019/09/install-ansible-awx-with-docker-compose-on-centos-7.html

  https://www.howtoforge.com/tutorial/how-to-install-ansible-awx-with-docker-on-centos/

  https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

  https://gist.github.com/dasgoll/7073664f0f7f73f4aa3e7cf8c95a8dbc

  https://mybrainimage.wordpress.com/2017/02/05/docker-change-port-mapping-for-an-existing-container/

  https://www.unixarena.com/2018/10/ansible-how-to-install-and-configure-awx.html/
