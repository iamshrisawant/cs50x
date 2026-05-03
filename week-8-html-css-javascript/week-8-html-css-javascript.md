# [Lecture 8](https://cs50.harvard.edu/x/weeks/8/)

- Most of the applications that we use are web/browser based
- HTML, CSS, Javascript are tools to design such applications and deploy them
- These application are accessible over the internet which a network of interconnected servers, routers and other such devices.

### TCP/IP
- There are a lot of ways data can travel from one point to another and it's not neccessary that the mode would be shortest but the least expensive.
- Internet Protocol(IP) gives a unique numeric address to each device contained in data packet for source and destination
- Transmission COntrol Protocol(TCP):
    - identifies a service(email) or resource(data) inside the internet packet
    - allows multiplexing - multiple services
    - ensures data delivery

### DNS
- Every campus, home or company has a domain name server
- A name can be associated with IP addresses to access a particular service over internet
- Root servers know IP for all service domains over the internet and our devices simply fetch the addresses from these

### DHCP
- Broadcasts a message to know IP address over the network
- Modern local networks are based on this
- Even Wi-Fi networks and campus networks have adopted

### HTTP
- Requests web-pages and recives web-pages
- Hyper-Text Transfer Protocol, added with a S(HTTPS) mentions it's Secure
- Accesses the domain name and requests it's root to respond with contents

### Status Codes
- `curl` - connect url is a headless browser to check for requests and responses details such as status codes
- Codes are as follows:
    - 200 - Ok. response may contain requested contents
    - 301 - Detour to other URL as contents moved permanantly
    - 404 - File not found at the URL
- 400s are associated with user side errors, 500s are associated with server side

### Inspecting Browser
- Developer tools exist to help inspect browser contents
- Give better representations of URL response
- May also show all contents fetched in structuredmanner

### HTML