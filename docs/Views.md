# Potassium Views
(written for Potassium **v0.1.0**)

Views can be used to take away boilerplate and allow you to focus on writing 
the code you want. Currently, views require only two things: a request type 
(such as `request.GetRequest()` for GET requests), and a function view. 
Function views are any functions that take a `requestData` object, and return a
Response object (or, technically, any object that has a `getResponse()` 
function).

## Usage
### Basic Usage
You need to reference the following libraries:

    use potassium.views;
    use potassium.response;
    
Then, you can can create function views like this:

    func homePage (requestData) {
        return HTMLResponse("<h1>Home Page</h1>", 200);
    }
    
    # You need to: use json; if you plan to use JSONResponses.
    func jsonPage (requestData) {
        responseData = hashMap();
        responseData["message"] = "Hello!";
        return JSONResponse(json.dump(responseData), 200);
    }
    
After this, you need to actually create the views:

    homePageView = views.View(request.GetRequest(), homePage);
    jsonPageView = views.View(request.GetRequest(), jsonPage);
    
If you like, you can manually run a view like this:

    homePageView.run();
    
However, the `View` really shines when used in conjunction with the `Router`
(see Routing.md).

### GET Parameters
You can access a request's GET parameters easily in the function view like so:

    func jsonPage (requestData) {
        responseData = hashMap();
        responseData["page"] = requestData.parameters.getParam("page");
        return JSONResponse(json.dump(responseData), 200);   
    }
    
### POST Parameters
You can also access POST data. Both `application/x-www-form-urlencoded` (the 
default HTML form encoding type) and `application/json` formats are supported. 
`multipart/form-data` is not currently supported, though support is planned in 
future.

    func jsonPage (requestData) {
        responseData = hashMap();
        responseData["username"] = requestData.postData.getParam("username");
        return JSONResponse(json.dump(responseData, 200));
    }
    

