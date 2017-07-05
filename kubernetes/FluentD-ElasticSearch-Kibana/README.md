Centralized log collection in Kubernetes cluster using FluentD, ElasticSearch and Kibana. 
The kubernetes 1.6 cluster I configured without SSL certificates, so additional settings are to be done to override the default ssl connection.
Fluentd fails to connect to kubernetes  
 [error]: config error file="/etc/td-agent/td-agent.conf" error="Invalid Kubernetes API v1 endpoint https://10.100.0.1:443/api: SSL_connect returned=1 errno=0 state=error: certificate verify failed"
 [warn]: process died within 1 second. exit

It is because kubernetes API server was not using SSL, so to connect kubernetes with HTTP, I created a config map for the fluentd’s configuration file /etc/td-agent/td-agent.conf, this file will have kubernetes API server’s non secure URL and this will override the default https connection. 
So a config map fluentd-config is created along with the daemon set in the fluentd-es-ds.yaml file.
