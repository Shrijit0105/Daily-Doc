# How DNS Works: Understanding the Internet's Phonebook

## 1. Introduction

Every time we open a website, we usually enter a domain name such as:

```text
www.google.com
```

But computers communicate with each other using IP addresses.

So how does our browser know which server to contact when we enter a domain name?

The answer is DNS, which stands for **Domain Name System**.

DNS is one of the fundamental systems that makes the internet easier to use. Instead of remembering numerical IP addresses for every website, we can use human-readable domain names.

In this document, I want to understand how DNS works, what happens behind the scenes when we open a website, and why this system is important for networking and web development.

## 2. What Is DNS?

DNS is a distributed naming system that translates domain names into information such as IP addresses.

For example:

```text
google.com → IP address
```

A browser needs the destination IP address to establish communication with the appropriate server.

DNS helps it discover that information.

We can compare DNS to the contacts application on a smartphone.

Instead of remembering someone's phone number, we save their name and look up the number when needed.

DNS follows a similar idea, except it operates across a globally distributed system.

## 3. Why Do We Need DNS?

Imagine if we had to remember the IP address of every website we visited.

We might have to remember something like:

```text
142.250.x.x
```

for a particular service instead of simply typing its domain name.

This would make browsing inconvenient.

DNS solves this problem by providing a system where domain names can be resolved into network addresses.

It also allows website owners to change hosting infrastructure without necessarily changing the domain name users type.

## 4. Understanding Domain Names

Let's break down this domain:

```text
www.example.com
```

It contains different parts.

- `www` is a subdomain.
- `example` is the second-level domain.
- `.com` is the top-level domain (TLD).

The final dot in a fully qualified domain name represents the DNS root, although browsers usually hide it.

A domain name is organised hierarchically.

This hierarchy helps DNS distribute responsibility across different organisations and servers.

## 5. How Does DNS Resolution Work?

Let's understand what happens when we enter:

```text
www.example.com
```

The browser needs to find the corresponding IP address.

A simplified resolution process looks like this:

```text
User enters domain name
          |
          v
Browser checks its DNS cache
          |
          v
Operating system checks its cache
          |
          v
DNS resolver receives the query
          |
          v
Root DNS server
          |
          v
TLD DNS server
          |
          v
Authoritative DNS server
          |
          v
IP address is returned
          |
          v
Browser connects to the server
```

This is a simplified example of a DNS lookup. Real systems may use cached results at different stages, so every lookup does not necessarily contact all these servers.

Let's understand each component.

### A. DNS Resolver

A DNS resolver receives DNS queries from applications or operating systems.

It is generally operated by an internet service provider or a public DNS provider.

Its job is to find the requested DNS information, either from its cache or by querying other DNS servers.

### B. Root DNS Servers

Root DNS servers are at the top of the DNS hierarchy.

They do not normally provide the final IP address of a website.

Instead, they direct resolvers towards the appropriate top-level domain servers.

For example, a query for a `.com` domain can be directed towards the relevant `.com` TLD servers.

### C. TLD DNS Servers

TLD stands for Top-Level Domain.

Examples include:

- `.com`
- `.org`
- `.net`
- `.in`
- `.edu`

TLD servers help identify the authoritative DNS servers responsible for a particular domain.

### D. Authoritative DNS Server

An authoritative DNS server stores the actual DNS records for a domain.

It can provide the requested information, such as an IPv4 address.

For example:

```text
www.example.com → 93.184.216.34
```

This is an illustrative address mapping.

The resolver can return the answer to the client, which can then connect to the destination server.

## 6. Important DNS Record Types

DNS does more than translate domain names into IPv4 addresses.

It supports different types of records for different purposes.

| Record | Purpose |
|---|---|
| A | Maps a domain name to an IPv4 address |
| AAAA | Maps a domain name to an IPv6 address |
| CNAME | Creates an alias pointing to another domain name |
| MX | Specifies mail servers for a domain |
| NS | Identifies authoritative name servers |
| TXT | Stores text information, often used for verification and email security |
| PTR | Used for reverse DNS lookups |

Let's look at a few examples.

### A Record

```text
example.com → 192.0.2.10
```

An A record maps a hostname to an IPv4 address.

### AAAA Record

An AAAA record maps a hostname to an IPv6 address.

### CNAME Record

A CNAME record makes one domain name an alias of another.

For example:

```text
blog.example.com → example.com
```

A CNAME does not directly store an IP address. It points to another canonical domain name.

### MX Record

MX records help email systems determine which mail servers handle incoming email for a domain.

### TXT Record

TXT records store text data associated with a domain.

They are commonly used for domain verification and email authentication mechanisms such as SPF and DKIM.

## 7. What Is DNS Caching?

Imagine opening the same website repeatedly.

