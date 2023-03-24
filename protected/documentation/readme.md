# VIES

Original WSDL URL: http://ec.europa.eu/taxation_customs/euVies/checkVatService.wsdl

EU initiative to let people resolve EU-based VAT numbers to validate them. A manual interface can be found here: https://ec.europa.eu/taxation_customs/euVies/#/vat-validation

It does not appear that there are pricing tiers or access restrictions, but the server is known to be slow to respond sometimes and can even return fault strings that point to too many concurrent connections globally or per country (rather than per user). Additionally, by default the call will be layered over HTTP.

So use with caution.

For completeness, here is the documentation that is available in the wsdl itself, I have not yet found further documentation on this service. Note that you should be able to mail them on taxud-viesweb@ec.europa.eu for more information.

```
The objective of this Internet site is to allow persons involved in the intra-Community supply of goods or of services to obtain confirmation of the validity of the VAT identification number of any specified person, in accordance to article 31 of Council Regulation (EC) No. 904/2010 of 7 October 2010.
Any other use and any extraction and use of the data which is not in conformity with the objective of this site is strictly forbidden. 
Any retransmission of the contents of this site, whether for a commercial purpose or otherwise, as well as any more general use other than as far as is necessary to support the activity of a legitimate user (for example: to draw up their own invoices) is expressly forbidden. In addition, any copying or reproduction of the contents of this site is strictly forbidden. 
The European Commission maintains this website to enhance the access by taxable persons making intra-Community supplies to verification of their customers' VAT identification numbers. Our goal is to supply instantaneous and accurate information. 
However the Commission accepts no responsibility or liability whatsoever with regard to the information obtained using this site. This information: 
- is obtained from Member States' databases over which the Commission services have no control and for which the Commission assumes no responsibility; it is the responsibility of the Member States to keep their databases complete, accurate and up to date; 
- is not professional or legal advice (if you need specific advice, you should always consult a suitably qualified professional); 
- does not in itself give a right to exempt intra-Community supplies from Value Added Tax; 
- does not change any obligations imposed on taxable persons in relation to intra-Community supplies. 
It is our goal to minimise disruption caused by technical errors. However some data or information on our site may have been created or structured in files or formats which are not error-free and we cannot guarantee that our service will not be interrupted or otherwise affected by such problems. The Commission accepts no responsibility with regard to such problems incurred as a result of using this site or any linked external sites. 
This disclaimer is not intended to limit the liability of the Commission in contravention of any requirements laid down in applicable national law nor to exclude its liability for matters which may not be excluded under that law. 
Collecting or handling personal data falls under the Data Protection Notice. This data protection declaration explains the Processing in the VIES-on-the-web Internet Website of VAT Identification Numbers for intra-Community Transaction on Goods or Services. Details of your legal rights associated with the collection, processing and use of this data are also provided: http://ec.europa.eu/dpo-register/details.htm?id=40647 . 

Usage: 
The countryCode input parameter must follow the pattern [A-Z]{2} 
The vatNumber input parameter must follow the pattern [0-9A-Za-z\+\*\.]{2,12} 
In case of problems, the returned FaultString can take the following specific values: 
- INVALID_INPUT: The provided CountryCode is invalid or the VAT number is empty; 
- GLOBAL_MAX_CONCURRENT_REQ: Your Request for VAT validation has not been processed; the maximum number of concurrent requests has been reached. Please re-submit your request later or contact TAXUD-VIESWEB@ec.europa.eu for further information": Your request cannot be processed due to high traffic on the web application. Please try again later; 
- MS_MAX_CONCURRENT_REQ: Your Request for VAT validation has not been processed; the maximum number of concurrent requests for this Member State has been reached. Please re-submit your request later or contact TAXUD-VIESWEB@ec.europa.eu for further information": Your request cannot be processed due to high traffic towards the Member State you are trying to reach. Please try again later. 
- SERVICE_UNAVAILABLE: an error was encountered either at the network level or the Web application level, try again later; 
- MS_UNAVAILABLE: The application at the Member State is not replying or not available. Please refer to the Technical Information page to check the status of the requested Member State, try again later; 
- TIMEOUT: The application did not receive a reply within the allocated time period, try again later. 
```

One comment pointed out (https://stackoverflow.com/questions/9158119/euVies-vat-number-validation):

```
You might expect this SOAP interface to just check a central database of VAT numbers but that doesn't exist. Every country manages its own database and the European Commission is just dispatching queries. The queries don't even stay on web services all the way, they're carried over a legacy Customs network (CCN/CSI) and the remote system can be really awful in some countries. It even happens that an entire country drops out of the system for days or even weeks !
```

The REST service that has been added seems to be the service they themselves use in the frontend. It is supposed to be slightly more stable though untested as of yet. Because it is not part of any official documentation it is unclear whether or not it will work in the long run.