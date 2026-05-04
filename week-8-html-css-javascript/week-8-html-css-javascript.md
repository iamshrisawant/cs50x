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
- Hyper Text Markup Language, not a programming language consisting of building blocks
- Tags are the code blocks to build a webpage
- Attributes are the properties assigned to tags to define their behaviour

### Regular Expressions
- To validate input with patterns
- Syntaxes:
    - `.` single character
    - `*` zero or more times
    - `+` one or more times
    - `?` zero or one time
    - `{n}` n times
    - `{n,m}` at least n at most m
    - `[characters]` any of ther characters enclosed in `[]`
    - `[char-char]` any one of the character from range
    - `\d` any digit
    - `\D` any character but a digit
- To escape any of these syntaxes to use as characters use `\`

### CSS
- Cascading Style Sheets - not a programming language that provides aesthetics to HTML
- Written in key-value pair properties under a selector:
    - type selector: defining style for tag
    - class selector: defining style for tags of declared class with `.` as prefix
    - ID selector: 
    - attribute selector:
- Can be written inside HTML file with style tag or attribute or in separate file linked in

### Bootstrap
- A framework to use set of premade CSS classes
- Referencing to such framework over link adds the style in that framework
- Many such frameworks exists promoting reusability of code

### Javascript
- A client-side programming language to make website interactive
- Allows fetch all data from server once and then proceed to show it computationally to allow Document Object Model(DOM)
- Defined in the script tag near end of end of HTML body to make sure all HTML exists first