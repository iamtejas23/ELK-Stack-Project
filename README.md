# ELK-Stack-Project

##Launch an EC2 instance with Ubuntu, choosing t2.medium as the instance type.

``1.install elasticsearch`` 
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
