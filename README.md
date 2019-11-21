# Cross-Origin Resource Sharing (CORS)

CORS is a security mechanism that determines when certain requests made from a web browser are "allowed", based on the domain at which the web app is running, and the domain from which the extra resources are requested.

## The simpler times

When we first started making our front-end applications and hosting them on GitHub Pages, our app may have been accessed from a URL like this:

https://austinbruch.github.io/MyFirstApp/index.html

where our HTML file would load in some JavaScript and CSS, perhaps from URLs like these:

* https://austinbruch.github.io/MyFirstApp/assets/js/app.js
* https://austinbruch.github.io/MyFirstApp/assets/css/styles.css

Notice that we are loading our JS and CSS from the same Domain (origin) that our application is running from in the browser. In other words, our web page is running at `https://austinbruch.github.io`, and we are also loading our JS and CSS from `https://austinbruch.github.io`.

Because these hosts are exactly the same, web browsers treat this as a "safe" request because it's a fair assumption that an app running at a given domain should be allowed to access resources from the same domain. After all, you own your own domain, right?

If you were to make API calls using AJAX to an API that you wrote and hosted at the same domain as your web app (we are going to be doing this next week, so stay tuned!)

## Getting more complicated

The above is great for when we own every single aspect of our application. But what happens when we want to start interacting with other people's assets, like calling an API from iTunes, Spotify, or some other provider? Those APIs are not located at our domain, since we don't own them. They live at some other domain, like `api.spotify.com` for example.

> Note: for the sake of this presentation, I am making up API calls to reference. I am not referencing actual APIs that exist in reality.

You may want to make a request like `GET https://api.spotify.com/v1/songs?artist=blink-182`.

At this point, our app is still running at `https://austinbruch.github.io/MyFirstApp`. So now, we're making a network request from one domain to another. This is where CORS steps in.

CORS mainly exists for security reasons. It is very valuable to be able to control where your APIs or resources can be executed from a web browser.

A classic example is if some rogue JavaScript is running on your web page and it makes a request to a common Bank's API, hoping to get your account information if you're signed in to the bank's site in your current browser session. If the Bank does not allow your current domain to access it's resources, the request will not be exposed to the JavaScript.

CORS makes sure that the resource that you're requesting (the Spotify API, in this example) is allowed to be invoked from your web app at your domain.

## When does CORS get involved?

For us in this class, CORS will take effect when:
* Making API calls through things like AJAX (which uses `XmlHttpRequest` under the hood) or using `fetch` which is a more modern alternative.
* Loading `@font-face`s in CSS

There are other circumstances that will invoke CORS, but most are not likely to be encountered in the scope of this class.

CORS _will not_ take effect when loading assets like JavaScript or CSS, which is why we didn't see these issues when loading things like jQuery, bootstrap, etc.

## The HTTP Headers Involved

Below are the most commonly used HTTP Headers with respect to a CORS request/response interaction. There are others that are not covered here.

### Access-Control-Allow-Origin

* **Response header** (returned from the server in response to a request)
* Indicates which domain(s) can access this resource 
* Can be `*` for any or specific domain(s)

### Access-Control-Allow-Credentials

* **Response header** (returned from the server in response to a request)
* Only relevant if the server performs authentication via cookies
* In practice, this is _not_ super common.

### Access-Control-Allow-Headers

* **Response header** (returned from the server in response to a request)
* Dictates which HTTP Headers can be used in the cross-origin request

### Access-Control-Expose-Headers

* **Response header** (returned from the server in response to a request)
* Allows the server to control which response headers are made available to the calling JavaScript in the web browser.

### Access-Control-Allow-Methods

* **Response header** (returned from the server in response to a request)
* Dictates which HTTP methods can be used in the cross-origin request

### Origin

* **Request header** (sent from the browser when making a cross-origin request)
* The origin from which the request is made

### References:
* https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
* https://medium.com/@baphemot/understanding-cors-18ad6b478e2b
