# Enrichable http client

the `go-enrichable-client` package is wrapper over the standard `net/http` client library 
allowing to enrich it functionality by using middleware extensions.

**Example of pure http.client usage**

```go
package main

import "github.com/shuvava/go-enrichable-client/client"

func main() { 
	// creates http client with with idle connections 
	// and keepalives disabled.
  c := client.DefaultHTTPClient()
  resp, err := c.Get(url)	
  ...
}
```

## Middleware 

|  Name  | Description             |
|:------:|:-----------------------:|
| Retry  | add retry functionality |

### Retry middleware

This middleware adds retry functionality with automatic retries and exponential backoff policy. Currently, package supports only json content type

**Example usage retryable client**

```go
package main

import (
	"github.com/shuvava/go-enrichable-client/client"
  "github.com/shuvava/go-enrichable-client/middleware"
)

func main() {
  // create enriched client
  richClient := client.DefaultClient()
  // add retry middleware
  richClient.Use(middleware.Retry())
  // receive reference to http.Client
  c := richClient.Client
  resp, err := c.Get(url)	
  ...
}
```

## Links 

* [AWS error handling](https://docs.aws.amazon.com/apigateway/api-reference/handling-errors/)
* [hashicorp http client](https://github.com/hashicorp/go-retryablehttp.git)
