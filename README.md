## HSC

**hsc** (http-status-checker) is a command line utility used to perform multiple HTTP status checks on remote endpoints. It is a perfect fit if you need to host multiple HTTP server on the same EC2 instance behind an Elastic Load Balancer which unfortunately allow status checks on a single HTTP interface.

#### Usage

**hsc** supports accepts options passed as environment variables or as command line arguments. The short list of options is:

* *p* - *env.PORT*, in which port running the *hsc* server (*default 9090*)
* *e* - *env.ENDPOINTS*, comma separated list of endpoints to perform checks against

Install **hsc** globally with `npm i -g http-status-checker`

**hsc** to actually check the status of the endpoints monitored you can perform a *GET* request to `http://your_ip:HSC_PORT/`, if everything looks good **hsc** will simply answer with `HTTP 200 "OK"`, otherwise with an `HTTP 500` containiung in the body a JSON object indicating which endpoint failed the check and which one looks good, eg:

```
{
    http://google.com: "OK",
    http://www.yahoo.com: "OK",
    http://foobarservice.com: "getaddrinfo ENOTFOUND foobarservice.com foobarservice.com:80"
}
```

Usage example:

* `hsc -p 9091 -e http://google.com,http://yahoo.com`

##### Note

Logs are printed in JSON suing [bunyan](https://github.com/trentm/node-bunyan), if you want you can pipe them through the bunyan command line tool to read them better.
