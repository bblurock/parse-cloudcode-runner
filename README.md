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
parse-cloudcode-runner hello -a '{"answer": 42}'
```

To run background jobs:
```
parse-cloudcode-runner worker -a '{"answer": 42}' -t job
```

Options are
```
  -p, --parse-path      Source root of your Parse app             [default: "."]
  -s, --json-stringify  Print result in JSON representation
                                                      [boolean] [default: false]
  -a, --arguments       Arguments (JSON String)         [string] [default: "{}"]
  -t, --type            Type of function to run
                     [string] [choices: "function", "job"] [default: "function"]
```

## Current support of `Parse.Cloud` module

* Cloud modules (by (by [flovilmart/parse-develop](https://github.com/flovilmart/parse-develop))
* function `Parse.Cloud.define`
* function `Parse.Cloud.job`
* function `Parse.Cloud.httpRequest` (by [flovilmart/parse-cloud](https://github.com/flovilmart/parse-cloud))
* class `Parse.Cloud.FunctionRequest`
* class `Parse.Cloud.FunctionResponse`
* class `Parse.Cloud.JobRequest`
* class `Parse.Cloud.JobStatus`

## TODO

1. Support of callbacks like `afterDelete` and etc.
