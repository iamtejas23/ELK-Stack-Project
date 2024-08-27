# ELK-Stack-Project

``1.install elasticsearch`` 
## Launch an EC2 instance with Ubuntu, choosing t2.medium as the instance type.

```
#update
sudo apt-get update
#Install the default JDK and JRE
sudo apt install default-jdk default-jre -y
#Add Elasticsearch’s GPG key and install necessary packages
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add 
sudo apt-get install apt-transport-https
#Add Elasticsearch’s APT repository
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee –a /etc/apt/sources.list.d/elastic-7.x.list
#Update
sudo apt-get update -y
#Install Elasticsearch
sudo apt-get install elasticsearch

```

### Configure Elasticsearch by editing the elasticsearch.yml file:
```
sudo nano /etc/elasticsearch/elasticsearch.yml
```
``
### make like similar
# ---------------------------------- Network -----------------------------------
#
# By default Elasticsearch is only accessible on localhost. Set a different
# address here to expose this node on the network:
#
network.host: 172.31.87.81     ---> Add
#
# By default Elasticsearch listens for HTTP traffic on the first free port it
# finds starting at 9200. Set a specific HTTP port here:
#
http.port: 9200                ---> Add
#
# For more information, consult the network module documentation.
#
# --------------------------------- Discovery ----------------------------------
discovery.type: single-node    ---> Add
# Pass an initial list of hosts to perform discovery when this node is started:
# The default list of hosts is ["127.0.0.1", "[::1]"]
###

Set the network.host to the private IPv4 address of your instance.
Save and exit the file.
``
