[Simple.books.API.postman_collection.json](https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/files/14345012/Simple.books.API.postman_collection.json)[Simple books API.postman_collection.json](https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/files/14344994/Simple.books.API.postman_collection.json)API Testing Project for Simple-books
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

Token generation

HTTP method for request: POST

Request description: Generate new token

Response status code" 201 Created

Below you can find a picture of the API request from Postman:
<img width="628" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/97ba0877-c4c3-4a31-86e6-c5add9c806aa">




JavaScript Tests:


    pm.test("Response status code is 201", function () {
        pm.expect(pm.response.code).to.equal(201);
    });


    pm.test("Response has the required field - accessToken", function () {
      const responseData = pm.response.json();
  
      pm.expect(responseData).to.be.an('object');
      pm.expect(responseData.accessToken).to.exist.and.to.be.a('string');
    });


    pm.test("Access token should not be empty", function () {
      const responseData = pm.response.json();
      pm.expect(responseData.accessToken).to.exist.and.to.not.be.empty;
    });


    pm.test("Content-Type is application/json", function () {
        pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
    });


    pm.test("Response time is less than 500ms", function () {
      pm.expect(pm.response.responseTime).to.be.below(500);
    });

Submit orders

HTTP method for request: POST

Request description: Submit orders

Response status code 201 Created

Below you can find a picture of the API request from Postman:

<img width="631" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/e54a1d9a-a232-42f0-8352-a14323adc6ee">



JavaScript Tests:


    pm.test("Response status code is 201", function () {
        pm.expect(pm.response.code).to.equal(201);
    });


    pm.test("Response has the required fields - created and orderId", function () {
        const responseData = pm.response.json();
        
        pm.expect(responseData).to.be.an('object');
        pm.expect(responseData).to.have.property('created');
        pm.expect(responseData).to.have.property('orderId');
    });


    pm.test("OrderId is a non-empty string", function () {
      const responseData = pm.response.json();
  
      pm.expect(responseData.orderId).to.be.a('string').and.to.have.lengthOf.at.least(1, "OrderId should not be empty");
    });


    pm.test("Content-Type header is application/json", function () {
        pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
    });


    pm.test("Created field is set to true", function () {
        const responseData = pm.response.json();
    
        pm.expect(responseData).to.be.an('object');
        pm.expect(responseData.created).to.equal(true);
    });



    

Get Orders

HTTP method for request: GET

Request description: Get Orders with Id:b8nIMcctaxBsr9B17x2r-.22

Response status code: 404 Not found

Below you can find a picture of the API request from Postman:
<img width="636" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/9dac7292-cb7f-4d6a-b2d6-80417c202dfd">



JavaScript Tests:

    pm.test("Response returns error", function () {
       pm.expect(pm.response.text()).to.include("error");
    });

    var responseData = pm.response.json()
    pm.test("Response returns correct error message", function ()
    {pm.expect(responseData.error).to.eql("No order with id b8nIMcctaxBsr9B17x2r-.22.");});

    pm.test("Check that the status code of the request is the correct one",() =>{
       pm.response.to.have.status(404)})



Update order

HTTP method for request: Patch

Request description: Update order with customer name 111

Response status code 404 Not found

Below you can find a picture of the API request from Postman:
<img width="632" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/08f04bbc-6bf4-4219-b240-99ddc5529d89">



JavaScript Tests:

    pm.test("Response status code is 404", function () {
      pm.expect(pm.response.code).to.equal(404);
    });


    pm.test("Response has the required field 'error'", function () {
        const responseData = pm.response.json();
    
        pm.expect(responseData).to.be.an('object');
    …        const orderId = pm.request.url.getPath().match(/orders\/([A-Za-z0-9-]+)/)[1];
        pm.expect(orderId).to.match(/[A-Za-z0-9-]+/);
    });



Delete order

HTTP method for request: DEL

Request description: Delete Order with inexistent ID

Response status code 404  Not found

Below you can find a picture of the API request from Postman:
<img width="631" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/f735c7b7-4903-426b-94d5-513b739ffd80">



JavaScript Tests:


pm.test("Response status code is 404", function () {
  pm.expect(pm.response.code).to.equal(404);
});


pm.test("Response has content type application/json", function () {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
});
…    
    pm.expect(responseData).to.be.an('object');
    pm.expect(responseData.error).to.exist;
});




Update status negativ testing

HTTP method for request: Patch

Request description: update status  negative testing

Response status code

Below you can find a picture of the API request from Postman:

<img width="846" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/35fb0ca9-d47b-4c51-914b-735bb5f3b833">




Get bookId with inexistent Id

HTTP method for request: GET

Request description: Get book with id 16

Response status code 404 Not found

