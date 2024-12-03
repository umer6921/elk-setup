# Follow to install the ELK with fleet server



## Download and install the public signing key:
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

## apt-transport-https package on Debian before proceeding
```sudo apt-get install apt-transport-https```

## Install elastic 8 debdian file

Refer the ELK official site for latest version of ELK. This is version 8.

```
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

```
sudo apt-get update && sudo apt-get install elasticsearch
```

## Status check of elasticsearch

```
systemctl status elasticsearch.service 
```

## Changes in file

```
 nano /etc/elasticsearch/elasticsearch.yml
```

Comment out if commented or make these changes

```
cluster.name: my-application
network.host: 0.0.0.0
http.port: 9200
http.host: 0.0.0.0
```

## Restart the elasticsearch
```
systemctl restart elasticsearch.service
```
```
sudo systemctl enable elasticsearch
```

## Install kibana
```
sudo apt-get update && sudo apt-get install kibana
```

## Edit the file of kibana.yml

```
nano /etc/kibana/kibana.yml
```

Uncomment it or edit it with the same value

```
server.port: 5601
server.host: "0.0.0.0"
```

## Restart it
```
sudo systemctl restart kibana
```
```
sudo systemctl enable kibana
```
## Extract the login detail of kibana

Go to this path
```
cd /usr/share/elasticsearch/bin/
```
### Create kibana token to login

```
./elasticsearch-create-enrollment-token --scope kibana
```

### Reset the login password 
```
./elasticsearch-reset-password -u elastic
```


## Access the elasticsearch server

Open these port before access it

```
https://server-ip:9200/
```

Enter the same username and password of kibana

## Access kibana dashboard

```
server-ip:5601
```


