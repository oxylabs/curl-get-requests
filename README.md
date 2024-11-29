

[![Oxylabs promo code](https://user-images.githubusercontent.com/129506779/250792357-8289e25e-9c36-4dc0-a5e2-2706db797bb5.png)](https://oxylabs.go2cloud.org/aff_c?offer_id=7&aff_id=877&url_id=112)

# How to Send GET Requests With cURL

[cURL](https://oxylabs.io/blog/what-is-curl) is a command-line tool and a library that allows you to transfer data to and from servers using various protocols. Besides extracting public data, which can be HTML, text, JSON, images, etc., cURL can also handle sessions and cookies. Follow this guide to learn how to send and manage cURL GET requests.

For more details, check out the [full article](https://oxylabs.io/blog/curl-get-requests) on our website.

- [Steps of sending GET requests with cURL](#steps-of-sending-get-requests-with-curl)
  * [Step 1 - Simple cURL GET requests](#step-1---simple-curl-get-requests)
  * [Step 2 - GET request with parameters](#step-2---get-request-with-parameters)
  * [Step 3 - GET HTTP Headers](#step-3---get-http-headers)
  * [Step 4 - Retrieve Data in JSON Format](#step-4---retrieve-data-in-json-format)
  * [Step 5 - Follow Redirects](#step-5---follow-redirects)
  * [Step 6 - Send Cookies with a GET Request](#step-6---send-cookies-with-a-get-request)
- [cURL GET Request Arguments](#curl-get-request-arguments)

## Steps of sending GET requests with cURL

### Step 1 - Simple cURL GET requests

If the default request method is GET, you can skip `--request` option and send a GET request as follows:

```shell
curl http://httpbin.org/get
```

---

### Step 2 - GET request with parameters
A GET request with parameters allows you to send additional data to the server within the URL of your request. cURL provides two powerful options, `-d` and `-G`, to facilitate this.

Note that if you use `-d` without `-G`, the request will be a POST request. Also, if you use the `-X` option with GET value, the data you want to send with `-d` will be ignored.

Therefore, you must use `-G` along with `-d` if you want to send parameters with a GET request.

```shell
curl -G -d "param1=value1" -d "param2=value2" http://httpbin.org/get
```

In the above command, `'param1'` and `'param2'` are the keys, and `'value1'` and `'value2'` are their respective values. The `-d` option can be used multiple times to send various parameters.
Alternatively, the GET parameters can be included as part of URL:

```shell
curl 'http://httpbin.org/get?param1=value1&param2=value2'
```

---

### Step 3 - GET HTTP Headers

HTTP headers allow for exchanging additional information between the client and server during an HTTP request. To get the HTTP headers along with the response body, use the `-i` or `--include` option in the curl GET command:

```shell
curl -i http://httpbin.org/headers
```

This command retrieves the HTTP response headers, such as the server, date, content type, and content length. They provide useful information about the nature and specifics of the response data.

Note that the long parameter for fetching response headers is `--head`:

```shell
curl --head http://httpbin.org/headers
```

---

### Step 4 - Retrieve Data in JSON Format

JSON has become a standard for data exchange in the modern web development ecosystem. When interacting with [APIs via cURL](https://oxylabs.io/blog/curl-with-api), requesting data in JSON format is crucial. You can instruct cURL to accept the response in JSON format by using the `-H` option followed by `"Accept: application/json"`:

```shell
curl -H "Accept: application/json" http://httpbin.org/get
```

Note that sending `"Accept: application/json"` doesn't guarantee that the response will be returned in JSON format. **It highly depends on whether the website supports returning a JSON response.
**

---

### Step 5 - Follow Redirects

In certain scenarios, the URL you're requesting might redirect to another URL. By default, cURL doesn't follow such redirects, but you can explicitly instruct it to do so. You can achieve this by using the `-L` or `--location` option:


```shell
curl -L 'http://httpbin.org/redirect-to?url=http://httpbin.org/get'
```

---

### Step 6 - Send Cookies with a GET Request

Sometimes, you may need to send cookies with your GET request, especially when interacting with websites that require user sessions or tracking user activity. You can use the `-b` or `--cookie` option followed by the name and value of the cookie:


```shell
curl -b "username=John" http://httpbin.org/cookies
```

---

## cURL GET Request Arguments

To learn how to send GET requests with cURL, we've prepared a table that shows some key arguments, the short option, the long option, and the description. 

> [!IMPORTANT]  
> Note that you must use either the short or long option, not both.

| Argument              | Short Option | Long Option        | Description                                                                                          |
|-----------------------|--------------|--------------------|------------------------------------------------------------------------------------------------------|
| -Headers              | `-I`           | `--head`           | Retrieves HTTP headers only.                                                                         |
| Include Headers       | `-i`           | `--include`        | Includes the HTTP response headers in the output.                                                   |
| User Agent            | `-A`           | `--user-agent`     | Specifies the User-Agent string to send to the server.                                              |
| Request Type          | `-X`           | `--request`        | Specifies the request type to use (GET, POST, PUT, DELETE, etc.)                                    |
| Follow Redirects      | `-L`           | `--location`       | Follows redirects in the server's response.                                                         |
| Send Cookies          | `-b`           | `--cookie`         | Sends cookies from a string or file. Format of string should be NAME=VALUE; another=anotherval.     |
| Verbose Mode          | `-v`           | `--verbose`        | Provides more information (debug info).                                                             |
| Silent Mode           | `-s`           | `--silent`         | Silent mode. Don't output anything.                                                                 |
| Output to File        | `-o`           | `--output`         | Writes output to `<file>` instead of stdout.                                                        |
| Pass a Custom Header  | `-H`           | `--header`         | Passes a custom header to the server. To get JSON, use `-H "Accept: application/json"`.              |

