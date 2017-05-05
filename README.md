# USTC CAS Redirect
A simple html page to help your application use USTC CAS(Central Authentication Service, https://passport.ustc.edu.cn/).

# Prerequisites
* A static html page under `*.ustc.edu.cn` (eg. `home.ustc.edu.cn`).
* An API from your application to receive and use the CAS ticket.

# Configurations
* Edit `index.html`
```javascript
// This page's url, the host must end with ".ustc.edu.cn"
var serviceURL = "https://home.ustc.edu.cn/~your_name/cas/index.html?id={0}";

// When this page get ticket, user will be redirected to apiUrl
var apiURL = "http://your_api_host/cas?id={0}&ticket={1}&service={2}";
```

* Upload `index.html` to your directory (Make sure `index.html` is at `serviceURL`)

# Usage
* Put the `serviceURL` in your application(with a specific `id`, which can help you controll the redirect when he come back from CAS server)
* When a user click the link, he will be first redirected to `CASURL` to login.
* If the user logins successfully, he will be redirected again to `serviceURL`, and automatically redirected to your `apiURL` with parameter `id`, `ticket` and `service`.
* With the `ticket` and `service`, your api server can get the login user from CAS server.(eg. get the content from `https://passport.ustc.edu.cn/serviceValidate?ticket=%s&service=%s`)

# Warning
* The parameter `id` isn't reliable. It's just for controlling the redirect more simply. Don't trust it.
* The common way to identify user is to use COOKIES or SESSIONS.

# About CAS
More info: http://www.ja-sig.org/products/cas