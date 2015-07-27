# Potassium Views
(written for Potassium **v0.2.0**)

Views can be used to take away boilerplate and allow you to focus on writing 
the code you want. Currently, views require only two things: a request type 
(such as `request.GetRequest()` for GET requests), and a function or class view. 
Function views are any functions that take a `requestData` (sometimes called 
`req`) object, and return a Response object (or, technically, any object that
has a `getResponse()` function). Class views are essentially function views 
named `get` and `post`.

## Usage
### Basic Usage
You need to reference the following libraries:
```go
use potassium.views;
use potassium.response;
```   
There are two ways to create views from here; class-based views or function-
based views.
#### Function-based Views
```go
@views.functionView ("GET")
func indexView (req) {
    return response.HTMLResponse ("<h1>Hello</h1>", 200);
}
```

If you're not an expert at Iodine, you may not know what the `@` symbol does.
This uses `functionView` as a *decorator*, which allows Potassium to wrap the
function with some extra code. 

> #### Irrelevant implementation detail
> 
> Internally Potassium wraps function-based views into class-based views. How 
> crafty is that?

#### Class-based views
```go
class IndexView : views.View {
    func IndexView (self) {
        super ();
    }
    
    func get (self, req) {
        return response.HTMLResponse ("<h1>Hey!</h1>", 200);
    }
}
```

Though class-based views are a little bit "*heavier*", they become much nicer
when both GET and POST are used in the same view. It's important to note that
the `super ()` call is **required**, otherwise the view won't inherit from the 
base view class in Potassium.

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
    

