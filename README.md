# Hit server bench

Comparison of raw HTTP hit performance of:

- [Node.js](http://nodejs.org)
- [Spray (Scala)](http://spray.io)
- [Erlang HTTP server](http://erlang.org/doc/apps/inets/http_server.html)
- [Http-kit (Clojure)](http://http-kit.org/index.html)
- [Warp (Haskell)](http://hackage.haskell.org/package/warp)
- [Tornado](http://www.tornadoweb.org/en/stable/)
- [Puma (Ruby)](http://puma.io/)

## Results

See `*-results.txt` for `wrk` benchmark results.

| Environment | Req/s (concurrency 1) | Req/s (concurrency 10) | Req/s (concurrency 50) | Req/s (concurrency 100) |
|-------------|----------------------:|-----------------------:|-----------------------:|------------------------:|
| Node.js     |               8590.95 |               19619.37 |               19217.57 |                19606.67 |
| Spray       |               7595.75 |               18592.71 |               29571.34 |                31541.73 |
| Erlang      |               6750.29 |               15574.33 |               13455.14 |                13931.52 |
| Http-kit    |              10145.90 |               34416.03 |               36520.01 |                34391.64 |
| Warp        |              12640.29 |               27749.54 |               26365.52 |                23916.69 |
| Tornado     |               2356.82 |                4590.33 |                4422.08 |                 4155.61 |
| Puma        |               6196.16 |               10780.66 |               12091.95 |                10586.83 |
| Netty       |              21354.85 |               67693.31 |               71727.45 |                67523.18 |
| Spark (Jetty) |               9637.85 |               21704.97 |               22607.68 |                28059.16 |
| Spring Boot (Tomcat) |               5087.81 |               13472.72 |               16365.36 |                17187.06 |
| Reactor     |              11190.68 |               31946.53 |               30796.76 |                30590.69 |
| PHP-FPM     |               1616.16 |                   1.60 |                   6.40 |                 1427.93 |
| HHVM        |               1498.68 |                5584.94 |                5314.37 |                 4804.49 |
| ReactPHP (PHP) |               1664.91 |                9570.31 |               13253.46 |                12034.07 |
| ReactPHP (HHVM) |               1248.12 |               10987.09 |               17032.59 |                18142.91 |


## I don't believe you!

You can checkout the repo and do benchmarking yourself.

Starting Node.js app:

    $ cd node
    $ node main.js
    Open new terminal window.
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Spray (Scala) app:

    $ cd spray
    $ sbt run
    Open new terminal window.
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Erlang app:

    $ cd erlang
    $ erl
    $ c(erlanghttp).
    $ erlanghttp:start().
    Open new terminal window.
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Http-kit app:

    $ cd httpkit
    $ lein run
    Open new terminal window.
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Warp (Haskell) app:

    $ cd warp
    $ ./warped
    Open new terminal window.
    $ ../do-benchmark.sh http://127.0.0.1:8080/

    # To compile, run:
    $ cd warp
    $ ghc -O3 warped.hs

Starting Puma + Rack (Ruby) app:

    $ cd puma-rack
    $ bundle install # Install gems
    # puma -C puma.rb
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Netty app:

    $ cd netty
    $ mvn install
    $ mvn compile
    $ mvn exec:java -Dexec.mainClass=NettyServer
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Spark app:

    $ cd spark
    $ mvn install
    $ mvn compile
    $ mvn exec:java -Dexec.mainClass=SparkMain
    $ ../do-benchmark.sh http://127.0.0.1:8080/

Starting Spring boot app:

    $ cd spring-boot
    $ mvn install
    $ mvn compile
    $ mvn exec:java -Dexec.mainClass=SpringBootMain

Starting Reactor app:

    $ cd reactor
    $ mvn install
    $ mvn compile
    $ mvn exec:java -Dexec.mainClass=ReactorExample

Starting PHP-FPM:

    $ cd php-fpm
    $ ./start.sh    # starts PHP-FPM and nginx

Starting HHVM:

    $ cd hhvm
    $ ./start.sh    # starts HHVM and nginx

Starting ReactPHP (PHP):

    $ cd reactphp
    $ ./start.sh    # starts ReactPHP using PHP and nginx

Starting ReactPHP (HHVM):

    $ cd reactphp
    $ ./start.sh    # starts ReactPHP using HHVM and nginx

## Kudos to

- [@olegsmith](https://github.com/olegsmith) for fixing Node.js to use clustering and Erlang benchmark
- [@ollie](https://github.com/ollie) for Warp and Puma
