#Available SOAP Web Services  

The HotSchedules SOAP API provides a user-friendly way to obtain HS Data. Each service contains a **sayHello** call, a test method intended to be used to validate access to the service. It returns a text message indicating success.

**[CertificationService](#certificationservice):** This service is intended for third parties to be able to request and set certification requests from HotSchedules.
<br>

**[EmpService](#empservice)** This service provides operations for a third party to push or request employee and employee job data into HotSchedules.
<br>

**[LaborService](#laborservice):** This service is intended for third parties to be able to request labor data from HotSchedules and import it into their POS/data warehouse/enterprise/etc.
<br>

**[OperatingBudgetPlanService](#operatingbudgetplanservice):** Allows a customer to SET their budget via API. The service also allow a customer to GET their labor budget data.
<br>

**[ProjectedSalesService](#projectedsalesservice):** This service is intended for third parties to be able to grab projected sales data from HotSchedules and import it into their POS/data warehouse/enterprise/etc.
<br>

**[SalesService](#salesservice):** This service is intended for third parties to be able to import their sales items into the HotSchedules system in a straightforward fashion. Currently there is only one method for setting sales items.
<br>

**[ScheduleService](#scheduleservice):** This service is intended for third parties to be able to grab scheduled shifts from HotSchedules and import them into their POS/data warehouse/enterprise/etc.
<br>

**[TimeCardService](#timecardservice):** This service is intended for third parties to be able to import their time cards into the HotSchedules system or get time cards from HotSchedules in a straightforward fashion.
<br>

**[TimeOffService](#timeoffservice):** This service is intended for third parties to be able to request approved timeoff requests from HotSchedules.
<br>

**[VolumeService](#volumeservice):** This service is intended for third parties to be able to request and send volume driver related data from/to HotSchedules. Driver items include examples such as guests, tables, entrees…. Etc. 

##CertificationService

This service is intended for third parties to be able to request and set certification requests from HotSchedules.

* Location: [http://services.hotschedules.com/api/services/CertificationService?wsdl](http://services.hotschedules.com/api/services/CertificationService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getClientCertifications:** This method takes in a concept ID and a store ID and returns an array of certification objects. It is meant to get a list of all certifications for that store.
<br>
- **getEmployeeCertifications:** This method takes in a concept ID, store ID and employee POS ID and returns an array of employee certificate objects. It is meant to get a list of all employee certification information for an employee for that store.
<br>
- **removeEmployeeCertifications:** This method takes in a concept ID and a store ID. It is meant to get allow you to remove certifications from a specified employee for that store.
<br>
- **setEmployeeCertiﬁcations:** This method takes in a concept ID, store ID. It is meant to set certifications from a specified employee for that store.

####getClientCertifications

This method takes in a concept ID and a store ID and returns client certification objects. It is meant to get a list of all certifications for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:cer="http://services.hotschedules.com/api/services/CertificationService">
   <soapenv:Header/>
   <soapenv:Body>
      <cer:getClientCertifications>
         <concept>1</concept>
         <storeNum>55</storeNum>
      </cer:getClientCertifications>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getClientCertificationsResponse xmlns:ns1="http://services.hotschedules.com/api/services/CertificationService">
         <return>
            <item>
               <certExtRef>-1</certExtRef>
               <certName>Team Member Alcohol Cert</certName>
               <certType>2</certType>
               <certTypeDescription>Expires Without AutoInactivation</certTypeDescription>
               <groupLevel>false</groupLevel>
            </item>
            <item>
               <certExtRef>-1</certExtRef>
               <certName>Alcohol Certification</certName>
               <certType>1</certType>
               <certTypeDescription>Expires With AutoInactivation</certTypeDescription>
               <groupLevel>false</groupLevel>
            </item>
         </return>
      </ns1:getClientCertificationsResponse>
   </soap:Body>
</soap:Envelope>
```

####getEmployeeCertifications

This method takes in a concept ID, store ID and employee POS ID and returns an array of employee certificate objects. It is meant to get a list of all employee certification information for an employee for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
<tr>
<td>empPOSId</td>
<td>Int</td>
<td>1..1</td>
<td>POS numeric employee ID.</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/CertificationService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262747932814">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">9iOMGex3ZDEpdw4xsAweWA==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T19:37:59.328Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <cer:getEmployeeCertifications>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                                  <empPosId>100</empPosId>
                      </cer:getEmployeeCertifications>
          </soapenv:Body>
</soapenv:Envelope>
 
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:getEmployeeCertificationsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/CertificationService">
                                  <return>
                                              <item>
                                                          <certExtRef>•1</certExtRef>
                                                          <certName>21 Day Certification</certName>
                                                          <certType>2</certType>
                                                          <certTypeDescription>Expires Without AutoInactivation</certTypeDescription>
                                                          <groupLevel>true</groupLevel>
                                                          <empPosId>100</empPosId>
                                                          <expirationDate>2016•11•30T00:00:00•06:00</expirationDate>
                                              </item>
                                  </return>
                      </ns1:getEmployeeCertificationsResponse>
          </soap:Body>
</soap:Envelope>
```
####setEmployeeCertifications

This method takes in a concept ID, store ID. It is meant to set certifications from a specified employee for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/CertificationService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262747932814">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">9iOMGex3ZDEpdw4xsAweWA==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T19:37:59.328Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <cer:setEmployeeCertifications>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                                  <certs>
                                              <item>
                                                          <certExtRef>500</certExtRef>
                                                          <certName>Laura Test</certName>
                                                          <certType>0</certType>
                                                          <certTypeDescription>Testingnewcert</certTypeDescription>
                                                          <groupLevel>1</groupLevel>
                                                          <empPosId>100</empPosId>
                                                          <expirationDate>?</expirationDate>
                                              </item>
                                  </certs>
                      </cer:setEmployeeCertifications>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:removeEmployeeCertificationsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/CertificationService">
                                  <return>
                                              <failCount>0</failCount>
                                              <success>true</success>
                                              <successCount>1</successCount>
                                  </return>
                      </ns1:removeEmployeeCertificationsResponse>
          </soap:Body>
</soap:Envelope>
```
####removeEmployeeCertifications

This method takes in a concept ID and a store ID. It is meant to get allow you to remove certifications from a specified employee for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/CertificationService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262747932814">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">9iOMGex3ZDEpdw4xsAweWA==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T19:37:59.328Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <cer:removeEmployeeCertifications>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                                  <certs>
                                              <item>
                                                          <certExtRef>200</certExtRef>
                                                          <certName>21 Day Certification</certName>
                                                          <certType>2</certType>
                                                          <certTypeDescription>Expires Without AutoInactivation</certTypeDescription>
                                                          <groupLevel>true</groupLevel>
                                                          <empPosId>100</empPosId>
                                                          <expirationDate>2016•11•30T00:00:00•06:00</expirationDate>
                                              </item>
                                  </certs>
                      </cer:removeEmployeeCertifications>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:setEmployeeCertificationsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/CertificationService">
                                  <return>
                                              <failCount>0</failCount>
                                              <success>true</success>
                                              <successCount>1</successCount>
                                  </return>
                      </ns1:setEmployeeCertificationsResponse>
          </soap:Body>
</soap:Envelope>
```
##EmpService

This service provides operations for a third party to push or request employee and employee job data into HotSchedules.

* Location: http://services.hotschedules.com/api/services/CertificationService?wsdl
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>

- **getEmpAvailability:** This method takes in a concept ID and a store ID and returns an array of wsEmpAvailability objects. It is meant to get a list of all availability for that store.
<br>
- **getEmpInfo:** This method takes in a concept ID and a store ID and returns an array of wsEmpInfo objects. It is meant to get a list of all employees for that store.
<br>
- **getEmpJobs:** This method takes in a concept ID and a store ID and returns an array of wsEmpJob objects. It is meant to get a list of all jobs assigned to all employees for that store.
<br>
- **getStoreEmployees:** This method takes in a concept ID, store ID, a flag to determine if only active employees are returned, and returns an array of WSEmployee objects.
<br>
- **getStoreJobs:** This method takes in a concept ID and a store ID, and returns an array of all jobs currently defined in HotSchedules for the given concept/store.
<br>
- **setEmpJobs:** This method takes in a concept ID, store ID, and an array of WSEmpJob objects to assign jobs to individual employees. This method returns a WSReturn object.
<br>
- **setEmps:** This method takes in a concept ID, store ID and an array of WSEmployee objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array of employees will be parsed on the server side to employees who need to be inserted or updated in the HS database. This method returns a WSReturn object.

####getStoreEmployees

This method takes in a concept ID, store ID, a flag to determine if only active employees are returned, and returns an array of WSEmployee objects.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>boolean</td>
<td>1..1</td>
<td>Boolean that defines whether or not to include terminated employees in response.
</td>
</tr>
<tr>
<td>activeOnly</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsEmployeeArray</td>
<td>1..1</td>
<td>Array of WSEmployee objects.
</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3009<br>API_EMP_PERMISSION_GET_STORE_EMPS<br>client not found
</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:emp="http://services.hotschedules.com/api/services/EmpService">
   <soapenv:Header/>
   <soapenv:Body>
      <emp:getStoreEmployees>
         <concept>1</concept>
         <storeNum>55</storeNum>
         <activeOnly>Y</activeOnly>
      </emp:getStoreEmployees>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getStoreEmployeesResponse xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
         <return>
            <item>
               <address>6504 Bridgepoint Pkwy #425</address>
               <address2/>
               <altId>-1</altId>
               <city>Austin</city>
               <clientId>17638840</clientId>
               <email/>
               <empNum>-1</empNum>
               <FName>HotSchedules</FName>
               <hsId>12262906</hsId>
               <LName>Support</LName>
               <mobile/>
               <NName/>
               <phone>(512) 123-4567</phone>
               <state>TX</state>
               <status>1</status>
               <storeNum>23</storeNum>
               <zipCode>78730</zipCode>
               <dob>2000-02-01T00:00:00-06:00</dob>
               <hireDate>2015-02-09T12:40:09.733-06:00</hireDate>
            </item>
            </return>
      </ns1:getStoreEmployeesResponse>
   </soap:Body>
</soap:Envelope>
```

####getEmpAvailability

This method takes in a concept ID and a store ID and returns an array of wsEmpAvailability objects. It is meant to get a list of all employee availability for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
<tr>
<td>activeOnly</td>
<td>bolean</td>
<td>1..1</td>
<td>Boolean that defines whether or not to include terminated employees in response.
</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsEmpAvailabilityArray</td>
<td>1..1</td>
<td>Array of wsEmpAvailability objects, which describes all jobs assigned to all active employees for that store.</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3021<br>API_EMP_PERMISSION_GET_EMP_AVAIL<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/EmpService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262747932814">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">9iOMGex3ZDEpdw4xsAweWA==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T19:37:59.328Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <emp:getEmpAvailability>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                                  <activeOnly>true</activeOnly>
                      </emp:getEmpAvailability>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:getEmpAvailabilityResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
                                  <return>
                                              <item>
                                                          <availabilities>
                                                                      <dayName>Sunday</dayName>
                                                                      <dayNum>1</dayNum>
                                                                      <parHoursMax>•1</parHoursMax>
                                                                      <parHoursMin>•1</parHoursMin>
                                                                      <parShiftsMax>•1</parShiftsMax>
                                                                      <parShiftsMin>•1</parShiftsMin>
                                                                      <partialBeforeAfter>After</partialBeforeAfter>
                                                                      <partialTime>11:45</partialTime>
                                                                      <shiftId>964362624</shiftId>
                                                                      <shiftName>Breakfast</shiftName>
                                                                      <statusName>Partially Available</statusName>
                                                                      <statusNum>1</statusNum>
                                                          </availabilities>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                              </item>
                                  </return>
                      </ns1:getEmpAvailabilityResponse>
          </soap:Body>
</soap:Envelope>
```

####getStoreJobs

This method takes in a concept ID and a store ID, and returns an array of all jobs currently defined in HotSchedules for the given concept/store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsJobArray</td>
<td>1..1</td>
<td>WSJob object</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3010<br>API_EMP_PERMISSION_GET_STORE_JOBS<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:emp="http://services.hotschedules.com/api/services/EmpService">
   <soapenv:Header/>
   <soapenv:Body>
      <emp:getStoreJobs>
         <concept>1</concept>
         <storeNum>32</storeNum>
      </emp:getStoreJobs>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getStoreJobsResponse xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
         <return>
            <item>
               <clientId>12316576</clientId>
               <defRate>1.0</defRate>
               <hsId>1236319092</hsId>
               <jobName>ATO</jobName>
               <posId>99</posId>
               <storeNum>32</storeNum>
            </item>
            </return>
      </ns1:getStoreJobsResponse>
   </soap:Body>
</soap:Envelope>
```


####getEmpInfo

This method takes in a concept ID and a store ID and returns an array of wsEmpInfo objects. It is meant to get a list of all employees assigned to a schedule for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
<tr>
<td>activeOnly</td>
<td>boolean</td>
<td>1..1</td>
<td>Boolean that defines whether or not to include terminated employees in response.</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsEmpInfoArray</td>
<td>1..1</td>
<td>Array of wsEmpInfo objects, which describes all jobs assigned to all active employees for that store.</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3020<br>API_EMP_PERMISSION_GET_EMP_INFO<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/EmpService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262475127713">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">deQn1F/GUBV/fMNJ7pdatA==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T18:52:31.276Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <emp:getEmpInfo>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                                  <activeOnly>true</activeOnly>
                      </emp:getEmpInfo>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soap:Envelope>
      <soap:Body>
                  <ns1:getEmpInfoResponse
                              xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
                              <return>
                                          <item>
                                                      <accountCreated>2015•11•04T10:54:22.807•06:00</accountCreated>
                                                      <assignedSchedules>
                                                                  <extId>0</extId>
                                                                  <hsId>964330043</hsId>
                                                                  <name>Kitchen</name>
                                                      </assignedSchedules>
                                                      <assignedSchedules>
                                                                  <extId>•1</extId>
                                                                  <hsId>964318722</hsId>
                                                                  <name>Meetings</name>
                                                      </assignedSchedules>
                                                      <assignedSchedules>
                                                                  <extId>0</extId>
                                                                  <hsId>964330041</hsId>
                                                                  <name>Team Member</name>
                                                      </assignedSchedules>
                                                      <empHrId>•1</empHrId>
                                                      <empNum>1</empNum>
                                                      <lastUpdated>2015•11•09T10:29:31.123•06:00</lastUpdated>
                                                      <permissionSetName>Employee</permissionSetName>
                                          </item>
                                          <item>
                                                      <accountCreated>2015•11•04T08:33:41.090•06:00</accountCreated>
                                                      <empHrId>•1</empHrId>
                                                      <empNum>•1</empNum>
                                                      <permissionSetName>HS ASC Support</permissionSetName>
                                          </item>
                                          <item>
                                                      <accountCreated>2015•11•04T08:42:02.483•06:00</accountCreated>
                                                      <empHrId>•1</empHrId>
                                                      <empNum>•1</empNum>
                                                      <lastUpdated>2015•11•05T18:29:55.857•06:00</lastUpdated>
                                                      <permissionSetName>Admin ALL</permissionSetName>
                                          </item>
                                          <item>
                                                      <accountCreated>2015•11•04T08:49:32.623•06:00</accountCreated>
                                                      <empHrId>•1</empHrId>
                                                      <empNum>•1</empNum>
                                                      <lastUpdated>2015•11•04T08:49:33.120•06:00</lastUpdated>
                                                      <permissionSetName>Default HS Support User</permissionSetName>
                                          </item>
                                          <item>
                                                      <accountCreated>2015•11•04T08:49:33.887•06:00</accountCreated>
                                                      <empHrId>•1</empHrId>
                                                      <empNum>•1</empNum>
                                                      <lastUpdated>2015•11•04T08:49:34.093•06:00</lastUpdated>
                                                      <permissionSetName>Default HotSchedules Employee</permissionSetName>
                                          </item>
                              </return>
                  </ns1:getEmpInfoResponse>
      </soap:Body>
</soap:Envelope>
```


####getEmpJobs

This method takes in a concept ID and a store ID and returns an array of wsEmpJob objects. It is meant to get a list of all jobs assigned to all employees for that store.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsEmpJobArray</td>
<td>1..1</td>
<td>Array of wsEmpJob objects, which describes all jobs assigned to all active employees for that store.</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3014<br>API_EMP_PERMISSION_GET_EMP_JOBS<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:emp="http://services.hotschedules.com/api/services/EmpService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•63A716DE011BE2D649145262410123010">
                                              <wsse:Username>laura1234!</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">laura 1234!</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">cZvq5MrVptRUWgLIIqmYRg==</wsse:Nonce>
                                              <wsu:Created>2016•01•12T18:41:41.230Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <emp:getEmpJobs>
                                  <concept>1</concept>
                                  <storeNum>1</storeNum>
                      </emp:getEmpJobs>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope>
          <soap:Body>
                      <ns1:getEmpJobsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
                                  <return>
                                              <item>
                                                          <clientId>19054117</clientId>
                                                          <hsEmpId>17896647</hsEmpId>
                                                          <hsJobId>27229283</hsJobId>
                                                          <ovtWage>14.25</ovtWage>
                                                          <posEmpId>1</posEmpId>
                                                          <posJobId>•1</posJobId>
                                                          <primary>true</primary>
                                                          <regWage>9.5</regWage>
                                                          <storeNum>1</storeNum>
                                              </item>
                                              <item>
                                                          <clientId>19054117</clientId>
                                                          <hsEmpId>17896647</hsEmpId>
                                                          <hsJobId>27229285</hsJobId>
                                                          <ovtWage>11.25</ovtWage>
                                                          <posEmpId>1</posEmpId>
                                                          <posJobId>•1</posJobId>
                                                          <primary>false</primary>
                                                          <regWage>7.5</regWage>
                                                          <storeNum>1</storeNum>
                                              </item>
                                  </return>
                      </ns1:getEmpJobsResponse>
          </soap:Body>
</soap:Envelope>
```


####setEmps

This method takes in a concept ID, store ID and an array of WSEmployee objects. Using the authentication from the username token and the conecpt and store IDs, the server will resolve which HotSchedules client this sync is for. The array of employees will be parsed on the server side to employees who need to be inserted or updated in the HS database. This method returns a WSReturn object.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
<tr>
<td>emps</td>
<td>wsEmployeeArray</td>
<td>1..1</td>
<td>Array of WSEmployee objects. Each object represents an employee at this store.</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>1..1</td>
<td>WSReturn object</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3007<br>API_EMP_PERMISSION_SET_EMPS<br>client not found
</td>
</tr>
</tbody>
</table>

**WSReturn object**

<table>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>dataEmpJob</td>
<td>Employee job object. Contains job information (job code, regular and OT rates, primary flag) for a given employee job.</td>
</tr>
<tr>
<td>dataEmployee</td>
<td>Employee information object. Contains employee information (name, address, phone info, active/terminated status).</td>
</tr>
<tr>
<td>dataJob</td>
<td>General job information object. Contains job information (job code, job name, default rate).</td>
</tr>
<tr>
<td>wsEmpJob</td>
<td>Extends dataEmpJob.</td>
</tr>
<tr>
<td>wsEmployee</td>
<td>Extends dataEmployee (contains DOB, hire date, termination date).</td>
</tr>
<tr>
<td>wsJob</td>
<td>Extends dataJob.</td>
</tr>
<tr>
<td>wsReturn</td>
<td>Contains array of error strings, fail count, success flag, success count.</td>
</tr>
</tbody>
</table>

**Array EmpJobs**
Employee job object. Contains job information (job code, regular and OT rates, primary flag) for a given employee job.

**Derived By**
Restricting anyType

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<tr><td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>hsEmpId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID</td></tr>
<td>hsJobId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal job code ID</td></tr>
<td>ovtWage</td><td>float</td><td>1..1</td><td>No</td><td>Overtime hourly wage rate for employee</td></tr>
<td>posEmpId</td><td>int</td><td>1..1</td><td>No</td><td>POS numeric ID for employee</td></tr>
<td>posJobId</td><td>int</td><td>1..1</td><td>No</td><td>POS numeric ID for the job code</td></tr>
<td>primary</td><td>boolean</td><td>1..1</td><td>No</td><td>Boolean flag to designate if the job code is the primary job for the employee</td></tr>
<td>regWage</td><td>float</td><td>1..1</td><td>No</td><td>Regular hourly wage rate for employee</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally, set up to mirror the client internal store IDs.</td></tr>
<td>date</td><td>dateTime</td><td>0..1</td><td>No</td><td>Date job was added for the employee</td></tr>
</tbody>
</table>

**Referenced By**
Complex Type wsEmpJob

**Emp Array**
Employee information object. Contains employee information (name, address, phone info, active/terminated status)

**Derived By**
Restricting anyType

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>address</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Address line 1</td></tr>
<td>address2</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Address line 2</td></tr>
<td>altId</td><td>int</td><td>1..1</td><td>No</td><td>Alternative ID for employee generally reserved for the HR ID.</td></tr>
<td>city</td><td>string</td><td>0..1</td><td>No</td><td>City field for Address</td></tr>
<td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>email</td><td>string</td><td>0..1</td><td>No</td><td>Employee’s email address</td></tr>
<td>empNum</td><td>int</td><td>1..1</td><td>No</td><td>Employee POS ID</td></tr>
<td>FName</td><td>string</td><td>0..1</td><td>No</td><td>Employee First Name</td></tr>
<td>hsId</td><td>int</td><td>1..1</td><td>No</td><td>Optional•HotSchedule unique employee account ID</td></tr>
<td>LName</td><td>string</td><td>0..1</td><td>No</td><td>Employee Last Name</td></tr>
<td>mobile</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employees Mobile Phone Number</td></tr>
<td>NName</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Nick Name</td></tr>
<td>phone</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee phone number</td></tr>
<td>state</td><td>string</td><td>0..1</td><td>No</td><td>State field for Address</td></tr>
<td>status</td><td>int</td><td>1..1</td><td>No</td><td>Active = 1, Inactive = 0, Terminated =•1</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.</td></tr>
<td>zipCode</td><td>string</td><td>0..1</td><td>No</td><td>Zip Code from Address</td></tr>
</tbody>
</table>

**Referenced By**
Complex Type wsEmployee

**WSJob Array**
General job information object. Contains job information (job code, job name, default rate).

**Derived By**
Restricting anyType

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>defRate</td><td>float</td><td>1..1</td><td>No</td><td>Default Pay Rate for a Job Code</td></tr>
<td>hsId</td><td>int</td><td>1..1</td><td>No</td><td>Optional•HotSchedules numeric ID for Job Code</td></tr>
<td>jobName</td><td>string</td><td>0..1</td><td>No</td><td>Name for Job Code</td></tr>
<td>posId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric POS ID for Job Code</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.</td></tr>
</tbody>
</table>

**Referenced By**
Complex Type wsJob

**wsEmpJobArray**
Extends dataEmpJob.
 
**Derived By**
Extending dataEmpJob

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>hsEmpId</td><td>int</td><td>1..1</td><td>No</td><td>Optional•HotSchedule unique employee account ID</td></tr>
<td>hsJobId</td><td>int</td><td>1..1</td><td>No</td><td>Optional•HotSchedules internal ID for the Job Code</td></tr>
<td>ovtWage</td><td>float</td><td>1..1</td><td>No</td><td>Overtime hourly wage for job code for the employee</td></tr>
<td>posEmpId</td><td>int</td><td>1..1</td><td>No</td><td>POS numeric identifier for the employee</td></tr>
<td>posJobId</td><td>int</td><td>1..1</td><td>No</td><td>POS numeric identifier for the job</td></tr>
<td>primary</td><td>boolean</td><td>1..1</td><td>No</td><td>Flag to indicate if a job is the primary job for the employee</td></tr>
<td>regWage</td><td>float</td><td>1..1</td><td>No</td><td>Regular hourly wage for the job for the employee</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.</td></tr>
<td>date</td><td>dateTime</td><td>0..1</td><td>No</td><td>Date job was added for the employee</td></tr>
</tbody>
</table>

**Referenced By**
Element item [type wsEmpJobArray]
<br>
Extends dataEmployee (contains DOB, hire date, termination date)

**Derived By**
Extending dataEmployee
 
**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>address</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Address line 1</td></tr>
<td>address2</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Address line 2</td></tr>
<td>altId</td><td>int</td><td>1..1</td><td>No</td><td>Alternative ID for employee generally reserved for the HR ID.</td></tr>
<td>city</td><td>string</td><td>0..1</td><td>No</td><td>City field for Address</td></tr>
<td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>email</td><td>string</td><td>0..1</td><td>No</td><td>Employee’s email address</td></tr>
<td>empNum</td><td>int</td><td>1..1</td><td>No</td><td>Employee POS ID</td></tr>
<td>FName</td><td>string</td><td>0..1</td><td>No</td><td>Employee First Name</td></tr>
<td>hsId</td><td>int</td><td>1..1</td><td>No</td><td>Optional•HotSchedule unique employee account ID</td></tr>
<td>LName</td><td>string</td><td>0..1</td><td>No</td><td>Employee Last Name</td></tr>
<td>mobile</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employees Mobile Phone Number</td></tr>
<td>NName</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee Nick Name</td></tr>
<td>phone</td><td>string</td><td>0..1</td><td>No</td><td>Optional•Employee phone number</td></tr>
<td>state</td><td>string</td><td>0..1</td><td>No</td><td>State field for Address</td></tr>
<td>status</td><td>int</td><td>1..1</td><td>No</td><td>Active = 1, Inactive = 0, Terminated =•1</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.</td></tr>
<td>zipCode</td><td>string</td><td>0..1</td><td>No</td><td>Zip Code from Address</td></tr>
<td>dob</td><td>dateTime</td><td>0..1</td><td>No</td><td>Employee Date of Birth</td></tr>
<td>hireDate</td><td>dateTime</td><td>0..1</td><td>No</td><td>Employee Hire Date</td></tr>
<td>termDate</td><td>dateTime</td><td>0..1</td><td>No</td><td>Employee Termination date. Only required for employees with a status of •1</td></tr>
</tbody>
</table>

**Referenced By**
Element item [type wsEmployeeArray]
Extends dataJob.

**Derived By**
Extending dataJob

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td>defRate</td><td>float</td><td>1..1</td><td>No</td><td>Default Pay Rate for a Job Code</td></tr>
<td>hsId</td><td>int</td><td>1..1</td><td>Yes</td><td>Optional•HotSchedules numeric ID for Job Code</td></tr>
<td>jobName</td><td>string</td><td>0..1</td><td>No</td><td>Name for Job Code</td></tr>
<td>posId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric POS ID for Job Code</td></tr>
<td>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.</td></tr>
</tbody>
</table>

**Referenced By**
Element item [type wsJobArray]
Contains array of error strings, fail count, success flag, success count.

**Derived By**
Restricting anyType

**Content Model**
Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Component</th>
<th>Type</th>
<th>Occurs</th>
<th>Nillable?</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td>errors</td><td>string</td><td>0..*</td><td>Yes</td><td>Description of the error code</td></tr>
<td>failCount</td><td>int</td><td>1..1</td><td>No</td><td>Total number of records that failed to meet basic import specifications</td></tr>
<td>success</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicator of the success or failure</td></tr>
<td>successCount</td><td>int</td><td>1..1</td><td>No</td><td>Total number of records that successfully met basic import specifications</td></tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>address [type dataEmployee]</td><td>Address Line 1</td></tr>
<td nowrap>address2 [type dataEmployee]</td><td>Address Line 2</td></tr>
<td nowrap>altId [type dataEmployee]</td><td>Alternative ID for employee generally reserved for the HR ID.</td></tr>
<td nowrap>city [type dataEmployee]</td><td>City field for Address</td></tr>
<td nowrap>clientId [type dataEmpJob]</td><td>Unique client ID provided via HotSchedules</td></tr>
<td nowrap>clientId [type dataEmployee]</td><td>Unique client ID provided via HotSchedules</td></tr>
<td nowrap>defRate [type dataJob]</td><td>Default Pay Rate for job code</td></tr>
<td nowrap>dob [type wsEmployee]</td><td>Employee Date of Birth</td></tr>
<td nowrap>email [type dataEmployee]</td><td>Employee email address</td></tr>
<td nowrap>empNum [type dataEmployee]</td><td>Employee POS ID</td></tr>
<td nowrap>errors [type wsReturn]</td><td>Error Codes</td></tr>
<td nowrap>Exception</td><td>Exception Codes</td></tr>
<td nowrap>failCount [type wsReturn]</td><td>Total number of records that failed to meet basic import specifications</td></tr>
<td nowrap>FName [type dataEmployee]</td><td>Employee First Name</td></tr>
<td nowrap>hireDate [type wsEmployee]</td><td>Employee Hire Date</td></tr>
<td nowrap>hsEmpId [type dataEmpJob]</td><td>HotSchedules Internal employee account ID</td></tr>
<td nowrap>hsId [type dataEmployee]</td><td>HotSchedules Internal employee account ID</td></tr>
<td nowrap>hsId [type dataJob]</td><td>HotSchedules Internal employee account ID</td></tr>
<td nowrap>hsJobId [type dataEmpJob]</td><td>HotSchedules Internal job code ID</td></tr>
<td nowrap>item [type wsEmpJobArray]</td><td>All jobs assigned to all active employees for that store</td></tr>
<td nowrap>item [type wsEmployeeArray]</td><td>All employees at this store.</td></tr>
<td nowrap>item [type wsJobArray]</td><td>All jobs at this store.</td></tr>
<td nowrap>jobName [type dataJob]</td><td>Address Line 1</td></tr>
<td nowrap>LName [type dataEmployee]</td><td>Address Line 2</td></tr>
<td nowrap>message [type Exception]</td><td>Alternative ID for employee generally reserved for the HR ID.</td></tr>
<td nowrap>mobile [type dataEmployee]</td><td>City field for Address</td></tr>
<td nowrap>NName [type dataEmployee]</td><td>Unique client ID provided via HotSchedules</td></tr>
<td nowrap>ovtWage [type dataEmpJob]</td><td>Unique client ID provided via HotSchedules</td></tr>
<td nowrap>phone [type dataEmployee]</td><td>Default Pay Rate for job code</td></tr>
<td nowrap>posEmpId [type dataEmpJob]</td><td>Employee Date of Birth</td></tr>
<td nowrap>posId [type dataJob]</td><td>Employee email address</td></tr>
<td nowrap>posJobId [type dataEmpJob]</td><td>Employee POS ID</td></tr>
<td nowrap>primary [type dataEmpJob]</td><td>Error Codes</td></tr>
<td nowrap>regWage [type dataEmpJob]</td><td>Exception Codes</td></tr>
<td nowrap>state [type dataEmployee]</td><td>Total number of records that failed to meet basic import specifications</td></tr>
<td nowrap>status [type dataEmployee]</td><td>Active = 1, Inactive = 0, Terminated = o1</td></tr>
<td nowrap>storeNum [type dataEmpJob]</td><td>Unique numeric store ID within HotSchedules. Generally, set up to mirror the client internal store IDs.</td></tr>
<td nowrap>storeNum [type dataEmployee]</td><td>Unique numeric store ID within HotSchedules. Generally, set up to mirror the client internal store IDs.</td></tr>
<td nowrap>storeNum [type dataJob]</td><td>Unique numeric store ID within HotSchedules. Generally, set up to mirror the client internal store IDs.</td></tr>
<td nowrap>success [type wsReturn]</td><td>Missing description.</td></tr>
<td nowrap>successCount [type wsReturn]</td><td>Number of records that successfully met the basic import specification</td></tr>
<td nowrap>termDate [type wsEmployee]</td><td>Employee termination date</td></tr>
<td nowrap>zipCode [type dataEmployee]</td><td>Zip code from Address</td></tr>
</tbody>
</table>




####setEmpJobs
This method takes in a concept ID, store ID, and an array of WSEmpJob objects to assign jobs to individual employees. This method returns a WSReturn object.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>Concept</td>
<td>Int</td>
<td>1..1</td>
<td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.
</td>
</tr>
<tr>
<td>storeNum</td>
<td>Int</td>
<td>1..1</td>
<td>Numeric (integer) identifier for the store. Must be unique within the concept.</td>
</tr>
<tr>
<td>jobs</td>
<td>wsEmpJobArray</td>
<td>1..1</td>
<td>Array of WSEmpJob objects. Each object represents one employee job, so a single employee can have one or more employee jobs (EmpJob) assigned to him/her. Each job that the employee works will be a separate object in this
array.
</td>
</tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td>1..1</td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>1..1</td>
<td>WSReturn object</td>
</tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Exception</td>
<td>Exception</td>
<td>perm 3008<br>API_EMP_PERMISSION_SET_EMP_JOBS<br>client not found
</td>
</tr>
</tbody>
</table>

##LaborService
This service is intended for third parties to be able to request labor data from HotSchedules and import it into their POS/data warehouse/enterprise/etc. system.

* Location: [http://services.hotschedules.com/api/services/LaborService?wsdl](http://services.hotschedules.com/api/services/LaborService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>

- **getLaborByBusDate:** This method will take a concept ID, store number, start and end dates and a labor type and return a list of total labor by job code for each interval for the business date requested for that concept, store and labor type.
<br>

 - Intervals are configured during initial setup for the customer and are typically 30 minutes or 15 minutes.
<br>

- **getLaborByJobAndInterval:** This method will take a concept ID, store number, start and end dates and a labor type and return a list of total labor by job code for each interval in the date range requested for that concept, store and labor type.
 <br>

 - Intervals are configured during initial setup for the customer and are typically 30 minutes or 15 minutes.
<br>

- **setLaborForecastByJob:** Setter of Labor forecast data for a particular store end point to update/set labor per job and xx-minute interval (xx = client interval length in minutes).

####getLaborByBusDate
This method will take a concept ID, store number, start and end dates and a labor type and return a list of total labor by job code for each interval in the date range requested for that concept, store and labor type.
 
Intervals are configured during initial setup for the customer and are typically 30 minutes.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td nowrap></td><td></td></tr></td></tr>
<td nowrap></td><td></td><td></td></tr>
<td nowrap>All</td>-<td>-</td><td>-</td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>Start date for the range of data requested</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>End date for the range of data requested</td></tr>
<td nowrap>laborType</td><td>laborType</td><td>Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled".</td></tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>return</td><td>wsLaborJobArray</td><td>Returns a wsLaborJobArray object, which is an array of wsLaborJob
    objects.<br>
    Each wsLaborJob object contains.<br><br>
    • &nbsp;&nbsp;a
    jobCode (which corresponds to the numeric ID that identifies this job)<br>
    • &nbsp;&nbsp;a
    jobName (the name for this job)<br>
    • &nbsp;&nbsp;a
    wsLaborInterval object, which can contain<br><br>
    + an intervalDate object (an hsSimpleDate that determines the date for this
    particular interval)<br>
    + an intervalTime object (an hsSimpleTime that determines the start time for
    this particular interval. Interval length in implied by&nbsp;&nbsp; the span
    between two intervalTime objects)<br>
    + a laborDate object (an enum which can be "optimal", "forecasted",
    "scheduled"<br>
    + an volume value (which represents the value for the laborDate type for
    this particular interval, determined by intervalDate and intervalTime)<br><br>

    <b>** </b>Note about labor types<b> **</b><br>
    <br>
    <b>"scheduled" </b>labor refers to shifts that have been scheduled and posted and
    are assigned to an employee. This will not include house shifts or shifts
    not assigned to an employee.<br>
    <br>
    <b>"forecasted" </b>labor refers to labor shifts generated after forecast labor
    drivers and applying labor shift generation rules within the Activity•based
    forecasting module in HotSchedules<br>
    <br>
    <b>"optimal" </b>labor refers to labor shifts generated by using actual labor
    driver values and applying labor shift generation rules specified in the
    Activity•based forecasting module in HotSchedules. It represents the labor
    shifts that would have been generated using an exact forecast of labor
    drivers.</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<SOAPENV:Envelope
          xmlns:SOAPENC="http://schemas.xmlsoap.org/soap/encoding/"
          xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
          xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
          xmlns:ns1="http://services.hotschedules.com/api/services/LaborService"
          xmlns:ns2="http://schemas.xmlsoap.org/soap/envelope/"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema•instance"
          xmlns:SOAPENV="http://schemas.xmlsoap.org/soap/envelope/" SOAPENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
          <SOAPENV:Header>
                      <wsse:Security mustUnderstand="true">
                                  <wsse:UsernameToken>
                                              <wsse:Username>REDACTED</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordT ext">REDACTED</wsse:Password>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </SOAPENV:Header>
          <ns2:Body>
                      <ns1:getLaborByJobAndInterval>
                                  <concept>1</concept>
                                  <storeNum>1101645</storeNum>
                                  <start>
                                              <day>8</day>
                                              <month>7</month>
                                              <year>2014</year>
                                  </start>
                                  <end>
                                              <day>14</day>
                                              <month>7</month>
                                              <year>2014</year>
                                  </end>
                                  <laborType>forecasted</laborType>
                      </ns1:getLaborByJobAndInterval>
          </ns2:Body>
</SOAPENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:getEmpInfoResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/EmpService">
                                  <return>
                                              <item>
                                                          <accountCreated>2015•11•04T10:54:22.807•06:00</accountCreated>
                                                          <assignedSchedules>
                                                                      <extId>0</extId>
                                                                      <hsId>964330043</hsId>
                                                                      <name>Kitchen</name>
                                                          </assignedSchedules>
                                                          <assignedSchedules>
                                                                      <extId>•1</extId>
                                                                      <hsId>964318722</hsId>
                                                                      <name>Meetings</name>
                                                          </assignedSchedules>
                                                          <assignedSchedules>
                                                                      <extId>0</extId>
                                                                      <hsId>964330041</hsId>
                                                                      <name>Team Member</name>
                                                          </assignedSchedules>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>1</empNum>
                                                          <lastUpdated>2015•11•09T10:29:31.123•06:00</lastUpdated>
                                                          <permissionSetName>Employee</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•04T08:33:41.090•06:00</accountCreated>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                                          <permissionSetName>HS ASC Support</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•04T08:42:02.483•06:00</accountCreated>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                                          <lastUpdated>2015•11•05T18:29:55.857•06:00</lastUpdated>
                                                          <permissionSetName>Admin ALL</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•04T08:49:32.623•06:00</accountCreated>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                                          <lastUpdated>2015•11•04T08:49:33.120•06:00</lastUpdated>
                                                          <permissionSetName>Default HS Support User</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•04T08:49:33.887•06:00</accountCreated>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                                          <lastUpdated>2015•11•04T08:49:34.093•06:00</lastUpdated>
                                                          <permissionSetName>Default HotSchedules Employee</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•05T18:02:12.477•06:00</accountCreated>
                                                          <assignedSchedules>
                                                                      <extId>0</extId>
                                                                      <hsId>964330043</hsId>
                                                                      <name>Kitchen</name>
                                                          </assignedSchedules>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>2</empNum>
                                                          <lastUpdated>2015•11•09T10:30:32.927•06:00</lastUpdated>
                                                          <permissionSetName>Employee</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2015•11•09T09:38:47.617•06:00</accountCreated>
                                                          <assignedSchedules>
                                                                      <extId>0</extId>
                                                                      <hsId>964330043</hsId>
                                                                      <name>Kitchen</name>
                                                          </assignedSchedules>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>3</empNum>
                                                          <lastUpdated>2015•11•09T10:29:31.170•06:00</lastUpdated>
                                                          <permissionSetName>Employee</permissionSetName>
                                              </item>
                                              <item>
                                                          <accountCreated>2016•01•07T11:25:55.020•06:00</accountCreated>
                                                          <empHrId>•1</empHrId>
                                                          <empNum>•1</empNum>
                                                          <lastUpdated>2016•01•07T11:28:13.373•06:00</lastUpdated>
                                                          <permissionSetName>Admin</permissionSetName>
                                              </item>
                                  </return>
                      </ns1:getEmpInfoResponse>
          </soap:Body>
</soap:Envelope>
```



####getLaborByJobAndInterval
This method will take a concept ID, store number, start and end dates and a labor type and return a list of total labor by job code for each interval in the date range requested for that concept, store and labor type.

Intervals are configured during initial setup for the customer and are typically 30 minutes.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap></td><td></td><td></td></tr>
<td nowrap>All</td><td> </td><td> </td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>Start date for the range of data requested</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>End date for the range of data requested</td></tr>
<td nowrap>laborType</td><td>laborType</td><td>Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled".</td></tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>return</td><td>wsLaborJobArray</td><td><b style="font-weight:normal;" id="docs-internal-guid-bdd39fa2-174d-fa7f-1f1d-d70a4fad8466">
              <p dir="ltr" style="line-height:1.2;margin-top:0pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">Returns a wsLaborJobArray object, which is an array of wsLaborJob objects.</span></p>
              <p dir="ltr" style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">Each wsLaborJob object contains.</span></p>
              <p dir="ltr" style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><br></span></p><p
dir="ltr"
style="line-height:1.2;margin-top:3pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">§ &nbsp;a jobCode (which corresponds to the numeric ID that identifies this job)</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">§ &nbsp;a jobName (the name for this job)</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:3pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">§ &nbsp;a wsLaborInterval object, which can contain</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:3pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><br></span></p><p
dir="ltr"
style="line-height:1.2;margin-top:3pt;margin-bottom:0pt;text-indent: 17pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">+ an intervalDate object (an hsSimpleDate that determines the date for this particular interval)</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;text-indent: 17pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">+ an intervalTime object (an hsSimpleTime that determines the start time for this particular interval. Interval length in implied by the span between two intervalTime objects)</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;text-indent: 17pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">+ a laborDate object (an enum which can be "optimal", "forecasted", "scheduled"</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;text-indent: 17pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">+ an volume value (which represents the value for the laborDate type for this particular interval, determined by intervalDate and intervalTime)</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><br></span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;">** Note about labor types **</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:3pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><strong>"scheduled"</strong> labor refers to shifts that have been scheduled and posted and are assigned to an employee. This will not include house shifts or shifts not assigned to an employee.</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><br></span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><strong>"forecasted"</strong> labor refers to labor shifts generated after forecast labor drivers and applying labor shift generation rules within the Activity•based forecasting module in HotSchedules</span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><br></span></p><p
dir="ltr"
style="line-height:1.2;margin-top:2pt;margin-bottom:0pt;"><span
style="font-size:10pt;font-family:'Open Sans';color:#000000;background-color:transparent;font-weight:400;font-style:normal;font-variant:normal;text-decoration:none;vertical-align:baseline;white-space:pre-wrap;"><strong>"optimal"</strong> labor refers to labor shifts generated by using actual labor driver values and applying labor shift generation rules specified in the Activity•based forecasting module in HotSchedules. It represents the labor shifts that would have been generated using an exact forecast of labor drivers</span></p></b><br
class="Apple-interchange-newline"></td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<SOAPENV:Envelope
          xmlns:SOAPENC="http://schemas.xmlsoap.org/soap/encoding/"
          xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
          xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
          xmlns:ns1="http://services.hotschedules.com/api/services/LaborService"
          xmlns:ns2="http://schemas.xmlsoap.org/soap/envelope/"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema•instance"
          xmlns:SOAPENV="http://schemas.xmlsoap.org/soap/envelope/" SOAPENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
          <SOAPENV:Header>
                      <wsse:Security mustUnderstand="true">
                                  <wsse:UsernameToken>
                                              <wsse:Username>REDACTED</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordT ext">REDACTED</wsse:Password>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </SOAPENV:Header>
          <ns2:Body>
                      <ns1:getLaborByJobAndInterval>
                                  <concept>1</concept>
                                  <storeNum>1101645</storeNum>
                                  <start>
                                              <day>8</day>
                                              <month>7</month>
                                              <year>2014</year>
                                  </start>
                                  <end>
                                              <day>14</day>
                                              <month>7</month>
                                              <year>2014</year>
                                </end>
                                  <laborType>forecasted</laborType>
                      </ns1:getLaborByJobAndInterval>
          </ns2:Body>
</SOAPENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope>
          <soap:Body>
                      <ns1:getLaborByJobAndIntervalResponse>
                                  <return>
                                              <item>
                                                          <interval>
                                                                      <intervalDate>
                                                                                  <day>8</day>
                                                                                  <month>7</month>
                                                                                  <year>2014</year>
                                                                      </intervalDate>
                                                                      <intervalTime>
                                                                                  <hours>0</hours>
                                                                                  <militaryTime>true</militaryTime>
                                                                                  <minutes>0</minutes>
                                                                                  <seconds>0</seconds>
                                                                      </intervalTime>
                                                                      <laborType>forecasted</laborType>
                                                                      <volume>0.0</volume>
                                                          </interval>
                                                          <interval>
                                                                      <intervalDate>
                                                                                  <day>8</day>
                                                                                  <month>7</month>
                                                                                  <year>2014</year>
                                                                      </intervalDate>
                                                                      <intervalTime>
                                                                                  <hours>0</hours>
                                                                                  <militaryTime>true</militaryTime>
                                                                                  <minutes>30</minutes>
                                                                                  <seconds>0</seconds>
                                                                      </intervalTime>
                                                                      <laborType>forecasted</laborType>
                                                                      <volume>0.0</volume>
                                                          </interval>
                                                          <jobCode>16000</jobCode>
                                                          <jobName>Crew Person</jobName>
                                              </item>
                                  </return>
                      </ns1:getLaborByJobAndIntervalResponse>
          </soap:Body> </soap:Envelope>
```





####setLaborForecastByJob
This method takes in a concept ID, store ID, business date, daypart start and end times,labor forecast and  jobExtId. Forecasted labor for the site, date, internal and job will be updated for the purpose of labor scheduling and all relevant reports. The call can be sent for a full week or single date. All intervals must be updated. A zero in the interval is an acceptable value. A null or blank is an acceptable value and will be treated as a zero. If sent for a single date only the date provided will be updated. All other dates within the week will not be impacted and any values already in the database will be retained. A full day's data must be sent, updating only one interval within a business date is not permitted and the call will fail.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td> </td><td>1..1</td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>1..1</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>jobs</td><td>wsEmpJobArray</td><td>1..1</td><td>Array of WSEmpJob objects. Each object represents one employee job, so a single employee can have one or more employee jobs (EmpJob) assigned to him/her. Each job that the employee works will be a separate object in this array.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>Formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Formatted yyyy</td></tr>
<td nowrap>dayPartStartTime</td><td>dateTime</td><td>0..1</td><td>Day part start time</td></tr>
<td nowrap>laborForecastMinutes</td><td>int</td><td>1..1</td><td>Minutes value</td></tr>
<td nowrap>jobExtRef</td><td>int</td><td>1..1</td><td>Job reference id</td></tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td>1..1</td><td></td></tr>
<td nowrap>return</td><td>wsReturn</td><td>1..1</td><td>WSReturn object</td></tr>
</tbody>
</table>

**Faults**

<table>
<thead>
<tr>
<th>Name</th>
<th>Content</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>Exception</td><td>Exception</td><td>perm 3008<br>
API_EMP_PERMISSION_SET_EMP_JOBS<br>
client not found</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:lab="http://services.hotschedules.com/api/services/LaborService">
   <soapenv:Header/>
   <soapenv:Body>
      <lab:setLaborForecastByJob>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <idata>
            <!--Zero or more repetitions:-->
            <item>
               <businessDate>
                  <day>10</day>
                  <month>9</month>
                  <year>2017</year>
               </businessDate>
               <dayPartStartDate>
                  <day>10</day>
                  <month>9</month>
                  <year>2017</year>
               </dayPartStartDate>
               <dayPartStartTime>0045</dayPartStartTime>
               <laborForecastMinutes>15</laborForecastMinutes>
               <jobExtRef>11</jobExtRef>
            </item>
         </idata>
      </lab:setLaborForecastByJob>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soapenv:Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:lab="http://services.hotschedules.com/api/services/LaborService">
  <soapenv:Header/>
  <soapenv:Body>
    <lab:setLaborForecastByJob>
      <concept>8436</concept>
      <storeNum231</storeNum>
      <idata>
        <item>
          <businessDate>
            <day>10</day>
            <month>9</month>
            <year>2017</year>
          </businessDate>
          <dayPartStartDate>
            <day>10</day>
            <month>9</month>
            <year>2017</year>
          </dayPartStartDate>
          <dayPartStartTime>0000</dayPartStartTime>
          <jobExtRef>55</jobExtRef>
          <laborForecastMinutes>1</laborForecastMinutes>
        </item>
        <item>
          <businessDate>
            <day>10</day>
            <month>9</month>
            <year>2017</year>
          </businessDate>
          <dayPartStartDate>
            <day>10</day>
            <month>9</month>
            <year>2017</year>
          </dayPartStartDate>
          <dayPartStartTime>0030</dayPartStartTime>
          <jobExtRef>55</jobExtRef>
          <laborForecastMinutes>2</laborForecastMinutes>
        </item>
      </idata>
    </lab:setLaborForecastByJob>
  </soapenv:Body>
</soapenv:Envelope>
```

##OperatingBudgetPlanService
Allows a customer to SET their budget via API. The service also allow a customer to GET their labor budget data.

* Location: [http://services.hotschedules.com/api/services/OperatingBudgetPlanService?wsdl](http://services.hotschedules.com/api/services/OperatingBudgetPlanService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getLaborData:** COMING SOON...
- **setLaborData:** COMING SOON...

####getLaborData
####setLaborData

##ProjectedLaborService
Description: Coming Soon...

* Location: [http://services.hotschedules.com/api/services/ProjectedLaborService?wsdl](http://services.hotschedules.com/api/services/ProjectedLaborService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>

####Coming Soon...


##ProjectedSalesService
This service is intended for third parties to be able to grab projected sales data from HotSchedules and import it into their POS/data warehouse/enterprise/etc. system.

* Location: [http://services.hotschedules.com/api/services/ProjectedSalesService?wsdl](http://services.hotschedules.com/api/services/ProjectedSalesService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getProjectedSales:** This method takes in a concept ID, store ID, start and end dates. It returns an array of WSProjectedSales objects, which represent the projected sales totals for a particular piece of time, for import into the POS.
<br>
- **getProjectedSalesV3:** This method takes in a concept ID, store ID, start and end dates. It returns an array of WSProjectedSales objects, which represent the projected sales totals for a particular piece of time, for import into the POS.

####getProjectedSales
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSProjectedSales objects, which represent the projected sales totals for a particular piece of time, for import into the POS.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap></td><td></td><td></td><td></td></tr>
<td nowrap>All</td><td> </td><td>1..1</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>concept</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>location. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>dateTime</td><td>1..1</td><td>First day of projected sales.</td></tr>
<td nowrap>end</td><td>dateTime</td><td>1..1</td><td>Last day of projected sales.</td></tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td>1..1</td><td></td></tr>
<td nowrap>return</td><td>wsProjectedSalesArray</td><td>1..1</td><td>Array of WSProjectedSales objects, which represent the projected sales totals for a particular period.</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:proj="http://services.hotschedules.com/api/services/ProjectedSalesService">
   <soapenv:Header/>
   <soapenv:Body>
      <proj:getProjectedSales>
         <concept>1</concept>
         <storeNum>55</storeNum>
         <start>2017-05-01</start>
         <end>2017-05-30</end>
      </proj:getProjectedSales>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getProjectedSalesResponse xmlns:ns1="http://services.hotschedules.com/api/services/ProjectedSalesService">
         <return>
            <item>
               <businessDate>2017-05-01T00:00:00-05:00</businessDate>
               <dateTotal>4903.84</dateTotal>
               <dayPartTotals>
                  <dayPartEndTime>1970-01-01T10:00:00-06:00</dayPartEndTime>
                  <dayPartName>AM</dayPartName>
                  <dayPartStartTime>1969-12-31T22:00:00-06:00</dayPartStartTime>
                  <dayPartTotal>1247.08</dayPartTotal>
               </dayPartTotals>
               <dayPartTotals>
                  <dayPartEndTime>1969-12-31T22:00:00-06:00</dayPartEndTime>
                  <dayPartName>PM</dayPartName>
                  <dayPartStartTime>1970-01-01T10:00:00-06:00</dayPartStartTime>
                  <dayPartTotal>3656.76</dayPartTotal>
               </dayPartTotals>
            </item>
</return>
      </ns1:getProjectedSalesResponse>
   </soap:Body>
</soap:Envelope>
```

####getProjectedSalesV3
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSProjectedSales objects, which represent the projected sales totals for a particular piece of time, for import into the POS.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.


<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td>1..1</td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>1..1</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>1..1</td><td>First day of projected sales requested. This is an hsSimpleDate object.</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>1..1</td><td>First day of projected sales requested. This is an hsSimpleDate object.</td></tr>
</tbody>
</table>

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

<table>
<thead>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Occurs</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>All</td><td></td><td>1..1</td><td></td></tr>
<td nowrap>return</td><td>wsProjectedSalesArray</td><td>1..1</td><td>Array of WSProjectedSales3 objects, which represent the projected sales totals for a particular period. hsSimpleDate objects are used for dates and hsSimpleTime objects for times.</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:proj="http://services.hotschedules.com/api/services/ProjectedSalesService">
   <soapenv:Header/>
   <soapenv:Body>
      <proj:getProjectedSalesV3>
         <concept>1</concept>
         <storeNum>55</storeNum>
         <start>
            <day>01</day>
            <month>05</month>
            <year>2017</year>
         </start>
         <end>
            <day>05</day>
            <month>05</month>
            <year>2017</year>
         </end>
      </proj:getProjectedSalesV3>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getProjectedSalesV3Response xmlns:ns1="http://services.hotschedules.com/api/services/ProjectedSalesService">
         <return>
            <item>
               <businessDate>
                  <day>1</day>
                  <month>5</month>
                  <year>2017</year>
               </businessDate>
               <dateTotal>4903.84</dateTotal>
               <dayPartTotals>
                  <dayPartEndTime>
                     <amPm/>
                     <hours>16</hours>
                     <militaryTime>true</militaryTime>
                     <minutes>0</minutes>
                     <seconds>0</seconds>
                  </dayPartEndTime>
                  <dayPartName>AM</dayPartName>
                  <dayPartStartTime>
                     <amPm/>
                     <hours>4</hours>
                     <militaryTime>true</militaryTime>
                     <minutes>0</minutes>
                     <seconds>0</seconds>
                  </dayPartStartTime>
                  <dayPartTotal>1247.08</dayPartTotal>
               </dayPartTotals>
               <dayPartTotals>
                  <dayPartEndTime>
                     <amPm/>
                     <hours>4</hours>
                     <militaryTime>true</militaryTime>
                     <minutes>0</minutes>
                     <seconds>0</seconds>
                  </dayPartEndTime>
                  <dayPartName>PM</dayPartName>
                  <dayPartStartTime>
                     <amPm/>
                     <hours>16</hours>
                     <militaryTime>true</militaryTime>
                     <minutes>0</minutes>
                     <seconds>0</seconds>
                  </dayPartStartTime>
                  <dayPartTotal>3656.76</dayPartTotal>
               </dayPartTotals>
            </item>
</return>
      </ns1:getProjectedSalesV3Response>
   </soap:Body>
</soap:Envelope>
```











##SalesService
This service is intended for third parties to be able to import their sales items into the HotSchedules system in a straightforward fashion. Currently there is only one method for setting sales items.

* Location: [http://services.hotschedules.com/api/services/SalesService?wsdl](http://services.hotschedules.com/api/services/SalesService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getRVCs:** This method takes in a concept ID and a store ID and returns an array of revenue centers for that store.
<br>

 - Revenue centers will typically establish where to attribute a sale: Bar, Dining, To go, etc.Revenue centers can be local to a particular store, or defined in HotSchedules as belonging to an entire group (called group•level RVCs).
 <br>
 <br>
- **getSalesCats:**  This method takes in a concept ID and a store ID and returns an array of sales categories for that store.
<br>

 - Sales categories will typically establish what kind of item was sold: Food, Beverage, Alcohol, Merchandise.Sales categories can be local to a particular store, or defined in HotSchedules as belonging to an entire group (called group•level sales categories)
 <br>
 <br>

- **getSalesItemsV3:** This method takes in a concept ID, store ID and returns an array of sales items for that store. Sales items indicated which item was sold.
<br>

- **setSalesItems:** This method takes in a concept ID, store ID, a start and end date and an array of WSSalesItem objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains sales items for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of sales, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the sales items are already in the HS database and do not need to be updated, then nothing will change. The method returns a WSReturn object.
<br>

- **setSalesItemsV3:** This method takes in a concept ID, store ID, a start and end date and an array of WSSalesItem objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains sales items for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of sales, every day, 6 days of it will be ""overlapping"" data) and will insert and update data as needed. If the sales items are already in the HS database and do not need to be updated, then nothing will change. The method returns a WSReturn object. This method uses hsSimpleDate objects for dates.
<br>

- **setSalesItemsV4:** Same as setSalesItemsV3 but accepts alphanum store XR.


####getRVCs
####getSalesCats
####getSalesItemsV3
####setSalesItems
####setSalesItemsV3
####setSalesItemsV4

##ScheduleService
This service is intended for third parties to be able to grab scheduled shifts from HotSchedules and import them into their POS/data warehouse/enterprise/etc. system.

* Location: [http://services.hotschedules.com/api/services/ScheduleService?wsdl](http://services.hotschedules.com/api/services/ScheduleService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getLocations:** This method takes in a concept ID and store ID. It returns an array of dataLocation objects, each of which represent one HotSchedules schedule location.
<br>

- **getSchedule:** This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem objects, which represent one scheduled shift each, for import into the POS. This method returns a limited amount of data per shift: employee HS ID, employee POS ID, internal HS Job ID, POS Job ID, shift start date/time, shift end date/time, work week start date/time, work week end date/time.
<br>

- **getSchedule2:** This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem2 objects, which represent one scheduled shift each, for import into the POS. This method returns the same data as getSchedule, plus extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS."
<br>

- **getScheduleV3:** This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem3 objects, which represent one scheduled shift each, for import into the POS. This method returns the same data as getSchedule, plus extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS. This method uses hsSimpleDate objects for dates."
<br>

- **getShiftsV3:** This method takes in a concept ID, store ID, start and end dates and three flags (isHouse, isScheduled and isPosted). It returns an array of WSScheduleItem3 objects, which represent one scheduled shift each. What shifts are returned depends on the flags set: isHouse • includes scheduled or posted shifts that are not assigned to an employee (called 'house shifts' in HotSchedules). isScheduled • includes shifts that are in schedules that have been saved in HotSchedules, but might not have been posted isPosted • includes shifts that are in schedules that have been set to the 'posted' status within HotSchedules. This method returns extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS."
<br>

- **getTemplates:** Getter of client-level forecast template information Start and End dates may not be more than 30 days apart for this method.

####getLocations
####getSchedule
####getSchedule2
####getScheduleV3
####getShiftsV3
####getTemplates


##TimeCardService
This service is intended for third parties to be able to import their time cards into the HotSchedules system or get time cards from HotSchedules in a straightforward fashion.

* Location: [http://services.hotschedules.com/api/services/TimeCardService?wsdl](http://services.hotschedules.com/api/services/TimeCardService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getTimeCards:** This method takes in a concept ID, store ID, start and end dates. It returns an array of wsTimeCard3 objects, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in and clock out times. If this store is using HotSchedules' web•based timeclock for employee clock•in, any open punches in the date range are also included in the response.
<br>

- **getTimeCardsDeclaredTips:** This method takes in a concept ID, store ID, start and end dates. It returns an array of wsTimeCardsDeclaredTips objects, which represent one employee time card each including Declared Tips. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in, clock out times and declared tips. If this store is using HotSchedules' web•based timeclock for employee clock•in, any open punches in the date range are also included in the response."
<br>

- **getTimeCardsV2:** Same as getTimeCards but additionally provides double time info for each timecard.
<br>

- **setTimeCards:** This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCard objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be ""overlapping"" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.
<br>

- **setTimeCardsDeclaredTips:** This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCardsDeclaredTips objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be ""overlapping"" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.
<br>

- **setTimeCardsV3:** This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCard objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object. This method uses hsSimpleDate objects for dates.
<br>

- **updateTimeCards:** This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCard objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

####getTimeCards
####getTimeCardsDeclaredTips
####getTimeCardsV2
####getTimeCardsV3
####setTimeCards
####setTimeCardsDeclaredTips
####setTimeCardsV3
####updateTimeCards


##TimeOffService
This service is intended for third parties to be able to request approved time off requests from HotSchedules.

* Location: [http://services.hotschedules.com/api/services/TimeOffService?wsdl](http://services.hotschedules.com/api/services/TimeOffService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getApprovedPTO:** Returns a list of approved time off for the specified client and time range. The result does not support range-based time off.

####getApprovedPTO

##VolumeService
This service is intended for third parties to be able to request and send volume driver related data from/to HotSchedules. Driver items include examples such as guests, tables, entrees, etc...

* Location: [http://services.hotschedules.com/api/services/VolumeService?wsdl](http://services.hotschedules.com/api/services/VolumeService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getDriversByInterval:** This method takes in a concept ID, store ID, start and end dates, a volume type, and a data type and returns a list of volume counts for each interval in the date range requested. Supported Volume Types are:  “TABLE”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS” Supported Data Types are: “ACTUAL”, “ADJ_FORECASTED”, and “PRE_ADJ_FORECASTED”.
<br>

- **getGuestCounts:** This method will take a concept ID, store number, start and end dates and return a list of guest counts for the date range requested.
<br>

- **getVolumeCounts:** This method will take a concept ID, store number, start and end dates and a volume type and return a list of volume counts for the date range requested. Supported Volume Types are: “TABLE”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS”
<br>

- **setForecastDrivers:** This method takes in a concept ID, store ID, workweek startdate and enddate , starttime and endtime, volume amount, volume type, and a revenue center for the purpose of submitting forecasted volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change.
<br>

- **setForecastDriversV2:** Same as setForecastDrivers but accepts alphanum store XR.
<br>

- **setGuestCounts:** This method takes in a concept ID, store ID, business date, date time, guest count and a revenue center for the purpose of submitting actual guest count drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains guest counts for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.
<br>

- **setVolumeCountsV2:** Same as setVolumeCounts but accepts alphanum store XR.
 <br>

- **setVolumeCountsV3:** Same as setVolumeCountsV2 but accepts custom volume types.

####getDriversByInterval
####getGuestCounts
####getVolumeCounts
####setForecastDrivers
####setForecastDriversV2
####setGuestCounts
####setVolumeCounts
####setVolumeCountsV2
####setVolumeCountsV3

