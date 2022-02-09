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
//JDBC Connection string here: https://www.soapui.org/docs/jdbc/reference/jdbc-drivers/
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
**SOAP project / Groovy script - Reading project artefacts**

```groovy
log.info testRunner.testCase.name
log.info testRunner.testCase.testSuite.name
log.info testRunner.testCase.testSuite.project.name
log.info testRunner.testCase.testSuite.project.workspace.name

log.info testRunner.testCase.testSuite.project.getTestSuiteByName('TS02_Test Suite to test bank service').getTestCaseByName('TC01_To test getBank operation').name

def testSuiteMap = testRunner.testCase.testSuite.project.testSuites

//loop through the map and print the values

testSuiteMap.each{
	tsEntry ->
	log.info tsEntry.key
}
log.info 'Done'

```
**SOAP project / Groovy script - Standart assertions**

```groovy
String expectedName, actualName

expectedName = 'John'
actualName = 'John'

int a, b, c
a = 10
b = 10 

c = a + b

log.info 'before assertion'
assert expectedName == actualName, "names are not matching, expected name is $expectedName but actual name was $actualName"
log.info 'after assertion'

assert 20 == c

```
**SOAP project / Groovy script - Conditions**

```groovy
boolean isPassed
String grade

isPassed = true
//isPassed = false

//if I'm passed exam my dad will buy me a bike

if (isPassed == true){ //evaluates a boolean expression
	log.info 'Hurray!! I got a bike..'
}else{
	log.error 'Better luck next time'
}

//How to handle multiple scenarious?
//A - car
//B - bike
//C - nothing

grade = 'A'

if(grade == 'A'){
	log.info 'You got a Car!!'
}else if(grade == 'B'){
	log.warn 'You got a bike'
}else{
	log.error 'You got nothing' 
}

```
**SOAP project / Groovy script - Working with List**

```groovy
String fruit, country
fruit = 'Apple'
fruit = 'Banana'
def fruits = ['Aplle', 'Banana', 'Grapes', 'Mango', 'Poir']
log.info "Fruit name = $fruit"
log.info "Fruits = $fruits"

//Reading one by one entry in the list
fruits.each{
	fruitName ->
	log.info "Name is $fruitName"
}

//I want to find out whether my fruit list contains a fruit?
String fruitIamLookingFor = 'Papaya'
boolean hasFruitInsideIt = fruits.contains(fruitIamLookingFor)

if(hasFruitInsideIt == true){
	log.info "Found $fruitIamLookingFor in the fruit list"
}else{
	log.error "Cannot find fruit $fruitIamLookingFor in the fruit list"
}

//During run time, can I add a fruit to the existing list?
fruits.add('Papaya')
fruits << 'Pomegranate'

hasFruitInsideIt = fruits.contains(fruitIamLookingFor)

log.info '-------------------After------------------------'
if(hasFruitInsideIt == true){
	log.info "Found $fruitIamLookingFor in the fruit list"
}else{
	log.error "Cannot find fruit $fruitIamLookingFor in the fruit list"
}

//Remove papaya from the list
fruits.remove('Papaya')
hasFruitInsideIt = fruits.contains(fruitIamLookingFor)

log.info '-------------------After removing again------------------------'
if(hasFruitInsideIt == true){
	log.info "Found $fruitIamLookingFor in the fruit list"
}else{
	log.error "Cannot find fruit $fruitIamLookingFor in the fruit list"
}

```
**SOAP project / Groovy script - Working with Map**

```groovy
//How to define a map?
def countries = ['IND' : 'India', 
                 'USA' : 'United States of America', 
                 'SIN' : 'Singapore', 
                 'AUS' : 'Australia',
                 'RUS' : 'Russia']
//Find a country in the map?
String countryIamLookingFor = 'ABC'

boolean foundCountry = countries.containsKey(countryIamLookingFor)

log.info "Found country $countryIamLookingFor ? : $foundCountry"
//How to get the country name for the given country code?

String countryName = countries.get(countryIamLookingFor)

if(foundCountry==true){
	log.info "Country name is $countryName"
}else{
	log.error "Sorry con't find the country"
}

//Adding an entry to map
countries.put('GB', 'Great Britain')

log.info countries

```