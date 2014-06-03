FROM 172.17.8.101:5000/petee/centos-confd

MAINTAINER Pete Erickson <petee@mindtouch.com>

# add datastax repo
ADD datastax.repo /etc/yum.repos.d/

# install JRE - note, cass requires the oracle JRE so you'll need to accept license agreement
ADD jre-7u60-linux-x64.rpm /tmp/
RUN rpm -i /tmp/jre-7u60-linux-x64.rpm
RUN rm /tmp/jre-7u60-linux-x64.rpm

# install cass
RUN yum install -y vim initscripts
RUN yum install -y cassandra20 dsc20

# set alternatives
RUN alternatives --install /usr/bin/java java /usr/java/jre1.7.0_60/bin/java 200000

# install jna
# commented out since it crashes my vagrant coreos vm :(
#RUN yum install -y wget tar
#RUN wget -q -O /tmp/jna-4.1.0.tar.gz https://github.com/twall/jna/archive/4.1.0.tar.gz
#RUN cd /tmp; tar xf jna-4.1.0.tar.gz
#RUN cp /tmp/jna-4.1.0/dist/jna.jar /usr/share/cassandra/lib/
#RUN rm -rf /tmp/jna-4.1.0*

# create cassandra config template
RUN mv /etc/cassandra/conf/cassandra-env.sh /etc/cassandra/conf/cassandra-env.sh.orig
RUN mv /etc/cassandra/conf/cassandra.yaml /etc/cassandra/conf/cassandra.yaml.orig

# add confd templates
ADD confd/cassandra-env.sh.tmpl /etc/confd/templates/
ADD confd/cassandra-env.sh.toml /etc/confd/conf.d/
ADD confd/cassandra.yaml.tmpl /etc/confd/templates/
ADD confd/cassandra.yaml.toml /etc/confd/conf.d/

# add run script
ADD run.sh /

# cleanup
RUN yum clean all

EXPOSE 7000 9160
CMD ["/run.sh"]
