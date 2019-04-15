# How does our authentication flow work?

## Elija / Backend

In Elija we use JWT-token based authentication with [flask-jwt-extended](https://flask-jwt-extended.readthedocs.io/en/latest/).
A JWT-token can encode arbitrary information. For our authentication flow the following fields are important:
- 'exp': Contains the time when a JWT-token expires.
- 'identity': Contains the user_id ('identity'-key can be changed in config)
- 'csrf': Contains the csrf-token
- 'type': The type of the JWT-token (At the moment we have 'access' and 'reset_password').

For more Information you can look at: https://blog.angular-university.io/angular-jwt/

### Login with password

The login route for elija is `POST /authentications`. It accepts the following parameters:
- 'id_token': A JWT-token issued by Google, that contains user information.
- 'email_or_username'
- 'password'
- 'set_cookies': Boolean. Decides wether the access token is returned in cookies or the body.

If 'email_or_username' and 'password' are specified, it will find the user by email or usernamen and compare the password
with the saved password hash. It than returns an access-token and a csrf-token in the cookies or in the body.

**Access tokens in Cookies vs. in the Header:**

There is a good article about the problem: http://www.redotheweb.com/2015/11/09/api-security.html.
Basically if we send the access-token in a http-only cookie, it cannot be accessed in the frontend javascript.
Therefore, if someone performs a successfull Cross-site scripting (XSS) attack, they cannot steal the access-token.

On the other hand we would be vulnerable to Cross-site request forgery (CSRF) attacks, because cookies are always send,
even if we are on a malicous webside. To solve that problem we also send a CSRF token that needs to be set in the 
header 'X-CSRF-TOKEN' for every authenticated request. The csrf-token is checked against the 'csrf' value in the access token.
This prevents CSRF-Attacks, because the malicous website does not know the csrf-token. Our frontend saves the token in local storage.
If someone make a successful XSS attack they only have the csrf-token, which is useless without the access-token.

### Login with Google

To login with Google we send the id_token to `POST /authentications`.
You can see the documentation on how to obtain a google id token here: https://developers.google.com/identity/sign-in/web/backend-auth
We decode the id_token and obtain the google_id in Elija. If a user exists in our database with that google_id, you are logged in
with that user, otherwise a new user will be created with the google email.

## Jona / Frotend

In Jona we obtain the csrf-token on login and store it in local storage. For every request an axios middleware checks,
if the csrf-token is set and adds it to the request header.

## Tobito / Dialogflow-Adapter

To authenticate with Google Assistant the user is asked if he wants to send his credentials to our app. If yes, Tobito receives an
id_token and sends it to Elija. This is almost the same as login with google, except that we send "set_cookies" set to false.
We receive the access token and store it in the user storage in dialogflow (https://developers.google.com/actions/assistant/save-data).
For every subsequent request the "Authorization" header is set with the access-token.





