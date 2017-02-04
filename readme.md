# Mustacheproxyd

A HTTP proxy that transcodes origin JSON response bodies to HTML via mustache 
templates. This is useful for producing HTML output for a JSON API without
modifying the API responses directly.

## Configuration

Configuration is accomplished using a CSV file with the following columns:

| Guard RegExp URL | Target URL            | Mustache template filename |
|------------------|-----------------------|----------------------------|
| /users/(.*)      | http://example.com/$1 | ./templates/$1.mustache    |

### Guard RegExp URL
Requested URLs must match the supplied pattern before they are processed. 
Requests that do not match any pattern return HTTP 404.

### Target URL
The target URL to proxy the request to. RegExpression expansion may occur in
the target URL. Expansion occurs per request.

### Mustache template filename
The mustache template filename to use when trnascoding the response body from
the target URL. RegExpression expansion may occur in the mustache template 
filename. Expansion occurs per request.

There may have multiple rules, one per row in the configuration CSV.

## Program 

Mustacheproxyd has two command line options. They are:

- host: The proxy listening hostname and port
- config: Filepath of the configurtion CSV