API Testing Project for Simple-books
The scope of this project is to use all API knowledge gained throught the Software Testing course and apply them in practice, using a live application.

Application under test: Simple-Books

Tools used: Postman, Newman

Collection link: https://web.postman.co/workspace/43cf1499-e222-4974-8d4c-989572e44abd/documentation/32285997-5fd8347a-80b8-4044-968c-6894b5634a46


Tests performed
GET Status

HTTP method for request: GET

Request description: Check that the status code is correct

Response status code
:{
    "status": "OK"
}

Below you can find a picture of the API request from Postman:

<img width="638" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/0a505d4b-15be-4b42-a048-5fad2079448d">


JavaScript Tests:


    pm.test("Response status code is 200", function () {
        pm.expect(pm.response.code).to.equal(200);
    });


    pm.test("Response has the required fields", function () {
        const responseData = pm.response.json();
    
        pm.expect(responseData).to.be.an('object');
    …



Get book Id 1

HTTP method for request: GET

Request description: See all book with Id1

Response status code: 200 ok

Below you can find a picture of the API request from Postman:

<img width="626" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/8db7252d-5a30-4036-bbe5-d007228c2086">



JavaScript Tests:

    pm.test("Check that the first results in the list are correct ", function () {
  
    var data = pm.response.json();
 
    pm.expect(data[0].name).to.eql("The Russian");
  
    pm.expect(data[0].type).to.eql("fiction");
   
    pm.expect(data[0].available).to.be.true
    });

Get all book

HTTP method for request: GET

Request description: See all books

Response status code: 200 ok

Below you can find a picture of the API request from Postman:
<img width="1049" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/70104794-52d2-404d-8bfd-12f38a2bb77b">




JavaScript Tests:


    pm.test("Response status code is 200", function () {
    pm.response.to.have.status(200);
    });

    pm.test("Response has valid Content-Type header of application/json", function () {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
    });

    pm.test("Name is a non-empty string", function () {
      const responseData = pm.response.json();
  
      pm.expect(responseData).to.be.an('array');
      responseData.forEach(function(book) {
        pm.expect(book.name).to.be.a('string').and.to.have.lengthOf.at.least(1, "Name should not be empty");
      });
    });
    
    pm.test("Type is a non-empty string", function () {
        const responseData = pm.response.json();
    
        pm.expect(responseData).to.be.an('array');
        responseData.forEach(function(book) {
            pm.expect(book.type).to.be.a('string');
            pm.expect(book.type).to.have.lengthOf.at.least(1, "Type should not be empty");
        });
    });


Create order without authentication

HTTP method for request: POST

Request description: Create order without authentication

Response status code: 401

Below you can find a picture of the API request from Postman:

<img width="632" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/943dbd57-06a8-4154-9398-68c26c59fcee">



JavaScript Tests:


    pm.test("Response status code is 401", function () {
        pm.expect(pm.response.code).to.equal(401);
    });


    pm.test("Response has the required 'error' field", function () {
      const responseData = pm.response.json();
      pm.expect(responseData).to.be.an('object');
      pm.expect(responseData.error).to.exist;
    });


    pm.test("Error field is a non-empty string", function () {
      const responseData = pm.response.json();

      pm.expect(responseData).to.be.an('object');
      pm.expect(responseData.error).to.be.a('string').and.to.have.lengthOf.at.least(1, "Error field should not be empty");
    });


    pm.test("Content type is application/json", function () {
      pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
    });


    pm.test("Verify response does not contain sensitive information", function () {
        const responseData = pm.response.json();
    
        pm.expect(responseData).to.be.an('object');
        pm.expect(responseData.error).to.exist.and.to.be.a('string');
    });




.............

**Nume Request n**
HTTP method for request: Inserati aici metoda HTTP a requestului
Request description: Inserati o scurta descriere a requestului, conform documentatiei de API
Test types / techniques used: Inserati tipurile si tehnicile de testare folosite pentru acest request
Response status code: Inserati aici status code-ul pe care l-ati obtinut in urma executiei requestului

Below you can find a picture of the API request from Postman:

Inserati aici o poza cu requestul din postman in care sa se observe request method, endpoint, request body si response body

JavaScript Tests:

Inserati aici o poza cu testele in java script pe care le-ati definit impreuna cu rezultatele executiei acestora

Execution report for the created API collection
Below you can find the execution report that was generated through the Postman collection runner.

Inserati aici o poza cu raportul de executie din Postman

The collection was also run through newman directly from the terminal, and the results can be found below:

Inserati aici o poza cu raportul de executie din Newman

Defects found
The following issues were identified while running the postman tests:

**Inserati aici fie un fisier pdf care sa contina raportarea tuturor bug-urilor, fie le descrieti direct in git Bug-urile trebuie sa contina titlu, preconditii, pasi de executie, rezultate asteptate si rezultate actuale. Optional, bug-urile pot fi raportate in jira, si apoi puteti pune poze direct din jira
