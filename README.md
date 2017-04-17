nginx-opentracing
-----------------

Enable requests served by nginx for distributed tracing via [The OpenTracing Project](opentracing.io).

Dependencies
------------
- nginx-opentracing currently only works with [LightStep's C++ tracer](https://github.com/lightstep/lightstep-tracer-cpp).  Also, see [here](http://lightstep.com/#request-access) to request access.
- Source for [Nginx 1.0.x](http://nginx.org/).

Building
--------
```
$ tar zxvf nginx-1.0.x.tar.gz
$ cd nginx-1.0.x
$ ./configure --add-module=/absolute/path/to/nginx-opentracing
$ make && sudo make install
```


Getting Started
---------------
```
http {
  # Provide your lightstep access token.
  lightstep_access_token ACCESSTOKEN;

  # Enable tracing for all requests.
  opentracing on;

  # Optionally, append additional information to spans.
  opentracing_tag http_user_agent $http_user_agent;

  location ~ \.php$ {
    # The operation name used for spans defaults to the name of the location
    # block, but you can use this directive to customize it.
    opentracing_operation_name $uri;
  }
}
```


