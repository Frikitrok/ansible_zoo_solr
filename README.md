# ansible_zoo_solr
# Ansible playbooks for deploy zookeepers with solr
### 2 roles to deploy zookeepers and solrCloud 4.10 version to hosts in any amount. Also it remove default collection1 collection/core and add new main collection based on collection1 schema.

## Ansible example command
```
ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i 52.34.69.230,34.210.244.68,54.71.200.23, baseInfra.yml --key-file ~/.ssh/ENDALI_dev.pem -e baseHosts=52.34.69.230,34.210.244.68,54.71.200.23 -u ubuntu
ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i 52.34.69.230, initSolr.yml --key-file ~/.ssh/ENDALI_dev.pem -e solrHost=52.34.69.230 -u ubuntu
```
## Some usefull commands to manage by hands:
### Solr:
```
curl "localhost:8983/solr/admin/collections?action=CREATE&name=test1&numShards=1&replicationFactor=3&property.name=test1&collection.configName=test1"
curl "localhost:8983/solr/admin/collections?action=DELETE&name=test1"
```
### Solr to zookeeper
```
java -Dlog4j.configuration=file:/opt/solr/example/scripts/cloud-scripts/log4j.properties -classpath /opt/solr/example/solr-webapp/webapp/WEB-INF/lib/*:/opt/solr/example/lib/ext/* org.apache.solr.cloud.ZkCLI -cmd upconfig -zkhost localhost:2181 -confdir /tmp/test1 -confname test1
java -Dlog4j.configuration=file:/opt/solr/example/scripts/cloud-scripts/log4j.properties -classpath /opt/solr/example/solr-webapp/webapp/WEB-INF/lib/*:/opt/solr/example/lib/ext/* org.apache.solr.cloud.ZkCLI -cmd linkconfig -zkhost localhost:2181 -collection test1 -confname test1
```
