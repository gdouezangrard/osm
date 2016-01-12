Run the proxy:
  - npm install corsproxy && ./node_modules/.bin/corsproxy
Run a local web server:
  - python -m http.server
Browser for index.html on localhost

Hackish note: In CORS spec, 3xx response to a POST is considered as a network
error, so you can't retrieve the response even with CORS disabled at browser
level (at least in major browsers). So we trick the browser to think it speaks
with the host the code was loaded from with a local CORS proxy + local file
server. corsproxy is not enough though, web browsers perform a GET request
after a 3xx response to a POST request, and we can't retrieve the POST
response. As we want the content of the header Location, an hack is to compare
the response url with the request url. The GET response url in case of
redirection is 'http://corsproxy-url/ + location_content' so we can retrieve
the Location header !
