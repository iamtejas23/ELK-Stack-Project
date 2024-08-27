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
--
![Image](https://i.imgur.com/FQkT8YG.png)

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
--
![Image](https://i.imgur.com/QgpY0iI.png)


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

--
``
3. Install Logstash
``

```
sudo apt-get install logstash
```

```
cd /etc/logstash/conf.d/ 
vim apache.conf
```

```
input {
  beats {
    port => "5044"
  }
}

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
}

output {
  elasticsearch {
    hosts => ["http://172.31.88.220:9200"]     -----> chnage IP Of Elasticserch
    index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
  }
  stdout {
    codec => rubydebug
  }
}
```

### Start Logstash and check its status:

```
sudo systemctl start logstash 
sudo systemctl status logstash
```

### Verify Logstash is running by checking the logs:
```
tail -f /var/log/logstash/logstash-plain.log
```

----
``
4. Deploy the Client Instance
``

```
sudo apt-get update
sudo apt-get install apache2 -y
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.17.6-amd64.deb
sudo dpkg -i filebeat-7.17.6-amd64.deb
```

### Configure Filebeat by editing the filebeat.yml file:

```
sudo nano /etc/filebeat/filebeat.yml
```

Set the hosts field to the private IP of the logstashkibana instance.
Save and exit the file.

### 2 images

```
sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["<elasticsearch_IP>:9200"]'

```

```
sudo filebeat modules enable system
sudo filebeat modules enable apache
```

```
systemctl restart filebeat.service
filebeat test output
```
