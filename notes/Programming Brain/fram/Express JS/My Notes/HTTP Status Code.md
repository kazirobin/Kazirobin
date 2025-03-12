# HTTP Status Code

The HTTP status code is a three-digit number that indicates the success or failure of an HTTP request. These numbers are usually displayed in the browser’s address bar and can also find them in logs, error messages and other places.

The first digit of the code defines the category of the response (e.g., `1xx` for informational, `2xx` for success, `4xx` for client errors, `5xx` for server errors).

A common status code is `200 OK`, which means the request was successful.

HTTPS Response Status Codes `1xx` Series

| Code | Reason Phrase |
| --- | --- |
| 100 | Continue |
| 101 | Switching Protocols |
| 102 | Processing |

HTTPS Response Status Codes `2xx` Series – Success

| Code | Reason Phrase |
| --- | --- |
| 200 | OK |
| 201 | Created |
| 202 | Accepted |
| 203 | Secondary Source Information |
| 204 | No Content |
| 205 | Content Reset |
| 206 | Partial Reset |
| 207 | Multistate |
| 208 | Already Reported |
| 226 | IM Used |

HTTPS Response Status Codes `3xx` Series – Redirect

| Code | Reason Phrase |
| --- | --- |
| 300 | Multiple Choices |
| 301 | Moved Permanently |
| 302 | Found |
| 303 | See Elsewhere |
| 304 | Unmodified |
| 305 | Use Proxy |
| 306 | Change Proxy |
| 307 | Temporary Redirect |
| 308 | Permanent Redirect |

HTTP status codes `4хх` Series – Web client error

| Code | Reason Phrase |
| --- | --- |
| 400 | Bad Request |
| 401 | Unauthorized |
| 402 | Payment Required |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 406 | Not Acceptable |
| 407 | Proxy Authentication Required |
| 408 | Request Timeout |
| 409 | Conflict |
| 410 | Gone |
| 411 | Length Required |
| 412 | Precondition Failed |
| 413 | Payload Too Large |
| 414 | URI Too Long |
| 415 | Unsupported Media Type |
| 416 | Range Not Satisfiable |
| 417 | Expectation Failed |
| `418-420` | `Unassigned` |
| 421 | Misdirected Request |
| 422 | Unprocessable Entity |
| 423 | Locked |
| 424 | Failed Dependency |
| 425 | Too Early |
| 426 | Upgrade Required |
| `427` | `Unassigned` |
| 428 | Precondition Required |
| 429 | Too Many Requests |
| `430` | `Unassigned` |
| 431 | Request Header Fields Too Large |
| `432-450` | `Unassigned` |
| 451 | Unavailable For Legal Reasons |
| `452-499` | `Unassigned` |

HTTP status code class `5xx` series – server error

| Code | Reason Phrase |
| --- | --- |
| 500 | Internal Server Error |
| 501 | Not Implemented |
| 502 | Bad Gateway |
| 503 | Server Not Available |
| 504 | Gateway Timeout Expired |
| 505 | Unsupported Version of HTTP |
| 506 | Variant Also Trades |
| 507 | Insufficient Storage |
| 509 | Bandwidth Limit Exceeded |
| 510 | No Extension |
| 511 | Network Authentication Required |