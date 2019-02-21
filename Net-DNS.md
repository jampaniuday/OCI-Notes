# DNS

## DNS Records

Also see [DNS Record Types](https://en.wikipedia.org/wiki/List_of_DNS_record_types "Wikipedia DNS Article")

### Supported by OCI DNS

- A Address Record
- NS Name Server Record
- SOA Start of Authority Record
  
OCI DNS also has an Alias record that is used only within the OCI environment (not visible to external resolvers)

### The 'dot'

CNAME, MX and NS names must end with a period or _dot_

The dot indicates that name is an FQDN

See [Why CNAME/MX/NS targets require a “dot”](https://stackexchange.github.io/dnscontrol/why-the-dot)

