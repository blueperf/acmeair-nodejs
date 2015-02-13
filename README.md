# Acme Air in NodeJS 

## Content

### Runtime Environment

* [NodeJs](http://nodejs.org/download/)


### Datastore Choices

Environment variable dbtype is used to determine the datastore choice. See under "More on datastore configuration".

datastore | dbtype value | Meaning
--- | --- | --- 
[MongoDB](https://www.mongodb.org/downloads) | mongo | The default choice
[Cloudant](https://cloudant.com) | cloudant | 


### Application Mode

Environment variable AUTH_Service is use to determine when Micro-Service is used.

application mode | AUTH_Service value | Meaning
--- | --- | --- 
Monolithic | | One NodeJS application connects to backend datastore. The default mode.
Micro-Service | host:port | Main NodeJS application delegates to authorization service NodeJS application hosted on host:port


### Application Run Platforms

* [Bluemix] (README_Bluemix.md)
* [Docker] (README_Docker.md)
* [Bluemix Container Service] (README_Bluemix_Container.md)


## How to get started

### Resolve module dependencies

	npm install


### Run Acmeair in Monolithic on Local

	node app.js
		
		
### Run Acmeair in Micro-Service on Local

	node authservice-app.js
	set AUTH_SERVICE=localhost:9443 or export AUTH_SERVICE=localhost:9443
	node app.js
	
	
### Access Application 

	http://localhost:9080/
	Load Database 
		preload 10k customers uid[0..9999]@email.com:password, 5 days' flights.  Defined in loader/loader-settings.json
	Login
	Flights
		such as Singapore to HongKong or Paris to Moscow 
	Checkin
		cancel some booked flights
	Account
		update account info
	Logout	
	
	
	
## More on datastore configuration

### How dbtype is determined

* Set environment variable dbtype to mongo or cloudant to determine which dbtype to use. The default mongo. 
* When running on Bluemix, dbtype is automactially discovered from the service the application is bound to.

### The datastore configuration

* All default datastore configuration is defined in settings.json.
* When running on Bluemix, datasource url will be read from bound service information.
* For CLoudant, you need to follow document/DDL/cloudant.ddl to create database and define search index.

### How to extend with more datasource types

* Create a folder under dataaccess with the new dbtype name. Look at current implementation for reference.

