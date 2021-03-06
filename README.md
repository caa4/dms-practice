# dms-practice
Diabetes Management Solution practice project

## DMS Installation Prerequisites
- [Installing Docker](https://docs.docker.com/get-docker/)

## Running Docker Authorization server on local machine
Execute docker command `docker run -p 8083:8083 mgharib/keycloack-auth-server` to run Authorization server on port 8083. Once it is up, you should be able to access it via [http://localhost:8083/auth/](http://localhost:8083/auth/)

## configuring OpenEMR with HAPI FHIR on local machine
-	Clone current repo 
-	Navigate with CMD into openemr-compose
-	Execute docker-compose -f openemr-compose.yml up -d
-	When all containers are started, you can access to:
	-	The FHIR server [http://localhost:8080/home](http://localhost:8080/home)
	-	The OpenEMR server: [http://localhost:80/](http://localhost:80/) 
	-	Login into OpenEMR
		-	Username: admin
		-	Password: pass
-	Follow steps in below article to configure OpenEMR to be able to export to the FHIR server 
	-	[https://medium.com/@ben.che/openemr-fhir-how-to-setup-your-instance-dd646b0daec3](https://medium.com/@ben.che/openemr-fhir-how-to-setup-your-instance-dd646b0daec3)
			

## Running Spring Authorization server on local machine
-	Clone current repo
-	Open with prefered Java IDE
-	use the following commands inside the terminal
	-	mvn clean
	-	mvn install
	-	mvn spring-boot:run
-	Once running, visit http://localhost:8083/auth/
	-	login: emr-admin
	-	password: pass

## Running HDI-HUB server on local machine and testing with PMS
-	Clone current repo
-	Running HDI-HUB lcoally (port 8080)
	-	mvn clean
	-	mvn install
	-	mvn jetty:run
-	Running HDI-HUB on Docker (assign port)
	-	Inside project ide terminal execute mvn package to generate war file
	-	Inside HDI-HUB directory using Powershell/Terminal
		-	Install Docker Jetty using docker run -d jetty
		-	Execute docker build -t fhir/hapiserver .
		-	Execute docker run -p 8090:8080 fhir/hapiserver
			-	runs fhir server on port 8090
-Running PMS to test HDI-HUB
-	Run Spring Authorization Server (docker works fine)
-	use the following commands inside the ide terminal
	-	mvn clean
	-	mvn install
	-	mvn spring-boot:run
-	Once running, PMS will post patient and organization information to HDI-HUB server every 5 seconds
-	Enter CTRL+C to terminate once enoough patient information is populated

## Running DMS UI on local machine and starting development
- Make sure you have the latest image of authorization server `docker image pull mgharib/keycloack-auth-server`
- Run the authorization server `docker run -p 8083:8083 mgharib/keycloack-auth-server`
- Navigate with CMD into dms-ui
- Install dependencies `npm install`
- Run the server `npm run start`
- You should be able to access the ui through [http://localhost:4200](http://localhost:4200)
- You can login using john@test.com/123

## OpenEMR- Local Development using Docker.
- Installation of docker and pull mariadb and mysql.
- Pull the latest image of openemr using `docker pull openemr/openemr`.
- From command line Run `docker-compose up`
- Access http://localhost:8300/ to login as `admin`. Password is `pass`. 
- More details at https://hub.docker.com/r/openemr/openemr/.
