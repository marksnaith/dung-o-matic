# Dung-O-Matic

## Introduction

Dung-O-Matic is a tool for evaluating Dung (1995)-style argumentation frameworks.

## Getting started

Dung-O-Matic is best run using docker. After cloning the repoisitory, run:

`$ docker-compose up`

This will build and run the docker container, with the web service API available at http://localhost:8080

## Usage

With the web service running, you can submit argumentation frameworks for evaluation using `curl`. Argumentation frameworks are expressed as JSON objects, with the following specification:

* `arguments`: an array of Strings, where each element is an individual argument
* `attacks`: an array of Strings, where each String is of the form `(x,y)` where `x` and `y` are arguments, and represents `x` attacking `y`
* `semantics` (optional): a single String specifying the evaluation semantics. Choose from: `grounded`, `preferred`, `stable` or `semistable`. Default is `grounded`.

The result of the evaluation is returned as a JSON object with the extension(s).

### Example

`$ curl -d '{"arguments":["a","b","c"], "attacks":["(a,b)","(b,a)","(b,c)"],"semantics":"preferred"}' localhost:8080`

`{"arguments":["c","b","a"],"attacks":["(a,b)","(b,a)","(b,c)"],"preferred":[["b"],["c","a"]]}`

## Acknowledgements

Development of the core Dung evaluation engine by Joseph Devereux; web API development by Mark Snaith, both while at the <a href="http://arg.tech">Centre for Argument Technology, University of Dundee</a>.
