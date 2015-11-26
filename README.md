An example implementation of the [pacto library](https://github.com/thoughtworks/pacto/).

## To run the tests

This example tests a simple HTTP api that provides json responses. There are two endpoints (`ping` and `/lat/lon`) and a generic 404 response test. To run it:

```bash
bundle exec rake pacto:validate['https://tide-api.herokuapp.com','contracts']
```

## To run a stub server

Pacto can act as a stub server, and it will respond with data present in the `examples` part of the contracts. As a stub server, it will also validate that request and response conform to contract. To run the server:

```bash
bundle exec pacto-server -sv -V --stub
```

You can then send requests to the stub server:

```bash
curl localhost:9000/ping
```

or

```bash
curl localhost:9000//23.98E/11.45N
```

## To run pacto server as a middleman dispute settler

Pacto server can also act as a middleman, and proxy requests to a live service while validating the request and response contract. This is particularly valuable for integration testing, to provide confidence that both the stubbing and the contract testing are valuable on their own. You can run the server as a middleman like this:

```bash
bundle exec pacto-server -sv -V --live -H https://tide-api.herokuapp.com
```

and then execute a request that will fail validation against the contract:

```bash
curl localhost:9000/23.98E/11.45N
```

## And so much more!

Visit the pacto website for full documentation and other ways to use the library: [https://thoughtworks.github.io/pacto/](https://thoughtworks.github.io/pacto/)
