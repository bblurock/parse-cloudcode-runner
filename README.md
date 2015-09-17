# Parse CloudCode Runner

## Setup

### Install
```
npm install parse-cloudcode-runner
```

### Change code
Modify your `cloud/main.js` by adding following lines before calling any `Parse` and `require` function.
```javascript
if (typeof Parse === 'undefined') {
    var parseCloudCodeRunner = require('parse-cloudcode-runner');
    /*globals require: true */
    require = parseCloudCodeRunner.require;
    var Parse = parseCloudCodeRunner.Parse;
    Parse.initialize('YOUR_PARSE_APPLICATION_ID', 'YOUR_PARSE_JAVASCRIPT_KEY');
}
```
(In Parse's CloudCode environment, `Parse` is globally available. But in local development environment,
you have to import it by yourself. Check `sample/cloud/main.js` for example.)

_Note: you could use [motdotla/dotenv](https://github.com/motdotla/dotenv)
to load your Parse credentials from environment._

### Run
Run your cloud code function by
```
parse-cloudcode-runner <function name> [Options]
```
like
```
parse-cloudcode-runner hello -p sample -a '{"answer": 42}'
```

Options are
```
  -p, --parse-path          Source root of your Parse app         [default: "."]
  -a, --arguments           Arguments (JSON String)     [string] [default: "{}"]
  -h, --help                Show help                                  [boolean]
  -s, --json-stringify                                [boolean] [default: false]
```

## Current support of `Parse.Cloud` module

* function `Parse.Cloud.define`
* function `Parse.Cloud.httpRequest` (by [flovilmart/parse-cloud](https://github.com/flovilmart/parse-cloud))
* class `Parse.Cloud.FunctionRequest`
* class `Parse.Cloud.FunctionResponse`

## TODO

1. Support of callbacks like `afterDelete` and etc.
