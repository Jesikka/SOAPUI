# SOAPUI


**Working with REST API using JSonSlurper**

```groovy
import groovy.json.JsonSlurper

//Create instance of JsonSlurper
def jsonSlurper = new JsonSlurper()
//Read the webservice response
def response = context.expand('${addPet#Response}')
//Parse the json response
def petData = jsonSlurper.parseText(response)

log.info "Pet data =" + petData
String status = petData.status
log.info "Status = $status"
assert status == 'available'

```
**SOAP project / Groovy script - SQL**

```groovy
import groovy.sql.*
//Read data from database table

String sqlStmt = 'SELECT * FROM BLZ_DATA'
def databaseUrl = 'jdbc:mysql://localhost:8080:/automation?user=root&password=root'
def username = 'root'
def password = 'root'
def driverName = 'com.mysql.jdbc.Driver'
def sql = Sql.newInstance(databaseUrl, username, password, driverName)

sql.eachRow(sqlStmt){
	row ->
	blz = row['blz_code']                                   //log.info row['blz_code']
	bic = row['bic_code']                                   //log.info row['bic_code']
	log.info "blz = $blz, bic = $bic"
}

```