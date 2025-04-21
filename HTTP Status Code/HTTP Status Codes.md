# HTTP Status Codes - Detailed Reference

HTTP status codes are 3-digit responses returned by servers to indicate the outcome of a client’s request. They are grouped into 5 categories:

---

## 🔵 1xx - Informational

These codes indicate a provisional response. The client should be prepared to receive another response.

|Code|Meaning|Description|
|---|---|---|
|100|Continue|The server has received the request headers, and the client should proceed to send the request body.|
|101|Switching Protocols|The requester has asked the server to switch protocols and the server has agreed.|
|102|Processing (WebDAV)|Server has received and is processing the request, but no response is available yet.|

---

## 🟢 2xx - Success

These codes indicate that the client’s request was successfully received, understood, and accepted.

|Code|Meaning|Description|
|---|---|---|
|200|OK|The request has succeeded.|
|201|Created|The request has been fulfilled and resulted in a new resource being created.|
|202|Accepted|The request has been accepted for processing, but the processing is not complete.|
|203|Non-Authoritative Info|The returned meta-information is not from the origin server, but a copy from a local or third-party.|
|204|No Content|The server successfully processed the request, but is not returning any content.|
|205|Reset Content|The server successfully processed the request, and asks the client to reset the document view.|
|206|Partial Content|The server is delivering only part of the resource due to a range header sent by the client.|

---

## 🟡 3xx - Redirection

These codes indicate that further action is needed to complete the request.

|Code|Meaning|Description|
|---|---|---|
|300|Multiple Choices|Indicates multiple options for the resource. The client must choose one.|
|301|Moved Permanently|The resource has been moved to a new URL permanently.|
|302|Found|The resource has been temporarily moved to another URL.|
|303|See Other|Directs the client to get the resource from another URI using GET.|
|304|Not Modified|Indicates the resource has not been modified since the last request.|
|305|Use Proxy|Deprecated. The requested resource must be accessed through a proxy.|
|307|Temporary Redirect|The request should be repeated with another URL, but future requests should still use the original URL.|
|308|Permanent Redirect|Similar to 301 but method and body will not be changed.|

---

## 🔴 4xx - Client Errors

These codes indicate the request contains bad syntax or cannot be fulfilled.

|Code|Meaning|Description|
|---|---|---|
|400|Bad Request|The request cannot be fulfilled due to bad syntax.|
|401|Unauthorized|Authentication is required and has failed or not been provided.|
|402|Payment Required|Reserved for future use (e.g., digital payment systems).|
|403|Forbidden|The request is understood but is being refused.|
|404|Not Found|The resource could not be found.|
|405|Method Not Allowed|The method is not allowed for the requested URL.|
|406|Not Acceptable|The requested resource is not capable of generating content acceptable according to Accept headers.|
|407|Proxy Authentication Required|Client must first authenticate with the proxy.|
|408|Request Timeout|The server timed out waiting for the request.|
|409|Conflict|The request could not be completed due to a conflict with the current state.|
|410|Gone|The resource is no longer available and will not be available again.|
|411|Length Required|The request did not specify the length of its content.|
|412|Precondition Failed|The server does not meet one of the preconditions specified by the client.|
|413|Payload Too Large|The request is larger than the server is willing or able to process.|
|414|URI Too Long|The URI provided was too long for the server to process.|
|415|Unsupported Media Type|The media format of the requested data is not supported.|
|416|Range Not Satisfiable|The range specified by the Range header can't be fulfilled.|
|417|Expectation Failed|The server cannot meet the requirements of the Expect request-header field.|
|418|I'm a teapot|(RFC 2324) A joke code. The server refuses to brew coffee in a teapot.|
|429|Too Many Requests|The user has sent too many requests in a given amount of time (rate limiting).|

---

## 🔥 5xx - Server Errors

These codes indicate that the server failed to fulfill a valid request.

|Code|Meaning|Description|
|---|---|---|
|500|Internal Server Error|A generic error message, given when no more specific message is suitable.|
|501|Not Implemented|The server either does not recognize the request method or lacks the ability to fulfill it.|
|502|Bad Gateway|The server was acting as a gateway or proxy and received an invalid response.|
|503|Service Unavailable|The server is currently unavailable (overloaded or down).|
|504|Gateway Timeout|The server was acting as a gateway or proxy and did not receive a timely response.|
|505|HTTP Version Not Supported|The server does not support the HTTP protocol version used in the request.|

---

Would you like a downloadable version of this or examples of how these are used in APIs?