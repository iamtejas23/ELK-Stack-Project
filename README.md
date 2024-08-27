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
Set the network.host to the private IPv4 address of your instance.
Save and exit the file.
``
[img]https://i.imgur.com/FQkT8YG.png[/img]

### Start Elasticsearch and check its status:
```
sudo systemctl start elasticsearch 
sudo systemctl status elasticsearch
```


``
2. Deploy Logstash and Kibana Instance
``
## EC2 instance with Ubuntu, naming it logstashkibana, and choose t2.medium.

```
sudo su
sudo apt-get update
#java-installing
sudo apt install default-jdk default-jre -y
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add 
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee –a /etc/apt/sources.list.d/elastic-7.x.list
apt-get update -y
sudo apt-get install kibana
```

### Configure Kibana by editing the kibana.yml file:
```
sudo nano /etc/kibana/kibana.yml
```

``
Set server.host to the private IP of the logstashkibana instance.
Set elasticsearch.hosts to the private IP of the Elasticsearch instance.
Save and exit the file.
``

### Start Kibana and check its status:
```
sudo systemctl start kibana 
sudo systemctl status kibana
```
