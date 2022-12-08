

# Project Title

This folder offers examples of how to use api methods like get, post, put, and delete to check values, giving you a basic grasp of how they work. Additionally, you may find check and report API codes here.[In API document you can find source codes and all the url to check or practice any task]

# Project requirements
### Java
https://www.oracle.com/java/technologies/downloads/
### Postman
https://www.postman.com/
### Node JS
https://nodejs.org/en/

## API Source Urls:

### Base_Url: https://restful-booker.herokuapp.com
### method:Get -Url: Base_Url/booking/id
### Method:Post -Url: Base_Url/booking/
### Method:Put -url: Base_Url/booking/id
### Method:Delete -url: Base_Url/booking/id


## Methods body code:

### Post: https://restful-booker.herokuapp.com/booking/

Body code:
 https://restful-booker.herokuapp.com/booking \
 ```ruby

  -H 'Content-Type: application/json' \
  -d '{
	"firstname" : "Jim",
	"lastname" : "Brown",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}
```

![pic1](https://user-images.githubusercontent.com/45315685/206577953-831de1d8-fe09-4454-b4c5-c49daa6b77ee.PNG)


### Post: Base_Url/auth
Body code:
```ruby

{
	"username": "admin",
	"password": "password123"
}
```

response code:
```ruby

{
    "token": "f66dcf8247182b9"
}
```
![pic2](https://user-images.githubusercontent.com/45315685/206578016-3d334a55-77f2-4ea8-a677-ccb6c60ff51e.PNG)


### Put: Base_Url/booking/id

set Header:
  -H 'Cookie: token=f66dcf8247182b9

![pic3](https://user-images.githubusercontent.com/45315685/206578133-08d63c46-84fc-45e6-9500-1d924496fd42.png)


Body code:
```ruby
  -d '{
	"firstname" : "James",
	"lastname" : "Brown",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}
```

![pic4](https://user-images.githubusercontent.com/45315685/206578159-d1c39363-4620-4ae7-8544-b00301b3a48b.PNG)


## Assertion details

### method Put : Base_Url/booking/bookingid

### to generate date 
#### Pre-request Script:
```ruby
const moment =require ('moment');
const today = moment();
pm.environment.set("checkin",today.add(0, 'day').format("YYYY-MM-DD"));
pm.environment.set("checkout",today.add(15,'day').format("YYYY-MM-DD"));
```

![date pic5](https://user-images.githubusercontent.com/45315685/206578219-8d6a8409-a39f-49bd-a35c-feacc9b6b63b.PN

#### Body:
```ruby
{
	"firstname" : "Sakif",
	"lastname" : "Abdullah",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "Breakfast"
}
```
![pic6](https://user-images.githubusercontent.com/45315685/206578318-cdc03f9a-6f3f-4444-baf0-d38e73b263c8.PNG)


### to generate random name 
#### Pre-request Script:
```ruby
var fname= pm.variables.replaceIn("{{$randomUserName}}");
pm.environment.set("fname",fname);
var lname = pm.variables.replaceIn("{{$randomUserName}}");
pm.environment.set("lname",lname);
```

![pic7](https://user-images.githubusercontent.com/45315685/206578369-52cb563e-56af-4140-9a77-2655e82e3241.PNG)
#### Body:
```ruby
{
	"firstname" : "{{fname}}",
	"lastname" : "{{lname}}",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "Breakfast"
}
```

![pic8](https://user-images.githubusercontent.com/45315685/206578451-0b130f9e-9288-4889-9fdd-ac5e5966b711.PNG)


## Environment setup variables:

![pic9](https://user-images.githubusercontent.com/45315685/206578611-b4d17fbf-8026-43fd-988b-bf018f0b2faa.PNG)

## test Stats code 

### test to check match with name , date and status code 

```ruby
var jsonData = pm.response.json();
var code = responseCode.code;

console.log(jsonData);
switch(code){
    case 200:
    pm.test("matched with 200", function(){
    })
    pm.test("first name check", function(){
        pm.expect(jsonData.firstname).to.eql(pm.environment.get("fname"));
    })
    pm.test("checkin matched",function(){
        pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkin"));
    })
    break;
    case 201:
    pm.test("matched with 201", function(){
    })
    break;
    default:
    pm.test("stats code unmatched", function(){

    })

}
```

![pic10](https://user-images.githubusercontent.com/45315685/206578702-01ddf885-6eca-49c4-a37e-fb60096f3a3e.PNG)
![pic11](https://user-images.githubusercontent.com/45315685/206578725-63752e27-3098-4c17-89c5-e9471c0b108f.PNG)

## Report Generate:

Comand prompt: 
Run Command: 

generat file without environment 
newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
Because of not setting environment we can see lots of error
![pic12](https://user-images.githubusercontent.com/45315685/206578759-1510ccf3-caf5-4950-9692-a7b7374764ba.PNG)

Now we gennerate file with environment file also
newman run “Collection Link” -e “Path”/EnvironmentName.json
![pic13](https://user-images.githubusercontent.com/45315685/206578813-7ab3a386-128e-4402-ac10-eda2240b4945.PNG)

### html report Generate
### only html:
newman run “Collection Link” -e EnvironmentName.json -r cli,html
![pic15](https://user-images.githubusercontent.com/45315685/206579052-2215394a-1530-4556-9fad-ff50ff118d6d.PNG)
![pic16](https://user-images.githubusercontent.com/45315685/206579212-320dc842-b2d7-44be-a3a3-131bd3fc8b2e.PNG)
![pic17](https://user-images.githubusercontent.com/45315685/206579258-ed879f24-ddb7-4f1d-96bf-468b131e7c87.PNG)

### html with extra:
newman run “Collection Link” -e EnvironmentName.json -r cli,htmlextra
![pic14](https://user-images.githubusercontent.com/45315685/206578976-53963987-87ef-49d9-bf8f-e10e7206e43c.PNG)

