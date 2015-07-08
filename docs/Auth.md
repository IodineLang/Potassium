# Potassium Authentication
(written for Potassium **v0.1.0**)

Almost all meaningful web applications depend on user authentication, so 
Potassium comes with an authentication system out of the box. All you need to 
do is hook up the code with your function views (this is useful, because it 
allows you to present your application in any way that you want, such as a 
RESTful API, or, alternatively, as a static HTML page).

Potassium's authentication system uses *token-based* authentication, so you 
need to handle user storage of the token client-side. You are also currently 
responsible for verifying authentication with the `verifyToken(token)` command; 
there is no automatic check yet.

## Usage
The best way to see the usage of the `Auth` class is to go to 
`src/cgi-bin/authtest.id`, where you can see all of the functions in use. The 
general principles are similar for most operations though:

    authHelper = auth.Auth(mySqlDatabaseConnection);
    # Do something with authHelper
    
You **can** use the database connection at any point while the `authHelper` is 
using it. This is designed to speed up response times by using only one 
database connection (since database connection is **very** slow in the `mysql` 
module currently).

## Example of Verification Check

    func tokenVerifiedPage(requestData) {
        authHelper = auth.Auth(mysql.openDatabase(CONNECTION_STRING));
        user = authHelper.verifyToken(requestData.postData.getParam("token"));
        if (user != null) {
            return HTMLResponse("<h1>Hey, " + user + "</h1>", 200);
        }
        else {
            return HTMLResponse("<h1>Who are you?</h1>", 400);
        }
    }
