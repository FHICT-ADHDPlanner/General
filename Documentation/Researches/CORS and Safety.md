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
| <b>(2)</b> What are the safety issues with allowing all CORS communication? | Internet-research/Expert interviews|
| <b>(3)</b> How can a developer only let certain CORS communication through? | Internet-research/Expert interviews |

### **Instruments**
Instruments are used to manage and conduct the research. In this research only the following instrument will be used:
- ADHD-planner application

This applicationwill be used as an example project where CORS will be used. 

### **Limitations**
The one limitation that this research has is that it will be limited to the type of application, in this case: React and ASP.NET applications. This might mean that the research will not be as usefull for everyone as the CORS methods might differ between application types.

## **Results**
> ### What is CORS?
CORS, also known as **C**ross-**O**rigin **R**esource **S**haring, enables web pages to request resources from domains other than the one they were initially served from. It operates through an HTTP-header based mechanism, allowing servers to specify which origins, apart from their own, are authorized to load resources. The implementation of CORS relies on a preflight mechanism within web browsers. Before making the actual request, the browser sends a preflight request to the server hosting the cross-origin resource, verifying if the server allows the intended request. During this preflight, the browser includes headers indicating the intended HTTP method and request headers for the actual request. *https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS*

Some requests do not trigger a preflight. These request are called simple requests. This type of request has to meet the following criteria:
> - Apart from the headers automatically set by the user agent, the only headers which are allowed to be manually set are those which the Fetch spec defines as a CORS-safelisted request-header.
> - The only type/subtype combinations allowed for the media type specified in the Content-Type header are: application/x-www-form-urlencoded, multipart/form-data, text/plain.
> > Taken from mdn web docs at [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)


CORS is a mechanism implemented in web browsers that allows regulated access to resources from domains other than the one originally accessed. It expands and enhances the **s**ame-**o**rigin **p**olicy (SOP) by introducing more flexibility. Nonetheless, if the CORS policy of a website is misconfigured or inadequately implemented, it can introduce vulnerabilities for cross-domain attacks. It's important to note that while CORS provides protection against certain security risks, it does not guard against cross-origin attacks like **c**ross-**s**ite **r**equest forgery (CSRF). *https://portswigger.net/web-security/cors*


CORS vulnerabilities primarily occur due to misconfigurations, making prevention a matter of proper configuration. To avoid CORS vulnerabilities, it is recommended to:

> - Do not whitelisting null.
> - Define CORS headers correctly by considering trusted origins for both private and public servers.
> - Maintain additional safeguards for sensitive data, such as authentication and session management, alongside appropriately configured CORS. *https://portswigger.net/web-security/cors*



> ### What are the safety issues with allowing all CORS communication


> ### How can a developer only let certain CORS communication through?


