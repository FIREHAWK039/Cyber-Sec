## Security Headers

HTTP Security Headers help improve the overall security of the web application by providing mitigations against attacks like Cross-Site Scripting (XSS), clickjacking, and others. We will now dig deeper into the following security headers:

- Content-Security-Policy (CSP)
- Strict-Transport-Security (HSTS)
- X-Content-Type-Options
- Referrer-Policy

You can use a site like [https://securityheaders.io/(opens in new tab)](https://securityheaders.io/) to analyse the security headers of any website. After the discussion in this task, you will hopefully have a better understanding of what it is reporting on.

### Content-Security-Policy (CSP)

A CSP header is an additional security layer that can help mitigate against common attacks like Cross-Site Scripting (XSS). Malicious code could be hosted on a separate website or domain and injected into the vulnerable website. A CSP provides a way for administrators to say what domains or sources are considered safe and provides a layer of mitigation to such attacks.

Within the header itself, you may see properties such as `default-src` or `script-src` defined and many more. Each of these give an option to an administrator to define at various levels of granularity, what domains are allowed for what type of content. The use of self is a special keyword that reflects the same domain on which the website is hosted.

Looking at an example CSP header:

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

We see the use of:

- **default-src**  
    - which specifies the default policy of self, which means only the current website.  
      
    
- **script-src**  
    - which specifics the policy for where scripts can be loaded from, which is self along with scripts hosted on `https://cdn.tryhackme.com`  
      
    
- **style-src**  
    - which specifies the policy for where style CSS style sheets can be loaded from the current website (self)

### Strict-Transport-Security (HSTS)

The HSTS header ensures that web browsers will always connect over HTTPS. Let's look at an example of HSTS:

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

  
Here’s a breakdown of the example HSTS header by directive:

- **max-age**  
    - This is the expiry time in seconds for this setting  
      
    
- **includeSubDomains**  
    - An optional setting that instructs the browser to also apply this setting to all subdomains.  
      
    
- **preload  
    **- This optional setting allows the website to be included in preload lists. Browsers can use preload lists to enforce HSTS before even having their first visit to a website.

### X-Content-Type-Options

The X-Content-Type-Options header can be used to instruct browsers not to guess the MIME type of a resource but only use the Content-Type header. Here’s an example:

`X-Content-Type-Options: nosniff`

Here’s a breakdown of the X-Content-Type-Options header by directives:

- **nosniff**  
    - This directive instructs the browser not to sniff or guess the MIME type.

### Referrer-Policy

This header controls the amount of information sent to the destination web server when a user is redirected from the source web server, such as when they click a hyperlink. The header is available to allow a web administrator to control what information is shared.  Here are some examples of Referrer-Policy:

- `Referrer-Policy: no-referrer`
- `Referrer-Policy: same-origin`
- `Referrer-Policy: strict-origin`
- `Referrer-Policy: strict-origin-when-cross-origin`

Here’s a breakdown of the Referrer-Policy header by directives:

- **no-referrer**  
    - This completely disables any information being sent about the referrer  
      
    
- **same-origin**  
    - This policy will only send referrer information when the destination is part of the same origin. This is helpful when you want referrer information passed when hyperlinks are within the same website but not outside to external websites.  
      
    
- **strict-origin**  
    - This policy only sends the referrer as the origin when the protocol stays the same. So, a referrer is sent when an HTTPS connection goes to another HTTPS connection.  
      
    
- **strict-origin-when-cross-origin**  
    - This is similar to strict-origin except for same-origin requests, where it sends the full URL path in the origin header.

Answer the questions below

In a Content Security Policy (CSP) configuration, which property can be set to define where scripts can be loaded from?

Correct Answer

When configuring the Strict-Transport-Security (HSTS) header to ensure that all subdomains of a site also use HTTPS, which directive should be included to apply the security policy to both the main domain and its subdomains?

Correct Answer

Which HTTP header directive is used to prevent browsers from interpreting files as a different MIME type than what is specified by the server, thereby mitigating content type sniffing attacks?

Correct Answer