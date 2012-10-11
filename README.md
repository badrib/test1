cloudflash
==========

CloudFlash is a web framework for cloud based automation of openvpn, dhcp,firmware, modules, and services.

CloudFlash supports JSON data serialization format. The format for both the request and the response
should be specified by using the Content-Type header, the Accept header.

Steps to Install
===============
1) Download cloudflash files into your system
2) Run the follwing commands in cloudflash directory
   - npm install 
   - sudo coffee cloudflash.coffee

Note: During new service post, deb package uses npm to fetch the published package

Webproxy
========

Webproxy is a system that passes along the http protocol request to the target url and returns the response from the target url to the system. In our scenario the cloudflash webproxy module does the passing of http protocol request to the target(CNAME) and the URL is identified by wildcard charachter *(Any URL in CNAME system) at the end point.

*List of APIs*
==============

<table>
  <tr>
    <th>Verb</th><th>URI</th><th>Description</th>
  </tr>
  <tr>
    <td>POST</td><td>/webproxy/cname/*</td><td>HTTP POST request is passed to target, identified by cname for the URL provided after /cname/</td>
  </tr>
  <tr>
    <td>GET</td><td>/webproxy/cname/*</td><td>HTTP GET request is passed to target, identified by cname for URL given after /cname/</td>
  </tr>

  <tr>
    <td>DELETE</td><td>/webproxy/cname/*</td><td>HTTP DELETE request is passed to target, identified by cname for URL given after /cname/</td>
  </tr>
  <tr>
    <td>PUT</td><td>/webproxy/cname/*</td><td>HTTP PUT request is passed to targer, identified by by cname for the URL provided after /cname/</td>
  </tr>

</table>

In all the above API's the response from target is passed back to the original caller.


*Webproxy API*
==============

 Get response from the system identified by cname
--------------

    Verb   URI                     Description
    GET	   /webproxy/cname/*	Lists summary of services configured in VCG identified by service ID.


Note: The request does not require a message body.
Success: Returns JSON data with list of services installed on VCG. Each service is identified by service ID

The service ID is generated is a UUID.

Service Family is the generic service type while name is the actual service name.

pkgurl: The package download link provided to VCG

api: Supported APIs for this service.

*Note: Currently no validation of the package contents done*

*TODO: Caller to provide md5sum of the package along with pkgurl*


**Example Request and Response**

*Request*

    GET /services

*Response*

```
{
    "services": 
    [
        {
            "id": "40860f06-7dcf-41ab-a414-98957b092b7b",
            "status": "installed"
            "api": "/dhcp",
			"description": {
				 "name": "udhcpd",
            	 "family": "dhcp",
			     "version": "1.0",
            	 "pkgurl": "http://my-url.com/udhcpd-0.0.1.deb"
			}
        }
    ]
}
```

Create Service
---------------


