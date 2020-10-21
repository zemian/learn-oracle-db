
## Oracle DB from hub.docker.com

https://hub.docker.com/search?q=oracle&type=image&certification_status=certified

https://hub.docker.com/u/zemiandeng/content/sub-be994fcc-219f-4ee1-9691-b2db11604915

Start server (it might take couple of mins)

	docker run -it -d --name myoracledb -p 1521:1521 store/oracle/database-enterprise:12.2.0.1
	docker container logs myoracledb

	# Or you can use random port then discover it
	docker run -it -d --name myoracledb -P store/oracle/database-enterprise:12.2.0.1
	docker port myoracledb

Connecting to the Database Server Container
(NOTE: You need to wait til the DB is ready first!)

	docker exec -it myoracledb bash -c "source /home/oracle/.bashrc; sqlplus /nolog"

	sql> verify DB here

	# Or using a sqlclient locally
	sqlplus sys/Oradoc_db1@ORCLCDB as sysdba


	# Or create tnsnames.ora in the directory pointed to by environment variable TNS_ADMIN

```
	ORCLCDB=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<ip-address of host>)(PORT=<mapped host port>))
	(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=ORCLCDB.localdomain)))
	ORCLPDB1=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<ip-address> of host)(PORT=<mapped host port>))
	(CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=ORCLPDB1.localdomain)))
```

Connect using JDBC:
	SID: ORCLCDB
	Host: localhost
	Port 1521
	Driver: Thin
	
	URL: jdbc:oracle:thin:@127.0.0.1:1521:ORCLCDB
	User: "sys as sysdba"
	Password: Oradoc_db1


## Oracle DB from Oracle Container Registry

NOTE: Ensure you have Oracle SSO credential:

	sudo -H docker login https://container-registry.oracle.com

	sudo -H docker run -it -d -p 1521:1521 container-registry.oracle.com/database/enterprise:latest


https://docs.oracle.com/en/operating-systems/oracle-linux/docker/docker-registry.html

https://docs.oracle.com/en/operating-systems/oracle-linux/docker/docker-ocr-login.html


https://github.com/oracle/docker-images

https://developer.oracle.com/cloud-native/

https://container-registry.oracle.com/pls/apex/f?p=113:10::::::

https://container-registry.oracle.com/pls/apex/f?p=113:4:16986425250095

https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=10&cad=rja&uact=8&ved=2ahUKEwjYpPHi4qnpAhXTgnIEHUTRAFQQwqsBMAl6BAgKEAk&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DXjM7lZ_TIAc&usg=AOvVaw2Lkof2fGS_WRQfqkuBP7wn



## Oracle Cloud Service + Docker

What is this? (it requires Cloud Account?)
https://oracle.github.io/learning-library/workshops/docker/?elqTrackId=05b8962236a74d4aa2a5603a18433e90&elqaid=74335&elqat=2&source=ad:pas:go:dg:paas1%2b:ow:lp:cpo::

https://www.oracle.com/technical-resources/articles/cloud/deploy-database-in-container-cloud.html


## How to Create Docker Image for Oracle DB

https://medium.com/oracledevs/creating-an-oracle-database-docker-image-f3cea1ea21bb

https://oracle-base.com/articles/linux/docker-oracle-database-on-docker

https://docs.oracle.com/en/operating-systems/oracle-linux/docker/docker-registry.html
