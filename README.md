# dohp
dohp is a tool designed to transform DNS over HTTPS (DoH) requests into HTTP proxy requests. This utility allows users to leverage a specified HTTP proxy address to handle DNS queries and utilize DNS over HTTPS resolvers for domain name resolution. One of its significant features is the ability to bypass local DNS queries by directly accessing IP addresses, which can be useful in scenarios where local DNS may be restricted or unreliable.
## Features
- DoH to HTTP Proxy Conversion: Converts DNS over HTTPS requests to standard HTTP proxy requests.
- Customizable Resolver: Allows users to specify a DNS over HTTPS resolver URL.
- Verbose Logging: Provides detailed logging for debugging purposes, including TLS handshake information.
- Certificate Verification Control: Option to ignore certificate errors for testing or insecure environments.
- Bypass Local DNS: Supports direct access to IP addresses, bypassing local DNS queries.
## Installation
- Clone the Repository:
```bash
git clone https://github.com/novohool/dohp.git
cd dohp
```
- Build the Binary:
```bash
go build -o dohp main.go
```
## Usage
### Basic Usage
To start the HTTP proxy on a specific address using the default DNS over HTTPS resolver:

```bash
./dohp -L http://:8080
```
This command starts the proxy on port 8080 and uses the default DNS over HTTPS resolver (`https://dns.google/dns-query`).
- Custom DNS over HTTPS Resolver
To use a custom DNS over HTTPS resolver:

```bash
./dohp -L http://:8080 -doh https://your-doh-resolver/dns-query
```
### Bypass Local DNS with IP Access
To bypass local DNS queries and directly access an IP address, you can use the IP address instead of the domain name in your requests. For example, if you know the IP address of a website is 192.0.2.1, you can make requests directly to this IP address through the proxy.

#### Configure Your Application:
Set your application to use the proxy address (http://localhost:8080 in the previous examples).
When making requests, use the IP address instead of the domain name. For example, in a curl command:
```bash
curl -x http://localhost:8080 http://www.google.com
```

This way, the request goes directly to the IP address, skipping the local DNS lookup.

This option disables the default behavior of ignoring certificate errors.
- Verbose Logging:
```bash
./dohp -L http://:8080 -v
```
Enables verbose logging, which includes detailed information about TLS handshakes, packets, and ClientHello details.
Command Line Flags
- -I: Fetch response headers only.
- -v: Enable verbose logging.
- -help: Show usage help information.
- -L: Run HTTP proxy on the specified address (e.g., http://:8080).
- -doh: DNS over HTTPS resolver URL (default: https://dns.google/dns-query).
## License
This project is licensed under the MIT License - see the LICENSE file for details.
