
# Create storage container
    docker run -v /var/lib/cassandra  --name cass_data busybox true

# run cass with volume
    docker run -i -t --rm --volumes-from cass_data \
      -e HOST_IP=${COREOS_PRIVATE_IPV4} \
      -e CASSANDRA_SETTINGS_MAXHEAPSIZE=512M \
      -e CASSANDRA_SETTINGS_HEAPNEWSIZE=50M \
      -e CASSANDRA_SETTINGS_CLUSTERNAME=cass_01 \
      -e CASSANDRA_SETTINGS_SEEDS=127.0.0.1 \
      -p 7000:7000 \
      -p 9160:9160 \
      172.17.8.101:5000/petee/centos-cassandra20 \
      /bin/bash

# create keyspace
CREATE KEYSPACE awesomesauce WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 2 };
