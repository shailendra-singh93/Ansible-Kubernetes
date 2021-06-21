FROM centos:centos8
MAINTAINER The CentOS Project <cloud-ops@centos.org>

RUN yum -y update; yum clean all
RUN yum -y install epel-release
RUN yum -y install python3-pip
RUN pip3 install --upgrade pip
RUN pip3 install Flask oslo_utils webob flask_sqlalchemy oslo_db flask_script flask_migrate flask_restful
RUN yum -y install git
RUN git clone https://github.com/opentechfn/medhavi.git

EXPOSE 8000
CMD ["python3", "/medhavi/wsgi.py"]
