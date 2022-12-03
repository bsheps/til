---
title: "On Wrapping Third Party Libraries"
date: 2022-12-02T09:20:48-06:00
draft: false
---

I recently came across a few scenarios where wrapping third party libraries would have likely saved considerable time and prevented a production bug. 

One scenario involved adding a Cross Site Request Forgery (CSRF) token to all HTTP requests made to all API endpoints (excluding GET requests since they are read only requests) to prevent replay attacks. 

*Background: CSRF tokens in a nutshell, prevent replay attacks where a malicious actor attempts to "replay" a valid HTTP request made by a user with malicious data. The typical goal of the attack is to overwrite the already submitted, valid, user data with malicious user data / executable exploit code. [OWASP explanation](https://owasp.org/www-community/attacks/csrf) | [Example of an attack](https://guides.codepath.com/websecurity/Cross-Site-Request-Forgery)*


For the API endpoints, all incoming requests are passed to an authorization service for verification. The implementation code was simple: if the request is anything besides GET, then verify the CRSF Token is valid. If the token check fails, respond to the request with an unauthorized message. The best part, we only need to update code in a single place and the change is only a few lines of code.

```js
// Authorization service
if(request.method != GET)
    user.verifyCsrfToken(csrf_token); // throws an unauthorized error if invalid
```

From a client perspective, we're working with multiple react applications using differing HTTP request approaches, scattered throughout the code. Some requests are made through the browser based fetch api, others through a polyfill library, etc. This change will be somewhat messy and tedious because we need to find and update all the places in the code where state changing HTTP requests are made. Couple hours later, done.

```js
// http request
request_header : {
 'method': 'POST',
 'csrf_token': csrf_token // <-- simple 1 line change, but needed in a lot of places
}
```


Fast forward a few days - calls are coming from users getting unauthorized errors when attempting to view/decrypt a sensitive field in the form (think something like on your bank website's reveal/show account number button). Turns out the CSRF token was never added to a HTTP POST request call triggered by the "reveal" button in a one-off, single use, react component. How did this POST call get missed? The method definition used a **lowercase** "post" instead of **uppercase** "POST" so the request flew under the radar and was missed.

`{ 'method': 'post' }` vs `{ 'method': 'POST' }`

A blocked user and couple of hours later, the code adding the CSRF token to the reveal component is progressing through the lower environments onto production. 

In retrospect, it's easy to chalk this up to blame the maintenance programmer but it's not realistic to test every endpoint (multiple large applications) and human mistakes happen, things can blur together, etc. On the other hand, we can leverage engineering to use a known solution: all client applications use a single wrapped HTTP request method (similar to how the API endpoints do for authorization). This solution makes sense here because we're making same the 3rd party API call throughout the code. In summary, wrapping 3rd party libraries can be a powerful tool when used in the right scenarios, and can help prevent bugs and reduce maintenance costs.
