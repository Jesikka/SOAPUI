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