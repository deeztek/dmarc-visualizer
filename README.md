# Deeztek dmarc-visualizer

Analyse and visualize DMARC results using open-source tools.

* [parsedmarc](https://github.com/domainaware/parsedmarc) for parsing DMARC reports,
* [Elasticsearch](https://www.elastic.co/) to store aggregated data.
* [Grafana](https://grafana.com/) to visualize the aggregated reports.

## Pre-requisites

Deeztek dmarc-visualizer requires that you have a fully updated Ubuntu 18.04 (also tested successfully on Ubuntu 20.04) machine with Docker and Docker Compose. You can easily install docker and docker-compose by following the instructions at [https://github.com/deeztek/deeztek-docker](https://github.com/deeztek/deeztek-docker).


Deeztek dmarc-visualizer assumes you will be processing DMARC reports from an IMAP account, so before installation, you must ensure you have the following:

- IMAP e-mail account Server Hostname
- IMAP e-mail account Username
- IMAP e-mail account Password

If you are planning on using Maxmind Geolocation data, you must ensure you have already created a Maxmind account which is now a requirement in order to download the GeoIP2 Country Database.
## Installation

Git clone the Deeztek dmarc-visualizer repository:

`sudo git clone https://github.com/deeztek/dmarc-visualizer.git`

This will clone the repository and create a dmarc-visualizer directory in the directory you ran the git clone command from.

Change to the dmarc-visualizer directory:

`cd dmarc-visualizer`

Edit the **parsedmarc/parsedmarc.ini** file:

`vi parsedmarc/parsedmarc.ini`

Under the **[imap]** section, substitute **imap.domain.tld**, **imap_username** and **imap_password** fields with your IMAP hostname, username and password respectively:

```
[imap]
host = imap.domain.tld
user = imap_username
password = imap_password
watch = True
```

If you wish to use Maxmind Geoloation data, ensure you copy the GeoIP2 Country Database (**GeoLite2-Country.mmdb**) under the **parsedmarc/** directory (same path as the parsedmarc.ini file) and uncomment the following line in the **parsedmarc/Dockerfile** file:

`#COPY GeoLite2-Country.mmdb /usr/share/GeoIP/GeoLite2-Country.mmdb`

Start the Deeztek dmarc-visualizer stack:

`docker-compose up --build -d`

Navigate to the Grafana Dashboard where **IP_ADDRESS** is the IP Address of your docker host:

http://IP_ADDRESS:3000

Login with the default username of **admin** and the default password of **admin**. You will be prompted to change the password upon first succesful login.

## Pretty Screenshot

![Screenshot of Grafana dashboard](/big_screenshot.png?raw=true)