Would it make sense to perform the entire DNS lookup process every single time?

Not really.

This is why DNS caching exists.

DNS information can be temporarily stored at different locations, including:

- Browser DNS cache
- Operating system DNS cache
- Recursive DNS resolver cache

When a cached record is still valid, the system can reuse it instead of performing another complete lookup.

The duration for which a DNS record can be cached is controlled by its **TTL (Time To Live)**.

For example:

```text
TTL = 3600 seconds
```

This means the record can generally be cached for up to one hour.

Caching reduces unnecessary DNS queries and can improve response times.

## 8. What Is DNS Propagation?

Sometimes, when we change a domain's DNS records, the changes do not appear everywhere immediately.

People often refer to this as DNS propagation.

For example, suppose we move a website to a new hosting provider and update its IP address.

Some DNS resolvers may still have the previous record cached.

They may continue using that record until its TTL expires or their cache is otherwise refreshed.

This is why DNS changes can take time to appear consistently across different networks.

## 9. DNS and Cybersecurity

DNS is also an important part of cybersecurity.

Since DNS helps users locate online services, attackers sometimes exploit it.

A few examples:

### DNS Spoofing

An attacker attempts to provide false DNS information so that a user is directed to an unintended destination.

### DNS Hijacking

An attacker changes DNS settings or records to redirect users towards malicious websites.

### DNS Tunnelling

Attackers can abuse DNS queries and responses to transfer information through DNS traffic.

This technique may be used to bypass certain network restrictions or communicate with compromised systems.

Understanding DNS is therefore useful not only for networking but also for security engineering.

## 10. DNS Over HTTPS (DoH)

Traditional DNS queries are commonly sent without encryption at the DNS transport layer.

This means network observers may be able to inspect DNS traffic.

DNS over HTTPS, commonly called DoH, sends DNS queries through HTTPS connections.

Its main purpose is to protect DNS queries from being easily observed or modified while they travel across the network.

However, DoH does not make all internet activity anonymous. Websites, network services, and other systems may still collect information about connections.

## 11. Practical Experiment: Performing DNS Lookups

We can experiment with DNS directly from our computers.

### Windows Command Prompt

Open Command Prompt and execute:

```bash
nslookup google.com
```

This command asks a DNS resolver to look up the domain.

We can also query a particular record type.

For an IPv4 address:

```bash
nslookup -type=A google.com
```

For mail server records:

```bash
nslookup -type=MX google.com
```

To inspect the DNS cache on Windows:

```bash
ipconfig /displaydns
```

To clear the local DNS resolver cache:

```bash
ipconfig /flushdns
```

Be aware that clearing the local cache does not clear caches maintained by your browser or external DNS resolvers.

### Using Python

Python also provides tools for working with DNS.

One popular third-party library is `dnspython`.

Install it using:

```bash
pip install dnspython
```

Example:

```python
import dns.resolver

domain = "google.com"

answers = dns.resolver.resolve(domain, "A")

for answer in answers:
    print(answer)
```

This program queries DNS for the A records associated with the domain.

It is a small example, but it demonstrates how DNS functionality can be integrated into Python applications.

## 12. Why DNS Matters in Software Development

DNS is not just a networking concept.

It is directly connected to several areas of software engineering.

**Web Development:** Browsers use DNS to locate the servers hosting websites and APIs.

**Cloud Computing:** Applications deployed on cloud platforms often use domain names to access services and resources.

**Backend Engineering:** APIs, databases, and microservices may communicate using hostnames.

**DevOps:** DNS configuration is important when deploying applications, configuring load balancers, and managing domains.

**Cybersecurity:** DNS monitoring can help identify suspicious network activity.

A developer who understands DNS can troubleshoot problems that might otherwise look like application failures.

## 13. What I Learned

The most interesting thing about DNS is that something as simple as entering a website address triggers a process involving multiple systems working together.

DNS removes the need for humans to remember IP addresses while providing a scalable way to organise internet naming.

I also learned about DNS hierarchy, recursive resolvers, authoritative servers, record types, caching, and DNS security.

Understanding these concepts gives me a better foundation for learning computer networking, cloud computing, and backend development.

## 14. Questions for Further Exploration

1. What is the difference between a recursive DNS resolver and an authoritative DNS server?
2. Why do we need both IPv4 and IPv6 DNS records?
3. What happens when a DNS server becomes unavailable?
4. How does DNS caching reduce network traffic?
5. What is the difference between DNS over HTTPS and traditional DNS?
6. Can two different domain names point to the same IP address?
7. How does DNS work when a website uses a Content Delivery Network (CDN)?
8. What happens when a DNS record's TTL expires?

---

**Next learning target:** Understand how HTTP and HTTPS work, including TCP connections, TLS handshakes, and how a browser communicates with a web server.
