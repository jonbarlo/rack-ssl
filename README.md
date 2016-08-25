Rack::SSL
=========

Force SSL/TLS in your app.

1. Redirects all "http" requests to "https"
2. Set `Strict-Transport-Security` header
3. Flag all cookies as "secure"


Installation
------------

    gem install rack-ssl


Usage
-----

    require 'rack/ssl'
    use Rack::SSL

Securing Cookies
----------------
```
use Rack::Session::Cookie, :key => 'rack.session',
                           :domain => 'foo.com',
                           :path => '/',
                           :expire_after => 2592000, # In seconds
                           :secret => 'some_secret'
```

Note
----

> In order for `Rack::SSL` to properly work it has to be at the top of the Rack Middleware.
Using `enable :session` will place `Rack::Session::Cookie` before `Rack::SSL` and will prevent `Rack::SSL` from marking cookies as secure.
To fix this issue do not use `enable :sessions` instead add the `Rack::Session::Cookie` middleware after `Rack::SSL`.

> Remenber to chance `:secret => 'some_secret'` for something more secure like creating and using enviroment variables. e.g.: `ENV['SINATRA_SESSION_SECRET']`
