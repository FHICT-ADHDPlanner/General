# CORS and Safety
## Table of contents
- [CORS and Safety](#cors-and-safety)
  - [Table of contents](#table-of-contents)
  - [**Introduction**](#introduction)
  - [**Methodology**](#methodology)
    - [**Research Strategies**](#research-strategies)
    - [**Instruments**](#instruments)
    - [**Limitations**](#limitations)
  - [**Results**](#results)
  - [**Sources**](#sources)


## **Introduction**
**C**ross-**O**rigin **R**esource **S**haring (CORS) is a vital part in any web based application. As it is such an important part, this research will be focussing on what CORS is and how it impacts the safety of applications.

The topic of this research was sparked by issues within my individual project, ADHD-planner. While connecting the React Typescript frontend to the C# backend, issues came up regarding CORS and the connection it made. Since this is a vital part of the application made, it was decided that it would make a good research topic.

## **Methodology**
This research will take a better look into CORS. The main research question that will be answered is as follows:
>How can a developer safely use CORS in their web application?

To help answer this question, it has been split into multiple sub questions:

1. What is CORS?
2. What are the safety issues with allowing all CORS communication?
3. How can a developer only let certain CORS communication through?

### **Research Strategies**
The research will be conducted using the DOT (**D**evelopment **O**riented **T**riangulation) framework. For the questions, the following research strategies will be used:
| Research Question | Research Strategy |
| --- | --- |
| <b>(1)</b> What is CORS? | Internet-research |
| <b>(2)</b> What are the safety issues with allowing all CORS communication? | Internet-research|
| <b>(3)</b> How can a developer only let certain CORS communication through? | Internet-research |

### **Instruments**
Instruments are used to manage and conduct the research. In this research only the following instrument will be used:
- ADHD-planner application

This application will be used as an example project where CORS will be used. 

### **Limitations**
The one limitation that this research has is that it will be limited to the type of application, in this case: React and ASP.NET applications. This might mean that the research will not be as useful for everyone as the CORS methods might differ between application types.

## **Results**
> ### What is CORS?
CORS, also known as **C**ross-**O**rigin **R**esource **S**haring, enables web pages to request resources from domains other than the one they were initially served from. It operates through an HTTP-header based mechanism, allowing servers to specify which origins, apart from their own, are authorized to load resources. The implementation of CORS relies on a preflight mechanism within web browsers. Before making the actual request, the browser sends a preflight request to the server hosting the cross-origin resource, verifying if the server allows the intended request. During this preflight, the browser includes headers indicating the intended HTTP method and request headers for the actual request *(Cross-Origin Resource Sharing (CORS) - HTTP | MDN, 2023)*.

Some requests do not trigger a preflight. These request are called simple requests. This type of request has to meet the following criteria:
> - Apart from the headers automatically set by the user agent, the only headers which are allowed to be manually set are those which the Fetch spec defines as a CORS-safelisted request-header.
> - The only type/subtype combinations allowed for the media type specified in the Content-Type header are: application/x-www-form-urlencoded, multipart/form-data, text/plain.
> > Taken from mdn web docs at [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)


CORS is a mechanism implemented in web browsers that allows regulated access to resources from domains other than the one originally accessed. It expands and enhances the **s**ame-**o**rigin **p**olicy (SOP) by introducing more flexibility. Nonetheless, if the CORS policy of a website is misconfigured or inadequately implemented, it can introduce vulnerabilities for cross-domain attacks. It's important to note that while CORS provides protection against certain security risks, it does not guard against cross-origin attacks like **c**ross-**s**ite **r**equest forgery (CSRF) *(What Is CORS (Cross-origin Resource Sharing)? Tutorial & Examples | Web Security Academy, n.d.)*.


CORS vulnerabilities primarily occur due to misconfigurations, making prevention a matter of proper configuration. To avoid CORS vulnerabilities, it is recommended to:

> - Do not whitelisting null.
> - Define CORS headers correctly by considering trusted origins for both private and public servers.
> - Maintain additional safeguards for sensitive data, such as authentication and session management, alongside appropriately configured CORS *(What Is CORS (Cross-origin Resource Sharing)? Tutorial & Examples | Web Security Academy, n.d.-b)*.



> ### What are the safety issues with allowing all CORS communication?

As mentioned before CORS can have major safety issues. This is mainly due to allowing all CORS communication in the web applications. Some of the main risks are:
- Leaking sensitive data
  > When CORS is misconfigured, it can lead to the leakage of sensitive data. For example, API keys and user information. An example of this is if the Access-Control-Allow-Origin header is set to * (All), it allows any origin to access the resources within. This an potentially expose sensitive data to unauthorized parties *(Pathak, 2021)*.
- Cross-communication attacks:
  > Misconfiguration can allow any attackers to gain access to sites behind the firewall using cross-communication types of attacks. This vulnerability can be exploited by an attacker by having a CORS-vulnerable intranet site open in one browser tab and accessing a malicious external site in another tab *(Barrus, 2023)*.
- Deceptive requests:
  > Next to cross-communication attacks, attackers can also make deceptive requests to vulnerable servers by using the browser as a proxy to make resource requests. The result of this can be unauthorized access Internal resources *(Barrus, 2023)*.
- Downgrade attacks:
  > If an app that uses HTTPS whitelists a domain that is using HTTP, with Access-Control-Allow-Origin = * and Access-Control-Allow-Credentials = TRUE, traffic can be intercepted over deprecated TLS protocols. The session token can be stolen this way and unauthorized access to the application *(Barrus, 2023)*.


> ### How can a developer only let certain CORS communication through?
For each type of development, there is also a way to enable CORS to only let certain communication through. 

**Node.js + Express.js**

For Node.js, it is possible to use the CORS middleware from npm to configure it. For example, allowing only GET requests from your own website with headers Content-Type and Authorization with a 10 minute preflight cache time. 
```
const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors({
  origin: 'https://yourwebsite.com',
  methods: ['GET'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  maxAge: 600
}));

app.get('/', (req, res) => {
  res.send('API running with CORS enabled');
});

app.listen(5000, console.log('Server running on port 5000'));
```
*(Ranganath, 2021)*

**ASP.NET Core**

In ASP.NET Core, there is a method to use called AddCors. To allow specific headers in this CORS request, call WithHeaders and specify the allowed headers
```
using Microsoft.Net.Http.Headers;

var MyAllowSpecificOrigins = "_MyAllowSubdomainPolicy";
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddCors(options =>
{
    options.AddPolicy(name: MyAllowSpecificOrigins,
        policy =>
        {
            policy.WithOrigins("http://example.com")
                    .WithHeaders(HeaderNames.ContentType, "x-custom-header");
        });
});
builder.Services.AddControllers();
var app = builder.Build();
```
*(Tdykstra, 2023)*

**API Gateway**

For an API Gateway, it works a little differently. In this case, it would have to be done through the console or the Cloudformation. For example, a script can be created to call the AWS REST API and deploy it to a private VM. To test the behavior of the API, the script can be accessed through a private IP address. This can be done with CORS enabled and disabled *(Hemnanirohan, 2022)*.

## **Sources**
Barrus, R. (2023). How to Avoid CORS Security Issues in 2021 | Cross-Origin Resource Sharing | Pivot Point Security. Pivot Point Security. https://www.pivotpointsecurity.com/cross-origin-resource-sharing-secu 

Cross-Origin Resource Sharing (CORS) - HTTP | MDN. (2023, May 10). https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

Hemnanirohan. (2022, January 6). Simple steps to enable CORS in API Gateway through console/cloud formation. Medium. https://medium.com/geekculture/simple-steps-to-enable-cors-in-api-gateway-through-console-cloud-formation-c09d9df31c07
 
Pathak, A. (2021, December 12). Security Risks of CORS - Ayush Pathak - Medium. Medium. https://medium.com/@ehayushpathak/security-risks-of-cors-e3f4a25c04d7 

Ranganath, N. (2021, June 11). The ultimate guide to enabling Cross-Origin Resource Sharing (CORS) - LogRocket Blog. LogRocket Blog. https://blog.logrocket.com/the-ultimate-guide-to-enabling-cross-origin-resource-sharing-cors/ 

Tdykstra. (2023, March 24). Enable Cross-Origin Requests (CORS) in ASP.NET Core. Microsoft Learn. https://learn.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-7.0 

What is CORS (cross-origin resource sharing)? Tutorial & Examples | Web Security Academy. (n.d.-a). https://portswigger.net/web-security/cors 
