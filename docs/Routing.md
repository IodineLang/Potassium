# Potassium Routing
Routing is a great way to make your web application semantic and flexible, as
[recommended by Tim Berners-Lee](http://www.w3.org/Provider/Style/URI.html) 
(despite being from 1998, the advice there still applies today).

Potassium's router integrates deeply with the Views system, which you can learn
about in Views.md. It will be assumed that you have a working knowledge of the 
view system before using the router.

## Using the Router
Firstly, you'll need to include a couple of Potassium libraries:

    use potassium.request;
    use potassium.views;
    use potassium.router;
    
    # Not strictly necessary, but advisable
    use potassium.response;
    
Then, in your `main` function, you need to create a `URLSpec` to pass to the 
router which will specify how requests should be routed. To make a `URLSpec`, 
you need to create a list of `URLItem`s, which act as a container to a View, 
its name and the request type that is required to activate it.

    # Let's assume homePage is a function-based view handler.
    homePageView = views.View(request.GetRequest(), homePage);
    urlList = list();
    urlList.add(router.URLItem("/", homePageView));

Now we have the `urlList`, we also need to specify a 404 view, in case the route 
isn't found. This is done when creating the `URLSpec`.

    urlSpec = router.URLSpec(urlList, "/");
    
If you haven't guessed already, the `"/"` parameter is the 404 route. For this 
simple example, we'll just send everything to the home page. If we'd set the 
404 route to a different page than the home page, POST requests to `/` would 
not be received by `homePageView`. This means that you can handle GET and POST 
requests completely differently, which is ideal for RESTful applications.
