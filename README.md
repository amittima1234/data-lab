# Data Lab: nifi + splunk 
Deploying nifi and splunk as a code on your local machine. 


## .env file

To run this lab, you'll need an .env file in root directory with this environment variables.


### nifi
`NIFI_HTTPS_GUI_PORT` -> the standard port is `8000`.  
`NIFI_MIN_GENERAL_LISTEN_PORT` -> read [this](#nifi-general-listen-ports) below.  
`NIFI_MAX_GENERAL_LISTEN_PORT` -> read [this](#nifi-general-listen-ports) below.    
`NIFI_HTTP_LOG_LISTEN_PORT` -> `8008` is recommended.  
`NIFI_ADMIN_USERNAME` -> it is recommended to keep it `admin`.  
`NIFI_ADMIN_PASSWORD` -> at least 8 characters, with letters and numbers.   

### splunk
`SPLUNK_ADMIN_PASSWORD` -> using the same password as the nifi admin is recommended. 
`SPLUNK_HTTP_UI_PORT` -> the standard port is `8000`.  
`SPLUNK_HTTP_INGEST_PORT` -> the standard port is `8088`.  


### nifi general listen ports
One of nifi's biggest advantages is the ability to use wide range of logic ports to collect data from different sources. To ensure NiFi can properly ingest data streams, the Docker container must be configured to expose the necessary TCP and UDP ports (e.g., `514` for Syslog, `8088` for HEC).

In the .env file, we use two variables to define this range of ports:  
`NIFI_MIN_GENERAL_LISTEN_PORT` -> defines the minimal value of this range.   
`NIFI_MAX_GENERAL_LISTEN_PORT` -> defines the maximum value of this range.  

For example, when we use this configuration:  
`NIFI_MIN_GENERAL_LISTEN_PORT=9000`   
`NIFI_MAX_GENERAL_LISTEN_PORT=9010`  
docker will expose **ALL** ports between `9000` and `9010` (including them both) and data can be ingested to the nifi container via these ports.

> [!CAUTION]  
> Don't use a range too big because it will consume all of the ram on your machine. Keep it simple with no more than 10-20 ports.
