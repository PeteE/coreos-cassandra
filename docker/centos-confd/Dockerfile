FROM centos

MAINTAINER Pete Erickson <petee@mindtouch.com>

# download and install confd
#RUN yum install -y wget
#RUN wget -O /usr/local/bin/confd https://github.com/kelseyhightower/confd/releases/download/v0.4.0-beta3/confd-0.4.0-beta3-linux-amd64
#RUN chmod +x /usr/local/bin/confd

# compiled from https://github.com/kelseyhightower/confd (master @ 413eddce78)
# This version has support for using env vars as a backend:  https://github.com/kelseyhightower/confd/blob/master/docs/env-getting-started.md
ADD confd /usr/local/bin/confd

# create confd dir
RUN mkdir -p /etc/confd/conf.d
RUN mkdir -p /etc/confd/templates

CMD ["/bin/bash"]
