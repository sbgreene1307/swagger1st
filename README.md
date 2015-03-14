# swagger1st (swagger first)

A Clojure [Ring](https://github.com/ring-clojure/ring) middleware that does routing, serialization and validation based
on [swagger](http://swagger.io/) definitions.

Currently only supports Swagger 2.0 specification.

[![Build Status](https://travis-ci.org/sarnowski/swagger1st.svg?branch=master)](https://travis-ci.org/sarnowski/swagger1st)
[![Coverage Status](https://coveralls.io/repos/sarnowski/swagger1st/badge.svg?branch=master)](https://coveralls.io/r/sarnowski/swagger1st?branch=master)

## Usage

Use the following dependency:

[![Clojars Project](http://clojars.org/io.sarnowski/swagger1st/latest-version.svg)](http://clojars.org/io.sarnowski/swagger1st)

Add the swagger1st middleware into your ring handler chain and specify the schema location.

```clojure
(ns example
  (:require [io.sarnowski.swagger1st.core :as s1st]
            [ring.middleware.params :refer [wrap-params]]))

(def app
  (-> (s1st/swagger-executor)
      (s1st/swagger-security)
      (s1st/swagger-validator)
      (s1st/swagger-parser)
      (s1st/swagger-discovery)
      (s1st/swagger-mapper ::s1st/yaml-cp "example/api.yaml")
      (wrap-params))
```

The following swagger definition inputs are possible:

* **direct** - swagger definition already as clojure data structures
* **json** - a string containing a JSON formatted swagger definition
* **json-file** - a reference to a file, containing JSON
* **json-cp** - a reference to a classpath resource, containing JSON
* **yaml** - a string containing a YAML formatted swagger definition
* **yaml-file** - a reference to a file, containing YAML
* **yaml-cp** - a reference to a classpath resource, containing YAML

## Detailed usage

TODO

* explain different steps of the middleware and their dependencies, inputs and outputs
* explain configuration options

## License

Copyright (c) 2015, Tobias Sarnowski

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted,
provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT,
INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF
THIS SOFTWARE.