Below you can find a picture of the API request from Postman:
<img width="623" alt="image" src="https://github.com/DianaBencea/API_Testing_Project_For_Simplebooks/assets/151565785/87dec815-32af-4e39-80aa-25f3b9005263">





Execution report for the created API collection
Below you can find the execution report that was generated through the Postman collection runner.

Inserati aici o poza cu raportul de executie din Postman
[Uploading Simple.{
	"info": {
		"_postman_id": "5fd8347a-80b8-4044-968c-6894b5634a46",
		"name": "Simple books API",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
		"_exporter_id": "32285997"
	},
	"item": [
		{
			"name": "Status",
			"request": {
				"method": "GET",
				"header": [],
				"url": {
					"raw": "https://simple-books-api.glitch.me/status",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"status"
					]
				}
			},
			"response": []
		},
		{
			"name": "Get all books",
			"request": {
				"method": "GET",
				"header": [],
				"url": {
					"raw": "https://simple-books-api.glitch.me/books",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"books"
					]
				}
			},
			"response": []
		},
		{
			"name": "Get bookId 1",
			"request": {
				"method": "GET",
				"header": [],
				"url": {
					"raw": "https://simple-books-api.glitch.me/books/1",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"books",
						"1"
					]
				}
			},
			"response": []
		},
		{
			"name": "Create order without authentication",
			"request": {
				"method": "POST",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n  \"bookId\": 1,\r\n  \"customerName\": \"John\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/orders",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"orders"
					]
				}
			},
			"response": []
		},
		{
			"name": "Token generation",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{Token for books}}",
							"type": "string"
						}
					]
				},
				"method": "POST",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n   \"clientName\": \"DidiElena\",\r\n   \"clientEmail\": \"ely@tmta.com\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/api-clients/",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"api-clients",
						""
					]
				}
			},
			"response": []
		},
		{
			"name": "Submit orders",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "112cf432216b5d5b36cd041938b5375923908265ed5baa7f0ea32a94bc806c0c",
							"type": "string"
						}
					]
				},
				"method": "POST",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n  \"bookId\": 1,\r\n  \"customerName\": \"John\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/orders",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"orders"
					]
				}
			},
			"response": []
		},
		{
			"name": "Get orders",
			"protocolProfileBehavior": {
				"disableBodyPruning": true
			},
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "112cf432216b5d5b36cd041938b5375923908265ed5baa7f0ea32a94bc806c0c",
							"type": "string"
						}
					]
				},
				"method": "GET",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n  \"bookId\": 1,\r\n  \"customerName\": \"John\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/orders",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"orders"
					]
				}
			},
			"response": []
		},
		{
			"name": "Update order",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "112cf432216b5d5b36cd041938b5375923908265ed5baa7f0ea32a94bc806c0c",
							"type": "string"
						}
					]
				},
				"method": "PATCH",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n\r\n  \"customerName\": \"Maria\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/orders/Lyl2clCpqTQ99t2ocXXP-",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"orders",
						"Lyl2clCpqTQ99t2ocXXP-"
					]
				}
			},
			"response": []
		},
		{
			"name": "Delete order",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "112cf432216b5d5b36cd041938b5375923908265ed5baa7f0ea32a94bc806c0c",
							"type": "string"
						}
					]
				},
				"method": "DELETE",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/orders/Lyl2clCpqTQ99t2ocXXP-",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"orders",
						"Lyl2clCpqTQ99t2ocXXP-"
					]
				}
			},
			"response": []
		},
		{
			"name": "Update status negative testing",
			"request": {
				"method": "PATCH",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\r\n  \"avaliable\": \"truen\"\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "https://simple-books-api.glitch.me/books/2",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"books",
						"2"
					]
				}
			},
			"response": []
		},
		{
			"name": "Get bookId with inexistent id",
			"request": {
				"method": "GET",
				"header": [],
				"url": {
					"raw": "https://simple-books-api.glitch.me/books/10",
					"protocol": "https",
					"host": [
						"simple-books-api",
						"glitch",
						"me"
					],
					"path": [
						"books",
						"10"
					]
				}
			},
			"response": []
		}
	],
	"variable": [
		{
			"key": "Token for books",
			"value": "8c5e92220abbb3a63485e33d0850e3a69811210a2e14d24bc5797227ff5a550a"
		}
	]
}books.API.postman_collection.json…]()


The collection was also run through newman directly from the terminal, and the results can be found below:

Inserati aici o poza cu raportul de executie din Newman

Defects found
The following issues were identified while running the postman tests:

**Inserati aici fie un fisier pdf care sa contina raportarea tuturor bug-urilor, fie le descrieti direct in git Bug-urile trebuie sa contina titlu, preconditii, pasi de executie, rezultate asteptate si rezultate actuale. Optional, bug-urile pot fi raportate in jira, si apoi puteti pune poze direct din jira
