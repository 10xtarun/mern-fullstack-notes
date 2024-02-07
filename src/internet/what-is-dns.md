# What is DNS?

DNS, or Domain Name System, is a hierarchical decentralized system that translates human-readable domain names into IP addresses. It acts as a directory service for the internet, helping users access websites and services using easy-to-remember domain names instead of numerical IP addresses. Working of DNS is as follows:

1. User Enters a Domain Name:

2. When a user enters a domain name (e.g., https://www.edba-academy.com/) into a web browser, the browser needs to find the IP address of the server hosting that website.
Local DNS Resolver (DNS Resolver):

3. The user's device first checks its local DNS resolver, which is typically provided by the Internet Service Provider (ISP). This resolver may have the IP address for the requested domain in its cache.
Root DNS Servers:

4. If the local resolver doesn't have the IP address, it contacts the root DNS servers. There are 13 root DNS servers worldwide. These servers provide information about top-level domains (TLDs) like .com, .org, and country-code TLDs (e.g., .uk, .jp).
TLD DNS Servers:

5. The root DNS servers direct the resolver to the TLD DNS servers responsible for the specific domain extension (e.g., .com). The resolver then queries the TLD DNS servers for information about the authoritative name server for the requested domain.
Authoritative Name Server:

6. The TLD DNS servers respond with the IP address of the authoritative name server for the requested domain. The authoritative name server holds the DNS records for the domain.
Querying Authoritative Name Server:

7. The resolver sends a query to the authoritative name server, asking for the IP address associated with the requested domain.
DNS Record Response:

8. The authoritative name server responds with the IP address for the requested domain.
Cache Update:

9. The local resolver caches the IP address for future use, reducing the need to repeat the entire DNS lookup process for the same domain.
Final IP Address Response:

10. The resolver provides the IP address to the user's device, allowing the browser to connect to the web server hosting the requested website.

Example:
1. Let's use the domain "https://www.edba-academy.com/" as an example:

2. User enters "https://www.edba-academy.com/" in the browser.
3. Local DNS resolver checks its cache.
4. If not found, it queries root DNS servers.
5. Root DNS servers direct to .com TLD DNS servers.
6. TLD DNS servers provide authoritative name server for "example.com."
7. Authoritative name server gives the IP address for "https://www.edba-academy.com/."
8. The IP address is returned to the local resolver.
9. The browser uses the IP address to connect to the web server hosting https://www.edba-academy.com/.
10. This entire process happens in the background, allowing users to access websites using easy-to-remember domain names while the underlying infrastructure deals with the translation to IP addresses.

---