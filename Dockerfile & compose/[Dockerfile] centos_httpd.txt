FROM  centos:latest

LABEL AUTHOR=ragesh \
      VERSION=0.1 \
      EMAIL=ragesh@gmailcom

RUN cd /etc/yum.repos.d/ \
&& sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
&& sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-* \
&& yum -y update \
&& yum install -y httpd 
      

COPY  index.html /var/www/html/index.html

EXPOSE 80

ENTRYPOINT apachectl -D FOREGROUND