#Available SOAP Web Services  

The HotSchedules SOAP API provides a user-friendly way to obtain HS Data. Each service contains a **sayHello** call, a test method intended to be used to validate access to the service. It returns a text message indicating success.

**[CertificationService](#certificationservice):** This service is intended for third parties to be able to request and set certification requests from HotSchedules.
<br>

**[EmpService](#empservice):** This service provides operations for a third party to push or request employee and employee job data into HotSchedules.
<br>

**[LaborService](#laborservice):** This service is intended for third parties to be able to request labor data from HotSchedules and import it into their POS/data warehouse/enterprise/etc.
<br>

**[OperatingBudgetPlanService](#operatingbudgetplanservice):** Allows a customer to SET their budget via API. You can submit multiple job data throughout a week for the same data type id. The service also allow a customer to GET their labor budget data.
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<td nowrap>success [type wsReturn]</td><td>Indicator of the success or failure.</td></tr>
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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
Enables a customer to GET their budget via API. The service also allow a customer to SET their labor budget data.

* Location: [http://services.hotschedules.com/api/services/OperatingBudgetPlanService?wsdl](http://services.hotschedules.com/api/services/OperatingBudgetPlanService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getLaborData:** Enables a customer to GET their labor budget data. 
- **setLaborData:** Enables a customer to SET their labor budget data.

####getLaborData
This method takes in a concept ID, store ID and a data Type ID. In order to utilize the method, customer must have 3031 "API - API Operating Budget Plan Service - Set OBP" permission enabled.

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
<td nowrap>All</td><td> </td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>dataTypeId</td><td>int</td><td>The id of Labor Budget Type (LaborDollars, LaborPercent, SPLH, GPLH, LH100, LaborHours types). The ids correspond to labor budget types in the following way: 0 - LaborDollars, 1 - LaborPercent, 2 - SPLH, 3 - GPLH, 4 - LH100, 5 - LaborHours. This parameter is mandatory. If you pass a non existing type (10, for instance), an error will appear. dataTypeId value must be integer from 0 to 5.</td></tr>
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
<td nowrap>dataTypeID</td><td>int</td><td>integer from 0 to 5</td></tr>
<td nowrap>dayOfWeek</td><td>int</td><td>the day of week (is valid for values from Sunday (1) to Saturday (7)</td></tr>
<td nowrap>value</td><td>int</td><td>actual volume of work</td></tr>
<td nowrap>id</td><td>int</td><td>posJobId of the job</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:oper="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
   <soapenv:Header/>
   <soapenv:Body>
      <oper:getLaborData>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <dataTypeId>1</dataTypeId>
      </oper:getLaborData>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getLaborDataResponse xmlns:ns1="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
         <return>
            <dataTypeId>1</dataTypeId>
            <jobs>
               <days>
                  <dayOfWeek>1</dayOfWeek>
                  <value>1.8</value>
               </days>
               <days>
                  <dayOfWeek>2</dayOfWeek>
                  <value>1.65</value>
               </days>
               <days>
                  <dayOfWeek>3</dayOfWeek>
                  <value>1.54</value>
               </days>
               <days>
                  <dayOfWeek>4</dayOfWeek>
                  <value>1.6</value>
               </days>
               <days>
                  <dayOfWeek>5</dayOfWeek>
                  <value>1.7</value>
               </days>
               <days>
                  <dayOfWeek>6</dayOfWeek>
                  <value>1.9</value>
               </days>
               <days>
                  <dayOfWeek>7</dayOfWeek>
                  <value>2.0</value>
               </days>
               <id>-1</id>
            </jobs>
         </return>
      </ns1:getLaborDataResponse>
   </soap:Body>
</soap:Envelope>
```

####setLaborData
This method takes in a concept ID, store ID, data Type ID, day of the week, value, and ID.

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
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>dataTypeID</td><td>int</td><td>integer from 0 to 5</td></tr>
<td nowrap>dayOfWeek</td><td>int</td><td>the day of week (is valid for values from Sunday (1) to Saturday (7)</td></tr>
<td nowrap>value</td><td>int</td><td>actual volume of work</td></tr>
<td nowrap>id</td><td>int</td><td>posJobId of the job</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:oper="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
   <soapenv:Header/>
   <soapenv:Body>
      <oper:setLaborData>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <budget>
            <!--type: int-->
            <dataTypeId>3</dataTypeId>
            <!--Zero or more repetitions:-->
            <jobs>
               <!--Zero or more repetitions:-->
               <days>
                  <!--type: int-->
                  <dayOfWeek>5</dayOfWeek>
                  <!--type: double-->
                  <value>1.65</value>
               </days>
               <!--type: int-->
               <id>6</id>
            </jobs>
         </budget>
      </oper:setLaborData>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setLaborDataResponse xmlns:ns1="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>2</successCount>
         </return>
      </ns1:setLaborDataResponse>
   </soap:Body>
</soap:Envelope>
```

####getLaborDataForWeek
Get multiple job data throughout a week for the same data type id.

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:oper="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
   <soapenv:Header/>
   <soapenv:Body>
      <oper:getLaborDataForWeek>
         <concept>3</concept>
         <storeNum>3</storeNum>
         <startDate>
            <!--type: int-->
            <day>3</day>
            <!--type: int-->
            <month>3</month>
            <!--type: int-->
            <year>3</year>
         </startDate>
         <endDate>
            <!--type: int-->
            <day>3</day>
            <!--type: int-->
            <month>3</month>
            <!--type: int-->
            <year>3</year>
         </endDate>
         <dataTypeId>3</dataTypeId>
      </oper:getLaborDataForWeek>
   </soapenv:Body>
</soapenv:Envelope>
```

####setLaborDataForWeek
Set multiple job data throughout a week for the same data type id.

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:oper="http://services.hotschedules.com/api/services/OperatingBudgetPlanService">
   <soapenv:Header/>
   <soapenv:Body>
      <oper:setLaborDataForWeek>
         <concept>3</concept>
         <storeNum>3</storeNum>
         <startDate>
            <!--type: int-->
            <day>3</day>
            <!--type: int-->
            <month>3</month>
            <!--type: int-->
            <year>3</year>
         </startDate>
         <endDate>
            <!--type: int-->
            <day>3</day>
            <!--type: int-->
            <month>3</month>
            <!--type: int-->
            <year>3</year>
         </endDate>
         <budget>
            <!--type: int-->
            <dataTypeId>3</dataTypeId>
            <!--Zero or more repetitions:-->
            <jobs>
               <!--Zero or more repetitions:-->
               <days>
                  <!--type: int-->
                  <dayOfWeek>3</dayOfWeek>
                  <!--type: double-->
                  <value>1.051732E7</value>
               </days>
               <!--type: int-->
               <id>3</id>
            </jobs>
         </budget>
      </oper:setLaborDataForWeek>
   </soapenv:Body>
</soapenv:Envelope>
```


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
<?xml version="1.0" encoding="UTFo8"?>
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
<?xml version="1.0" encoding="UTFo8"?>
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
This method takes in a concept ID and a store ID and returns an array of revenue centers for that store.
Revenue centers will typically establish where to attribute a sale: Bar, Dining, To go, etc.Revenue centers can be local to a particular store, or defined in HotSchedules as belonging to an entire group (called group•level RVCs).

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
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
<td nowrap>return</td><td>wsRevenueCenterArray</td><td>1..1</td><td>Array of wsRevenueCenter objects, which represents all revenue centers defined for that store. This will include store and group level revenue centers, and will be flagged appropriately.</td></tr>
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
<td>perm 3002<br>API_SALES_PERMISSION<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:sal="http://services.hotschedules.com/api/services/SalesService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•5A4A0145444B759EC8145272034993393">
                                              <wsse:Username>HSAPIUser</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">ao24 wO2n8gkh7lp</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">eup88j1y/qnxGKg2Rn6J4A==</wsse:Nonce>
                                              <wsu:Created>2016•01•13T21:25:49.933Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <sal:getRVCs>
                                  <concept>101</concept>
                                  <storeNum>111</storeNum>
                      </sal:getRVCs>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:getRVCsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/SalesService">
                                  <return>
                                              <item>
                                                          <extId>10</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <revenueCenterName>Dine in</revenueCenterName>
                                              </item>
                                              <item>
                                                          <extId>17</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <revenueCenterName>Bar</revenueCenterName>
                                              </item>
                                              <item>
                                                          <extId>15</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <revenueCenterName>To go</revenueCenterName>
                                              </item>
                                  </return>
                      </ns1:getRVCsResponse>
          </soap:Body>
</soap:Envelope>
```
####getSalesCats
This method takes in a concept ID and a store ID and returns an array of sales categories for that store. Sales categories will typically establish what kind of item was sold: Food, Beverage, Alcohol,
Merchandise.Sales categories can be local to a particular store, or defined in HotSchedules as belonging to an entire group (called group•level sales categories).

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
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
<td nowrap>return</td><td>wsSalesCategoryArray</td><td>1..1</td><td>Array of wsSalesCategory objects, which represents all sales categories defined for that store. This will include store and group level sales categories, and will be flagged appropriately.</td></tr>
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
<td>perm 3002<br>API_SALES_PERMISSION<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
          xmlns:sal="http://services.hotschedules.com/api/services/SalesService"
          xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
          <soapenv:Header>
                      <wsse:Security
                                  xmlns:wsse="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•secext•1.0.xsd"
                                  xmlns:wsu="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•wssecurity•utility•1.0.xsd" soapenv:mustUnderstand="1">
                                  <wsse:UsernameToken wsu:Id="UsernameToken•5A4A0145444B759EC8145272075572695">
                                              <wsse:Username>HSAPIUser</wsse:Username>
                                              <wsse:Password Type="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•username•token•profile•1.0#PasswordText">ao24 wO2n8gkh7lp</wsse:Password>
                                              <wsse:Nonce EncodingType="http://docs.oasis•open.org/wss/2004/01/oasis•200401•wss•soap•message•security•1.0#Base64Bina ry">HWXdmwP4l8qNEDjt4a0G9Q==</wsse:Nonce>
                                              <wsu:Created>2016•01•13T21:32:35.726Z</wsu:Created>
                                  </wsse:UsernameToken>
                      </wsse:Security>
          </soapenv:Header>
          <soapenv:Body>
                      <sal:getSalesCats>
                                  <concept>101</concept>
                                  <storeNum>111</storeNum>
                      </sal:getSalesCats>
          </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
          <soap:Body>
                      <ns1:getSalesCatsResponse
                                  xmlns:ns1="http://services.hotschedules.com/api/services/SalesService">
                                  <return>
                                              <item>
                                                          <extId>10</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <salesCategoryName>Food</salesCategoryName>
                                              </item>
                                              <item>
                                                          <extId>20</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <salesCategoryName>Beverages</salesCategoryName>
                                              </item>
                                              <item>
                                                          <extId>30</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <salesCategoryName>Beer</salesCategoryName>
                                              </item>
                                              <item>
                                                          <extId>40</extId>
                                                          <groupLevel>true</groupLevel>
                                                          <salesCategoryName>Wine</salesCategoryName>
                                              </item>
                                  </return>
                      </ns1:getSalesCatsResponse>
          </soap:Body>
</soap:Envelope>
```
####getSalesItemsV3
This method takes in a concept ID, store ID, start and end dates.It returns an array of sales for that store.

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
<td nowrap>day</td><td>int</td><td></td><td>Formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td></td><td>Formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td></td><td>Formatted yyyy</td></tr>
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
<td nowrap>return</td><td>wsSalesItem3Array</td><td>1..1</td><td>Array of WSSalesItem objects. Each object represents one sales item at this store.</td></tr>
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
<td>perm 3002<br>API_SALES_PERMISSION<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soapenv:Envelope
  xmlns:sal="http://services.hotschedules.com/api/services/SalesService"
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header>
    <wsse:Security
      xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
      xmlns:wsu="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityoutilityo1.0.xsd" soapenv:mustUnderstand="1">
      <wsse:UsernameToken wsu:Id="UsernameTokeno5A4A0145444B759EC81452722705669100">
        <wsse:Username>HSAPIUser</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText">ao24 wO2n8gkh7lp</wsse:Password>
        <wsse:Nonce EncodingType="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssosoapomessageosecurityo1.0#Base64Bina ry">WHQ2rdJcHsI92WDsEaBDpA==</wsse:Nonce>
        <wsu:Created>2016o01o13T22:05:05.669Z</wsu:Created>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>
  <soapenv:Body>
    <sal:getSalesItemsV3>
      <concept>101</concept>
      <storeNum>111</storeNum>
      <start>
        <day>1</day>
        <month>1</month>
        <year>2015</year>
      </start>
      <end>
        <day>1</day>
        <month>2</month>
        <year>2015</year>
      </end>
    </sal:getSalesItemsV3>
  </soapenv:Body> </soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getSalesItemsV3Response
      xmlns:ns1="http://services.hotschedules.com/api/services/SalesService">
      <return>
        <item>
          <clientId>16477839</clientId>
          <empId>o1</empId>
          <extId>o1</extId>
          <rvc>o1</rvc>
          <salesCat>o1</salesCat>
          <storeNum>111</storeNum>
          <ttl>13.45</ttl>
          <businessDate>
            <day>3</day>
            <month>1</month>
            <year>2015</year>
          </businessDate>
          <transDate>
            <day>4</day>
            <month>1</month>
            <year>2015</year>
          </transDate>
          <transTime>
            <hours>2</hours>
            <militaryTime>true</militaryTime>
            <minutes>28</minutes>
            <seconds>35</seconds>
          </transTime>
        </item>
        <item>
          <clientId>16477839</clientId>
          <empId>o1</empId>
          <extId>o1</extId>
          <rvc>o1</rvc>
          <salesCat>o1</salesCat>
          <storeNum>111</storeNum>
          <ttl>0.0</ttl>
          <businessDate>
            <day>3</day>
            <month>1</month>
            <year>2015</year>
          </businessDate>
          <transDate>
            <day>4</day>
            <month>1</month>
            <year>2015</year>
          </transDate>
          <transTime>
            <hours>2</hours>
            <militaryTime>true</militaryTime>
            <minutes>33</minutes>
            <seconds>19</seconds>
          </transTime>
        </item>
      </return>
    </ns1:getSalesItemsV3Response>
  </soap:Body>
</soap:Envelope>
```
####setSalesItems
This method takes in a concept ID, store ID, a start and end date and an array of WSSalesItem objects. If the sales items are already in the HS database and do not need to be updated, then nothing will change. The method returns a WSReturn object.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>sales</td><td>wsSalesItemArray</td><td>1..1</td><td>Array of WSSalesItem objects. Each object represents one sales item at this store.</td></tr>
<td nowrap>start</td><td>dateTime</td><td>1..1</td><td>Business date of the first sales item in the array.</td></tr>
<td nowrap>end</td><td>dateTime</td><td>1..1</td><td>Business date of the last sales item in the array.</td></tr>

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
<td>perm 3002<br>API_SALES_PERMISSION<br>client not found
</td>
</tr>
</tbody>
</table>


####setSalesItemsV3
This method takes in a concept ID, store ID, a start and end date and an array of WSSalesItem objects. If the sales items are already in the HS database and do not need to be updated, then nothing will change. The method returns a WSReturn object.

This method uses hsSimpleDate objects for dates.

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
<td nowrap>sales</td><td>wsSalesItem3Array</td><td>1..1</td><td>Array of WSSalesItem objects. Each object represents one sales item at this store.</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>1..1</td><td>Business date of the first sales item in the array. This method uses hsSimpleDate objects for dates.</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>1..1</td><td>Business date of the last sales item in the array. This method uses hsSimpleDate objects for dates.</td></tr>
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
<td nowrap>Exception</td><td>Exception</td><td>perm 3002<br>
API_SALES_PERMISSION<br>
client not found<br>
validation errors</td></tr>
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
<td nowrap>dataSalesItem</td><td>Contains sales item data (sales category, revenue center, sales amount, ID of employee that made the sale, store ID where the sale ocurred)</td></tr>
<td nowrap>hsSimpleDate</td><td>Simple date object that excludes any time zone or locale data. Consists of day, month and year integer values.</td></tr>
<td nowrap>hsSimpleTime</td><td>Simple time object that excludes any time zone or locale data. Consists of hour, minute and second integer values, am/pm string indicator and militaryTime flag.</td></tr>
<td nowrap>wsReturn</td><td>Contains array of error strings, fail count, success flag, success count.</td></tr>
<td nowrap>wsRevenueCenter</td><td>Contains revenue center objects (RVC ID (external ref ID), RVC name)</td></tr>
<td nowrap>wsRevenueCenterArray</td><td>An array of wsRevenueCenterArray objects. Each wsRevenueCenter object describes the total revenue center sales for a given revenue center.<br>
Each wsRevenueCenter object contains,<br>
•      a RevenueCenter (which corresponds to the numeric ID that identifies this revenue center)</td></tr>
<td nowrap>wsSalesCategory</td><td>Contains sales category objects (salesCategoryName, extId, groupLevel)</td></tr>
<td nowrap>wsSalesCategoryArray</td><td>Array of wsSalesCategory objects, which represents all sales categories defined for that store. This will include store and group level sales categories, and will be flagged appropriately.
</td></tr>
<td nowrap>wsSalesItem</td><td>Extends dataSalesItem (includes business date and calendar date of the sale)</td></tr>
<td nowrap>wsSalesItem3</td><td>Extends dataTimeCard (includes business date and hsSimpleDate object and clock in and clockout date/times as hsSimpleDate and hsSimpleTime objects)</td></tr>
</tbody>
</table>

Contains sales item data (sales category, revenue center, sales amount, ID of employee that made the sale, store ID where the sale occurred)

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>catName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the category</td></tr>
<td nowrap>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>empId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID</td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction</td></tr>
<td nowrap>rvc</td><td>int</td><td>1..1</td><td>No</td><td>Revenue Center ID</td></tr>
<td nowrap>rvcName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the revenue center</td></tr>
<td nowrap>salesCat</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the sales category</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>ttl</td><td>float</td><td>1..1</td><td>No</td><td>Total of the sales category</td></tr>
</tbody>
</table>

**Referenced By**

  - Complex Type wsSalesItem
  - Complex Type wsSalesItem3
 
Simple date object that excludes any time zone or locale data. Consists of day, month and year integer values.

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>No</td><td>Formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>No</td><td>Formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>No</td><td>Formatted yyyy</td></tr>
</tbody>
</table>

**Referenced By**

  - Element businessDate [type wsSalesItem3]
  - Element transDate [type wsSalesItem3]
 
Simple time object that excludes any time zone or locale data. Consists of hour, minute and second integer values, am/pm string indicator and militaryTime flag.

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>amPm</td><td>string</td><td>0..1</td><td>No</td><td>AM or PM indicator. amPm enum. If militaryTime is set to true, amPm is ignored.</td></tr>
<td nowrap>hours</td><td>int</td><td>1..1</td><td>No</td><td>Hour value</td></tr>
<td nowrap>militaryTime</td><td>boolean</td><td>1..1</td><td>No</td><td>Military Time indicator</td></tr>
<td nowrap>minutes</td><td>int</td><td>1..1</td><td>No</td><td>Minutes value</td></tr>
<td nowrap>seconds</td><td>int</td><td>1..1</td><td>No</td><td>Seconds value</td></tr>
</tbody>
</table>

**Referenced By**

  - Element transTime [type wsSalesItem3]
 
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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>errors</td><td>string</td><td>0..*</td><td>Yes</td><td>Error messages</td></tr>
<td nowrap>failCount</td><td>int</td><td>1..1</td><td>No</td><td>Number of records that failed to meet basic import specifications</td></tr>
<td nowrap>success</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicator of the success or failure</td></tr>
<td nowrap>successCount</td><td>int</td><td>1..1</td><td>No</td><td>Total number of records that successfully met basic import specifications</td></tr>
</tbody>
</table>

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>groupLevel</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>revenueCenterName</td><td>string</td><td>0..1</td><td>No</td><td>Revenue center name.</td></tr>
</tbody>
</table>

**Referenced By**

  - Element item [type wsRevenueCenterArray]

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>item</td><td>wsRevenueCenter</td><td>0..*</td><td>Yes</td><td>Contains revenue center objects (RVC ID (external ref ID), RVC name)</td></tr>
</tbody>
</table>

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction</td></tr>
<td nowrap>groupLevel</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>salesCategoryName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the sales category.</td></tr>
</tbody>
</table>

**Referenced By**

  - Element item [type wsSalesCategoryArray]

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>item</td><td>wsSalesCategory</td><td>0..*</td><td>Yes</td><td>Contains sales category objects (salesCategoryName, extId, groupLevel)</td></tr>
</tbody>
</table>

Extends dataSalesItem (includes business date and calendar date of the sale)

**Derived By**

Extending dataSalesItem

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>catName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the category.</td></tr>
<td nowrap>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>empId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID.</td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction.</td></tr>
<td nowrap>rvc</td><td>int</td><td>1..1</td><td>No</td><td>Revenue Center ID.</td></tr>
<td nowrap>rvcName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the revenue center.</td></tr>
<td nowrap>salesCat</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the sales category.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the
concept.</td></tr>
<td nowrap>ttl</td><td>float</td><td>1..1</td><td>No</td><td>Total of the sales category.</td></tr>
<td nowrap>businessDate</td><td>dateTime</td><td>0..1</td><td>No</td><td>Business date of transaction.</td></tr>
<td nowrap>dateTime</td><td>dateTime</td><td>0..1</td><td>No</td><td>Date and time of transaction.</td></tr>
</tbody>
</table>

**Referenced By**

  - Element item [type wsSalesItemArray]
 
**Description**

Extends dataTimeCard (includes business date and hsSimpleDate object and clock in and clockout date/times as hsSimpleDate and hsSimpleTime objects).

**Derived By**

Extending dataSalesItem

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>catName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the category</td></tr>
<td nowrap>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>empId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID</td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction</td></tr>
<td nowrap>rvc</td><td>int</td><td>1..1</td><td>No</td><td>Revenue Center ID</td></tr>
<td nowrap>rvcName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the revenue center</td></tr>
<td nowrap>salesCat</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the sales category</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept</td></tr>
<td nowrap>ttl</td><td>float</td><td>1..1</td><td>No</td><td>Total of the sales category</td></tr>
<td nowrap>businessDate</td><td>hsSimpleDate</td><td>0..1</td><td>No</td><td>Business date of transaction</td></tr>
<td nowrap>transDate</td><td>hsSimpleDate</td><td>0..1</td><td>No</td><td>Date of the transaction</td></tr>
<td nowrap>transTime</td><td>hsSimpleTime</td><td>0..1</td><td>No</td><td>Time of the transaction</td></tr>
</tbody>
</table>

**Referenced By**

  - Element item [type wsSalesItem3Array]

**Elements: SalesItemService**

**Elements**

<table>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>amPm [type hsSimpleTime]</td><td>AM or PM indicator.</td></tr>
<td nowrap>businessDate [type wsSalesItem]</td><td>Business date of transaction.</td></tr>
<td nowrap>businessDate [type wsSalesItem3]</td><td>Business date of transaction.</td></tr>
<td nowrap>catName [type dataSalesItem]</td><td>Category name.</td></tr>
<td nowrap>clientId [type dataSalesItem]</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>dateTime [type wsSalesItem]</td><td>Date time of transaction.</td></tr>
<td nowrap>day [type hsSimpleDate]</td><td>Day formatted dd.</td></tr>
<td nowrap>empId [type dataSalesItem]</td><td>Employee ID.</td></tr>
<td nowrap>errors [type wsReturn]</td><td>Error messages.</td></tr>
<td nowrap>Exception</td><td>Message for the exception</td></tr>
<td nowrap>extId [type dataSalesItem]</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>extId [type wsRevenueCenter]</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>extId [type wsSalesCategory]</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>failCount [type wsReturn]</td><td>Total number of records that failed to meet basic import specifications.</td></tr>
<td nowrap>groupLevel [type wsRevenueCenter]</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>groupLevel [type wsSalesCategory]</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>hours [type hsSimpleTime]</td><td>Number of hours.</td></tr>
<td nowrap>item [type wsRevenueCenterArray]</td><td>Array of wsRevenueCenter objects, which represents all revenue centers defined for that store. This will include store and group level revenue centers, and will be flagged appropriately.</td></tr>
<td nowrap>item [type wsSalesCategoryArray]</td><td>Array of wsSalesCategory objects, which represents all sales categories defined for that store. This will include store and group level sales categories, and will be flagged appropriately.</td></tr>
<td nowrap>item [type wsSalesItem3Array]</td><td>Array of WSSalesItem objects. Each object represents one sales item at this store.</td></tr>
<td nowrap>item [type wsSalesItemArray]</td><td>Array of WSSalesItem objects. Each object represents one sales item at this store.</td></tr>
<td nowrap>message [type Exception]</td><td>Information about an exception that has been caught.</td></tr>
<td nowrap>militaryTime [type hsSimpleTime]</td><td>Military Time indicator.</td></tr>
<td nowrap>minutes [type hsSimpleTime]</td><td>Minute value.</td></tr>
<td nowrap>month [type hsSimpleDate]</td><td>Month value.</td></tr>
<td nowrap>revenueCenterName</td><td>Revenue center name.</td></tr>
<td nowrap>[type wsRevenueCenter]</td><td>Contains revenue center objects (RVC ID (external ref ID), RVC name).</td></tr>
<td nowrap>rvc [type dataSalesItem]</td><td>Revenue Center.</td></tr>
<td nowrap>rvcName [type dataSalesItem]</td><td>Name for the revenue center associated with the location within the restaurant.</td></tr>
<td nowrap>salesCat [type dataSalesItem]</td><td>Sales category.</td></tr>
<td nowrap>salesCategoryName [type</td><td>Name of the sales category.</td></tr>
<td nowrap>wsSalesCategory]</td><td>Contains sales category objects (salesCategoryName, extId, groupLevel)</td></tr>
<td nowrap>seconds [type hsSimpleTime]</td><td>Seconds value.</td></tr>
<td nowrap>storeNum [type dataSalesItem]</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>success [type wsReturn]</td><td>Indicator of the success or failure</td></tr>
<td nowrap>successCount [type wsReturn]</td><td>Total number of records that successfully met basic import specifications.</td></tr>
<td nowrap>transDate [type wsSalesItem3]</td><td>Transaction date.</td></tr>
<td nowrap>transTime [type wsSalesItem3]</td><td>Time of the transaction</td></tr>
<td nowrap>ttl [type dataSalesItem]</td><td>Total of the sales category</td></tr>
<td nowrap>year [type hsSimpleDate]</td><td>year yyyy format</td></tr>
</tbody>
</table>

Type String

**Referenced By**

 - Complex Type hsSimpleTime

Type dateTime

**Referenced By**

 - Complex Type wsSalesItem Type hsSimpleDate

**Content Model**

Contains elements as defined in the following table.

<table>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>No</td><td>Formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>No</td><td>Formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>No</td><td>Formatted yyyy</td></tr>
</tbody>
</table>

**Referenced By**

 - Complex Type wsSalesItem3 Type string

**Referenced By**

 - Complex Type dataSalesItem

 - Complex Type wsSalesItem

 - Complex Type wsSalesItem3
 
Type int

**Referenced By**

 - Complex Type dataSalesItem

 - Complex Type wsSalesItem

 - Complex Type wsSalesItem3

Type dateTime

**Referenced By**

 - Complex Type wsSalesItem

 - Complex Type hsSimpleDate

 - Complex Type dataSalesItem

 - Complex Type wsSalesItem

 - Complex Type wsSalesItem3 

 - Complex Type wsReturn

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>message</td><td>string</td><td>0..1</td><td>No</td><td>Return message</td></tr>
</tbody>
</table>

 - Complex Type dataSalesItem
 - Complex Type wsSalesItem
 - Complex Type wsSalesItem3
 - Complex Type wsRevenueCenter
 - Complex Type wsSalesCategory
 - Complex Type wsReturn
 - Complex Type hsSimpleTime

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>groupLevel</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>revenueCenterName</td><td>string</td><td>0..1</td><td>No</td><td>Revenue center name.</td></tr>
</tbody>
</table>

**Referenced By**

 - Complex Type wsRevenueCenterArray

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>groupLevel</td><td>boolean</td><td>1..1</td><td>No</td><td>Indicates if the revenue center is assigned at the group level.</td></tr>
<td nowrap>salesCategoryName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the sales category.</td></tr>
</tbody>
</table>

**Referenced By**

 - Complex Type wsSalesCategoryArray

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>catName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the category</td></tr>
<td nowrap>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>empId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID</td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction</td></tr>
<td nowrap>rvc</td><td>int</td><td>1..1</td><td>No</td><td>Revenue Center ID</td></tr>
<td nowrap>rvcName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the revenue center</td></tr>
<td nowrap>salesCat</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the sales category</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>ttl</td><td>float</td><td>1..1</td><td>No</td><td>Total of the sales category</td></tr>
<td nowrap>businessDate</td><td>hsSimpleDate</td><td>0..1</td><td>No</td><td>Business date of transaction</td></tr>
<td nowrap>transDate</td><td>hsSimpleDate</td><td>0..1</td><td>No</td><td>Date of the transaction</td></tr>
<td nowrap>transTime</td><td>hsSimpleTime</td><td>0..1</td><td>No</td><td>Time of the transaction</td></tr>
</tbody>
</table>

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>catName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the category</td></tr>
<td nowrap>clientId</td><td>int</td><td>1..1</td><td>No</td><td>Unique identifier for client provided via HotSchedules.</td></tr>
<td nowrap>empId</td><td>int</td><td>1..1</td><td>No</td><td>HotSchedules internal employee account ID</td></tr>
<td nowrap>extId</td><td>int</td><td>1..1</td><td>No</td><td>Numeric ID from the external system associated with the transaction</td></tr>
<td nowrap>rvc</td><td>int</td><td>1..1</td><td>No</td><td>Revenue Center ID</td></tr>
<td nowrap>rvcName</td><td>string</td><td>0..1</td><td>No</td><td>Name of the revenue center</td></tr>
<td nowrap>salesCat</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the sales category</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>No</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>ttl</td><td>float</td><td>1..1</td><td>No</td><td>Total of the sales category</td></tr>
<td nowrap>businessDate</td><td>dateTime</td><td>0..1</td><td>No</td><td>Business date of transaction</td></tr>
<td nowrap>dateTime</td><td>dateTime</td><td>0..1</td><td>No</td><td>Date time of the transaction</td></tr>
</tbody>
</table>

 - Complex Type wsSalesItem
 - Complex Type wsSalesItem3

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>No</td><td>Day formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>No</td><td>Month formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>No</td><td>Year formatted yyyy</td></tr>
</tbody>
</table>

**Referenced By**

 - Complex Type wsSalesItem3

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
<td nowrap>Sequence</td><td></td><td>1..1</td><td></td><td></td></tr>
<td nowrap>amPm</td><td>string</td><td>0..1</td><td>No</td><td>AM or PM indicator. amPm enum. If militaryTime is set to true, amPm</td></tr>
<td nowrap>hours</td><td>int</td><td>1..1</td><td>No</td><td>is ignored.</td></tr>
<td nowrap>militaryTime</td><td>boolean</td><td>1..1</td><td>No</td><td>Hour value</td></tr>
<td nowrap>minutes</td><td>int</td><td>1..1</td><td>No</td><td>Military Time indicator</td></tr>
<td nowrap>seconds</td><td>int</td><td>1..1</td><td>No</td><td>Minutes value</td></tr>
<td nowrap></td><td></td><td></td><td></td><td>Seconds value</td></tr>
</tbody>
</table>

**Referenced By**

 - Complex Type wsSalesItem3
 - Complex Type dataSalesItem
 - Complex Type wsSalesItem
 - Complex Type wsSalesItem3
 - Complex Type hsSimpleDate

####setSalesItemsV4
Same as **[setSalesItemsV3](#setsalesitemsv3)** but accepts alphanum store XR

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
This method takes in a concept ID and store ID. It returns an array of dataLocation objects, each of which represent one HotSchedules schedule location.

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
<td nowrap>return</td><td>dataLocationArray</td><td>1..1</td><td>Array of dataLocation objects.</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<SOAPoENV:Envelope
  xmlns:SOAPoENC="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
  xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:ns1="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:ns2="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:xsi="http://www.w3.org/2001/XMLSchemaoinstance"
  xmlns:SOAPoENV="http://schemas.xmlsoap.org/soap/envelope/" SOAPoENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
  <SOAPoENV:Header>
    <wsse:Security mustUnderstand="true">
      <wsse:UsernameToken>
        <wsse:Username>REDACTED</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText"
>REDACTED</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </SOAPoENV:Header>
  <ns1:Body>
    <ns2:getLocations>
      <concept>1</concept>
      <storeNum>103</storeNum>
    </ns2:getLocations>
  </ns1:Body>
</SOAPoENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope>
  <soap:Body>
    <ns1:getLocationsResponse>
      <return>
        <item>
          <disabled>false</disabled>
          <id>677337753</id>
          <name>Location Name 1</name>
        </item>
        <item>
          <disabled>false</disabled>
          <id>517879406</id>
          <name>Location Name 2</name>
        </item>
      </return>
    </ns1:getLocationsResponse>
  </soap:Body>
</soap:Envelope>
```

####getSchedule
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem objects, which represent one scheduled shift each, for import into the POS. This method returns a limited amount of data per shift: employee HS ID, employee POS ID, internal HS Job ID, POS Job ID, shift start date/time, shift end date/time, work week start date/time, work week end date/time.

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
<td nowrap>start</td><td>dateTime</td><td>1..1</td><td>First day of scheduled shifts you are requesting.</td></tr>
<td nowrap>end</td><td>dateTime</td><td>1..1</td><td>Last day of scheduled shifts you are requesting.</td></tr>
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

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<SOAPoENV:Envelope
  xmlns:SOAPoENC="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
  xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:ns1="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:ns2="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:xsi="http://www.w3.org/2001/XMLSchemaoinstance"
  xmlns:SOAPoENV="http://schemas.xmlsoap.org/soap/envelope/" SOAPoENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
  <SOAPoENV:Header>
    <wsse:Security mustUnderstand="true">
      <wsse:UsernameToken>
        <wsse:Username>REDACTED</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText"
>REDACTED</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </SOAPoENV:Header>
  <ns1:Body>
    <ns2:getSchedule>
      <concept>1</concept>
      <storeNum>37</storeNum>
      <start>2014o04o18T00:00:00</start>
      <end>2014o04o18T00:00:00</end>
    </ns2:getSchedule>
  </ns1:Body>
</SOAPoENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope>
  <soap:Body>
    <ns1:getScheduleResponse>
      <return>
        <item>
          <empHsId>REDACTED
          </empHSId>
          <empPosId>REDACTED</empPosId>
          <jobHsId>2129482342</jobHsId>
          <jobPosId>453</jobPosId>
          <in>2014o04o18T05:00:00o05:00</in>
          <out>2014o04o18T16:00:00o05:00</out>
          <weekEnd>2014o04o24T00:00:00o05:00</weekEnd>
          <weekStart>2014o04o18T00:00:00o05:00</weekStart>
        </item>
        <item>
          <empHSId>REDACTED</empHSId>
          <empPosId>REDACTED</empPosId>
          <jobHsId>837906321</jobHsId>
          <jobPosId>600</jobPosId>
          <in>2014o04o18T06:00:00o05:00</in>
          <out>2014o04o18T14:00:00o05:00</out>
          <weekEnd>2014o04o24T00:00:00o05:00</weekEnd>
          <weekStart>2014o04o18T00:00:00o05:00</weekStart>
        </item>
      </return>
    </ns1:getScheduleResponse>
  </soap:Body>
</soap:Envelope>
```

####getSchedule2

This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem2 objects, which represent one scheduled shift each, for import into the POS. This method returns the same data as getSchedule, plus extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS.

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
<td nowrap>start</td><td>dateTime</td><td>1..1</td><td>First day of scheduled shifts you are requesting.</td></tr>
<td nowrap>end</td><td>dateTime</td><td>1..1</td><td>Last day of scheduled shifts you are requesting.</td></tr>

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
<td nowrap>return</td><td>wsScheduleItem2Array</td><td>1..1</td><td>Array of WSScheduleItem2 objects, which represent one scheduled shift each.</td></tr>
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
<td>perm 3004<br>API_SCHEDULE_PERMISSION
<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<SOAPoENV:Envelope
  xmlns:SOAPoENC="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
  xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:ns1="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:ns2="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:xsi="http://www.w3.org/2001/XMLSchemaoinstance"
  xmlns:SOAPoENV="http://schemas.xmlsoap.org/soap/envelope/"
SOAPoENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
  <SOAPoENV:Header>
    <wsse:Security mustUnderstand="true">
      <wsse:UsernameToken>
        <wsse:Username>REDACTED</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText"
>REDACTED</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </SOAPoENV:Header>
  <ns1:Body>
    <ns2:getSchedule2>
      <concept>1</concept>
      <storeNum>37</storeNum>
      <start>2014o04o18T00:00:00</start>
      <end>2014o04o18T00:00:00</end>
    </ns2:getSchedule2>
  </ns1:Body>
</SOAPoENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope>
  <soap:Body>
    <ns1:getSchedule2Response>
      <return>
        <item>
          <empHSId>REDACTED</empHSId>
          <empPosId>REDACTED</empPosId>
          <jobHsId>2129482342</jobHsId>
          <jobPosId>453</jobPosId>
          <in>2014o04o18T05:00:00o05:00</in>
          <out>2014o04o18T16:00:00o05:00</out>
          <weekEnd>2014o04o24T00:00:00o05:00</weekEnd>
          <weekStart>2014o04o18T00:00:00o05:00</weekStart>
          <locationId>578176916</locationId>
          <ovtMinutes>0</ovtMinutes>
          <ovtRate>0.0</ovtRate>
          <payRate>0.0</payRate>
          <regMinutes>660</regMinutes>
          <scheduleId>2129477321</scheduleId>
          <specialPay>0.0</specialPay>
        </item>
        <item>
          <empHSId>REDACTED</empHSId>
          <empPosId>REDACTED</empPosId>
          <jobHsId>837906321</jobHsId>
          <jobPosId>600</jobPosId>
          <in>2014o04o18T06:00:00o05:00</in>
          <out>2014o04o18T14:00:00o05:00</out>
          <weekEnd>2014o04o24T00:00:00o05:00</weekEnd>
          <weekStart>2014o04o18T00:00:00o05:00</weekStart>
          <locationId>o1</locationId>
          <ovtMinutes>0</ovtMinutes>
          <ovtRate>0.0</ovtRate>
          <payRate>24.0</payRate>
          <regMinutes>480</regMinutes>
          <scheduleId>2129477321</scheduleId>
          <specialPay>0.0</specialPay>
        </item>
      </return>
    </ns1:getSchedule2Response>
  </soap:Body> </soap:Envelope>
```

####getScheduleV3
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItem3 objects, which represent one scheduled shift each, for import into the POS. This method returns the same data as getSchedule, plus extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS.
This method uses hsSimpleDate objects for dates.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>1..1</td><td>First day of scheduled shifts you are requesting. This method uses hsSimpleDate objects for dates.</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>1..1</td><td>Last day of scheduled shifts you are requesting. This method uses hsSimpleDate objects for dates.</td></tr>
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
<td nowrap>return</td><td>wsScheduleItem3Array</td><td>1..1</td><td>Array of WSScheduleItem3 objects, which represent one scheduled shift each.
Dates are hsSimpleDate objects and times are hsSimpleTime objects.</td></tr>
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
<td>perm 3004<br>API_SCHEDULE_PERMISSION
<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<SOAPoENV:Envelope
  xmlns:SOAPoENC="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:wsse="http://docs.oasisoopen.org/wss/2 004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
  xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:ns1="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:ns2="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:xsi="http://www.w3.org/2001/XMLSchemaoinstance"
  xmlns:SOAPoENV="http://schemas.xmlsoap.org/soap/envelope/" SOAPoENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
  <SOAPoENV:Header>
    <wsse:Security mustUnderstand="true">
      <wsse:UsernameToken>
        <wsse:Username>REDACTED</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText"
>REDACTED</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </SOAPoENV:Header>
  <ns1:Body>
    <ns2:getScheduleV3>
      <concept>1</concept>
      <storeNum>37</storeNum>
      <start>
        <day>18</day>
        <month>4</month>
        <year>2014</year>
      </start>
      <end>
        <day>18</day>
        <month>4</month>
        <year>2014</year>
      </end>
    </ns2:getScheduleV3></ns1:Body></SOAPoENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope>
  <soap:Body>lOCA
    <ns1:getScheduleV3Response>
      <return>
        <item>
          <empHSId>1712094</empHSId>
          <empPosId>190</empPosId>
          <jobHsId>489527461</jobHsId>
          <jobPosId>120000</jobPosId>
          <inDate>
            <day>18</day>
            <month>4</month>
            <year>2014</year>
          </inDate>
          <inTime>
            <hours>6</hours>
            <militaryTime>true</militaryTime>
            <minutes>30</minutes>
            <seconds>0</seconds>
          </inTime>
          <locationId>o1</locationId>
          <outDate>
            <day>18</day>
            <month>4</month>
            <year>2014</year>
          </outDate>
          <outTime>
            <hours>15</hours>
            <militaryTime>true</militaryTime>
            <minutes>0</minutes>
            <seconds>0</seconds>
          </outTime>
          <ovtMinutes>0</ovtMinutes>
          <ovtRate>0.0</ovtRate>
          <payRate>0.0</payRate>
          <regMinutes>0</regMinutes>
          <scheduleId>o1</scheduleId>
          <specialPay>0.0</specialPay>
          <weekEnd>
            <day>24</day>
            <month>4</month>
            <year>2014</year>
          </weekEnd>
          <weekStart>
            <day>18</day>
            <month>4</month>
            <year>2014</year>
          </weekStart>
        </item>
      </return>
    </ns1:getScheduleV3Response>
  </soap:Body>
</soap:Envelope>
```
####getShiftsV3
This method takes in a concept ID, store ID, start and end dates and three flags (isHouse, isScheduled and isPosted). It returns an array of WSScheduleItem3 objects, which represent one scheduled shift each. What shifts are returned depends on the flags set:

**isHouse:** includes scheduled or posted shifts that are not assigned to an employee (called 'house shifts' in HotSchedules).

**isScheduled:** includes shifts that are in schedules that have been saved in HotSchedules, but might not have been posted

**isPosted:** includes shifts that are in schedules that have been set to the 'posted' status within HotSchedules

This method returns extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Day formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>Month formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Year formatted yyyy</td></tr>
<td nowrap>isHouse</td><td>boolean</td><td>1..1</td><td>Include house shifts? These are shifts which were never assigned to someone on a schedule, or were once assigned but removed from an employee when their status, job, etc. changed.</td></tr>
<td nowrap>isScheduled</td><td>boolean</td><td>1..1</td><td>Include scheduled shifts? These are shifts which are on a schedule that has been saved in HotSchedules, but might not have been posted</td></tr>
<td nowrap>isPosted</td><td>boolean</td><td>1..1</td><td>These are shifts that are in schedules that have been set to the 'posted' status within HotSchedules.</td></tr>
<td nowrap>jobCodes</td><td>intArray</td><td>1..1</td><td>Integer array of job codes to be included in this method's return. if this parameter is null or empty, all jobs will be included.</td></tr>
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
<td nowrap>return</td><td>wsScheduleItem3Array</td><td>1..1</td><td>Array of WSScheduleItem3 objects, which represent one scheduled shift each.
Dates are hsSimpleDate objects and times are hsSimpleTime objects.</td></tr>
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
<td>perm 3004<br>API_SCHEDULE_PERMISSION
<br>client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soapenv:Envelope
  xmlns:sch="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header>
    <wsse:Security
      xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
      xmlns:wsu="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityoutilityo1.0.xsd" soapenv:mustUnderstand="1">
      <wsse:UsernameToken wsu:Id="UsernameTokeno5A4A0145444B759EC8145271260874466">
        <wsse:Username>laura1234!</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText">laura 1234!</wsse:Password>
        <wsse:Nonce EncodingType="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssosoapomessageosecurityo1.0#Base64Bina ry">m2/v7Yt2bmHeTDmYvu85CA==</wsse:Nonce>
        <wsu:Created>2016o01o13T19:16:48.744Z</wsu:Created>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>
  <soapenv:Body>
    <sch:getShiftsV3>
      <concept>1</concept>
      <storeNum>1</storeNum>
      <start>
        <day>1</day>
        <month>1</month>
        <year>2016</year>
      </start>
      <end>
        <day>9</day>
        <month>2</month>
        <year>2016</year>
      </end>
      <isHouse>false</isHouse>
      <isScheduled>true</isScheduled>
      <isPosted>true</isPosted>
      <jobCodes>
        <!ooZero or more repetitions:
<item>871507284</item>oo>
</jobCodes>
</sch:getShiftsV3>
</soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getShiftsV3Response
      xmlns:ns1="http://services.hotschedules.com/api/services/ScheduleService">
      <return>
        <item>
          <empHSId>17896647</empHSId>
          <empPosId>1</empPosId>
          <jobHsId>964330045</jobHsId>
          <jobPosId>o1</jobPosId>
          <inDate>
            <day>11</day>
            <month>1</month>
            <year>2016</year>
          </inDate>
          <inTime>
            <hours>7</hours>
            <militaryTime>true</militaryTime>
            <minutes>0</minutes>
            <seconds>0</seconds>
          </inTime>
          <locationId>o1</locationId>
          <outDate>
            <day>11</day>
            <month>1</month>
            <year>2016</year>
          </outDate>
          <outTime>
            <hours>15</hours>
            <militaryTime>true</militaryTime>
            <minutes>0</minutes>
            <seconds>0</seconds>
          </outTime>
          <ovtMinutes>0</ovtMinutes>
          <ovtRate>0.0</ovtRate>
          <payRate>9.5</payRate>
          <regMinutes>480</regMinutes>
          <scheduleId>964330041</scheduleId>
          <specialPay>0.0</specialPay>
          <weekEnd>
            <day>16</day>
            <month>1</month>
            <year>2016</year>
          </weekEnd>
          <weekStart>
            <day>10</day>
            <month>1</month>
            <year>2016</year>
          </weekStart>
        </item>
      </return>
    </ns1:getShiftsV3Response>
  </soap:Body>
</soap:Envelope>
```

####getTemplates
This method takes in a concept ID, store ID, start and end dates. This method returns template information.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Day formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>Month formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Year formatted yyyy</td></tr>
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
<td nowrap>return</td><td>Template objects</td><td>1..1</td><td>Returns a list of template objects.</td></tr>
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
<td>invalid start and/or end dates<br>
perm 3004<br>
perm 3002<br>
API_SCHEDULE_PERMISSION<br>
API_SCHEDULE_GET_TEMPLATES_PERMISSION<br>
client not found
</td>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soapenv:Envelope
  xmlns:sch="http://services.hotschedules.com/api/services/ScheduleService"
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header>
    <wsse:Security
      xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
      xmlns:wsu="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityoutilityo1.0.xsd" soapenv:mustUnderstand="1">
      <wsse:UsernameToken wsu:Id="UsernameTokeno63A716DE011BE2D649145262988637423">
        <wsse:Username>laura1234!</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText">laura 1234!</wsse:Password>
        <wsse:Nonce EncodingType="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssosoapomessageosecurityo1.0#Base64Bina ry">WjFLOOT1CCJWLffHSRdCnQ==</wsse:Nonce>
        <wsu:Created>2016o01o12T20:18:06.374Z</wsu:Created>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>
  <soapenv:Body>
    <sch:getTemplates>
      <concept>1</concept>
      <storeNum>1</storeNum>
      <start>
        <day>1</day>
        <month>1</month>
        <year>2016</year>
      </start>
      <end>
        <day>20</day>
        <month>1</month>
        <year>2016</year>
      </end>
    </sch:getTemplates>
  </soapenv:Body>
</soapenv:Envelope>

```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getTemplatesResponse
      xmlns:ns1="http://services.hotschedules.com/api/services/ScheduleService">
      <return>
        <item>
          <durationMinutes>360</durationMinutes>
          <endTime>
            <hours>16</hours>
            <militaryTime>true</militaryTime>
            <minutes>0</minutes>
            <seconds>0</seconds>
          </endTime>
          <jobCode>o1</jobCode>
          <jobName>Baker</jobName>
          <locationId>o1</locationId>
          <locationName>NO_LOC</locationName>
          <scheduleId>964330043</scheduleId>
          <scheduleName>Kitchen</scheduleName>
          <shiftName>Kitchen</shiftName>
          <startTime>
            <hours>10</hours>
            <militaryTime>true</militaryTime>
            <minutes>0</minutes>
            <seconds>0</seconds>
          </startTime>
          <templateDesc>Low Volume</templateDesc>
          <templateGroupId>o1</templateGroupId>
          <templateGroupName>NOT_GROUPED</templateGroupName>
          <templateId>964318045</templateId>
          <templateName>Low Volume</templateName>
          <weekday>6</weekday>
          <weekdayName>Friday</weekdayName>
        </item>
      </return>
    </ns1:getTemplatesResponse>
  </soap:Body></soap:Envelope>
```

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
This method takes in a concept ID, store ID, start and end dates. It returns an array of wsTimeCard3 objects, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in and clock out times. If this store is using HotSchedules' web-based timeclock for employee clock-in, any open punches in the date range are also included in the response.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Day formatted dd</td></tr>
<td nowrap>Month</td><td>int</td><td>1..1</td><td>Month formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Year formatted yyyy</td></tr>

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
<td nowrap>return</td><td>wsTimeCard3Array</td><td>1..1</td><td>Array of wsTimeCard3 objects. Each
object has data for one employee punch record.
Dates are hsSimpleDate objects and times are hsSimpleTime objects.</td></tr>
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
<td nowrap>Exception</td><td>Exception</td><td>perm 3003<br>
perm 3011<br>
API_LABOR_SERVICE<br>
API_LABOR_PERMISSION_GET_TIMECARDS<br>
client not found</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<SOAPoENV:Envelope
  xmlns:SOAPoENC="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
  xmlns:ns0="http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:ns1="http://services.hotschedules.com/api/services/TimeCardService"
  xmlns:ns2="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:xsi="http://www.w3.org/2001/XMLSchemaoinstance"
  xmlns:SOAPoENV="http://schemas.xmlsoap.org/soap/envelope/"
SOAPoENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
  <SOAPoENV:Header>
    <wsse:Security mustUnderstand="true">
      <wsse:UsernameToken>
        <wsse:Username>REDACTED</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText"
>REDACTED</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </SOAPoENV:Header>
  <ns2:Body>
    <ns1:getTimeCards>
      <concept>1</concept>
      <storeNum>103</storeNum>
      <start>
        <day>25</day>
        <month>2</month>
        <year>2014</year>
      </start>
      <end>
        <day>25</day>
        <month>2</month>
        <year>2014</year>
      </end>
    </ns1:getTimeCards>
  </ns2:Body>
</SOAPoENV:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope>
  <soap:Body>
    <ns1:getTimeCardsResponse>
      <return>
        <item>
          <breakMinutes>0</breakMinutes>
          <empPosId>210</empPosId>
          <extId>156393867196</extId>
          <hsId>156393867197</hsId>
          <jobExtId>12</jobExtId>
          <jobName>Expediter</jobName>
          <ovtHrs>0.0</ovtHrs>
          <ovtMins>0</ovtMins>
          <ovtTtl>0.0</ovtTtl>
          <ovtWage>0.0</ovtWage>
          <regHrs>4.6833334</regHrs>
          <regTtl>0.0</regTtl>
          <regWage>8.0</regWage>
          <spcHrs>0.0</spcHrs>
          <spcTtl>0.0</spcTtl>
          <storeNum>103</storeNum>
          <businessDate>
            <day>25</day>
            <month>2</month>
            <year>2014</year>
          </businessDate>
          <clockIn>2014o02o25T10:26:00o06:00</clockIn>
          <clockOut>2014o02o25T15:07:00o06:00</clockOut>
        </item>
        <item>
          <breakMinutes>0</breakMinutes>
          <empPosId>207</empPosId>
          <extId>156393867200</extId>
          <hsId>156393867201</hsId>
          <jobExtId>12</jobExtId>
          <jobName>Expediter</jobName>
          <ovtHrs>0.0</ovtHrs>
          <ovtMins>0</ovtMins>
          <ovtTtl>0.0</ovtTtl>
          <ovtWage>0.0</ovtWage>
          <regHrs>4.983333</regHrs>
          <regTtl>0.0</regTtl>
          <regWage>8.0</regWage>
          <spcHrs>0.0</spcHrs>
          <spcTtl>0.0</spcTtl>
          <storeNum>103</storeNum>
          <businessDate>
            <day>25</day>
            <month>2</month>
            <year>2014</year>
          </businessDate>
          <clockIn>2014o02o25T16:28:00o06:00</clockIn>
          <clockOut>2014o02o25T21:27:00o06:00</clockOut>
        </item>
      </return>
    </ns1:getTimeCardsResponse>
  </soap:Body>
</soap:Envelope>
```

####getTimeCardsDeclaredTips
This method takes in a concept ID, store ID, start and end dates. It returns an array of wsTimeCard3 objects, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in, clock out times and declared tips. If this store is using HotSchedules' webobased timeclock for employee clockoin, any open punches in the date range are also included in the response.

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
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Day formatted dd</td></tr>
<td nowrap>Month</td><td>int</td><td>1..1</td><td>Month formatted mm</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Year formatted yyyy</td></tr>

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
<td nowrap>return</td><td>wsTimeCard3Array</td><td>1..1</td><td>Array of wsTimeCard3 objects. Each
object has data for one employee punch record.
Dates are hsSimpleDate objects and times are hsSimpleTime objects.</td></tr>
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
<td nowrap>Exception</td><td>Exception</td><td>perm 3003<br>
perm 3011<br>
API_LABOR_SERVICE<br>
API_LABOR_PERMISSION_GET_TIMECARDS<br>
client not found</td></tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soapenv:Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:tim="http://services.hotschedules.com/api/services/TimeCardService">
  <soapenv:Header>
    <wsse:Security
      xmlns:wsse="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityosecexto1.0.xsd"
      xmlns:wsu="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssowssecurityoutilityo1.0.xsd" soapenv:mustUnderstand="1">
      <wsse:UsernameToken wsu:Id="UsernameTokeno5A4A0145444B759EC8145271596284975">
        <wsse:Username>laura1234!</wsse:Username>
        <wsse:Password Type="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssousernameotokenoprofileo1.0#PasswordText">laur a1234!</wsse:Password>
        <wsse:Nonce EncodingType="http://docs.oasisoopen.org/wss/2004/01/oasiso200401owssosoapomessageosecurityo1.0#Base64Bin ary">mafwHuh4YzpETuPwHxlC2g==</wsse:Nonce>
        <wsu:Created>2016o01o13T20:12:42.849Z</wsu:Created>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>
  <soapenv:Body>
    <tim:getTimeCardsDeclaredTips>
      <concept>1</concept>
      <storeNum>1</storeNum>
      <start>
        <day>1</day>
        <month>1</month>
        <year>2016</year>
      </start>
      <end>
        <day>10</day>
        <month>1</month>
        <year>2016</year>
      </end>
    </tim:getTimeCardsDeclaredTips>
  </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<?xml version="1.0" encoding="UTFo8"?>
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getTimeCardsDeclaredTipsResponse
      xmlns:ns1="http://services.hotschedules.com/api/services/TimeCardService">
      <return>
        <item>
          <breakMinutes>0</breakMinutes>
          <empPosId>2</empPosId>
          <extId>844268158324</extId>
          <hsId>844268158325</hsId>
          <jobExtId>o1</jobExtId>
          <jobId>o1</jobId>
          <jobName>Baker</jobName>
          <ovtHrs>1.0</ovtHrs>
          <ovtMins>0</ovtMins>
          <ovtTtl>0.0</ovtTtl>
          <ovtWage>0.0</ovtWage>
          <regHrs>8.0</regHrs>
          <regTtl>0.0</regTtl>
          <regWage>0.0</regWage>
          <spcHrs>0.0</spcHrs>
          <spcTtl>0.0</spcTtl>
          <storeNum>1</storeNum>
          <businessDate>
            <day>10</day>
            <month>1</month>
            <year>2016</year>
          </businessDate>
          <clockIn>2016o01o10T15:00:00o06:00</clockIn>
          <clockOut>2016o01o11T00:00:00o06:00</clockOut>
          <declaredTips>0.0</declaredTips>
        </item>
      </return>
    </ns1:getTimeCardsDeclaredTipsResponse>
  </soap:Body>
</soap:Envelope>
```

####getTimeCardsV2
Same as getTimeCards but additionally provides double time info for each timecard.

####getTimeCardsV3
Same as getTimeCardsV2 but additionally exposes the "hsid" info for each timecard.

####setTimeCards
This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCard objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The serveroside logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.


####setTimeCardsDeclaredTips
This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCardsDeclaredTips objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

####setTimeCardsV3
This method takes in a concept ID, store ID, a start and end date and an array of WSTimeCard objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server•side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object. This method uses hsSimpleDate objects for dates.

####updateTimeCards
Similar to setTimeCards but allows for many more flags to control the timecard sync: dropCards, createIds, calculateOvertime, usePunchIds, isSalary, overrideOT, manualPunchUpdate, skipAggregation. The API was created for simulation and shall be used with caution.


##TimeOffService
This service is intended for third parties to be able to request approved time off requests from HotSchedules.

* Location: [http://services.hotschedules.com/api/services/TimeOffService?wsdl](http://services.hotschedules.com/api/services/TimeOffService?wsdl)
* Protocol: SOAP
* Default style: rpc
* Transport protocol: SOAP over HTTP  

<aside class="notice"> <strong>AVAILABLE METHODS</strong> </aside>
- **getApprovedPTO:** Returns a list of approved time off for the specified client and time range. The result does not support range-based time off.

####getApprovedPTO
This method takes in a concept ID, store ID, start date, end date and returns a list of employees approved scheduled time off.

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
<td nowrap>concept</td><td>int</td><td>1..1</td><td>The identifier for the location's concept/group. Must be unique within the company. Contact HotSchedules if you're Not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>1..1</td><td>Numeric (integer) identifier for the location. Must be unique within the concept.</td></tr>
<td nowrap>day</td><td>int</td><td>1..1</td><td>Formatted dd</td></tr>
<td nowrap>month</td><td>int</td><td>1..1</td><td>Formatted dd</td></tr>
<td nowrap>year</td><td>int</td><td>1..1</td><td>Formatted mm</td></tr>
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
<td nowrap>return</td><td>wsReturn</td><td>1..1</td><td>wsReturn object</td></tr>
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
<td>perm 3050<br>API_TIME_OFF_SERVICE_PERMISSION<br>client not found
</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tim="http://services.hotschedules.com/api/services/TimeOffService">
   <soapenv:Header/>
   <soapenv:Body>
      <tim:getApprovedPTO>
         <concept>28</concept>
         <storeNum>408</storeNum>
         <start>
            <!--type: int-->
            <day>27</day>
            <!--type: int-->
            <month>4</month>
            <!--type: int-->
            <year>2016</year>
         </start>
         <end>
            <!--type: int-->
            <day>10</day>
            <!--type: int-->
            <month>5</month>
            <!--type: int-->
            <year>2016</year>
         </end>
      </tim:getApprovedPTO>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getApprovedPTOResponse xmlns:ns1="http://services.hotschedules.com/api/services/TimeOffService">
         <return>
            <item>
               <clientId>408</clientId>
               <date>2016-05-08</date>
               <dayParts>
                  <dayPart>Dinner</dayPart>
                  <dayPart>Lunch</dayPart>
               </dayParts>
               <employeeFirstName>SAM</employeeFirstName>
               <employeeHrId>-1</employeeHrId>
               <employeeLastName>SMITH</employeeLastName>
               <employeePosId>142</employeePosId>
               <jobId>200</jobId>
               <jobName>SERVER/200</jobName>
               <jobRate>11.25</jobRate>
               <timeOffHours>9.00</timeOffHours>
               <timeOffTypeCode>VAC</timeOffTypeCode>
            </item>
            <item>
               <clientId>408</clientId>
               <date>2016-05-09</date>
               <dayParts>
                  <dayPart>Dinner</dayPart>
                  <dayPart>Lunch</dayPart>
               </dayParts>
               <employeeFirstName>SAM</employeeFirstName>
               <employeeHrId>-1</employeeHrId>
               <employeeLastName>SMITH</employeeLastName>
               <employeePosId>142</employeePosId>
               <jobId>200</jobId>
               <jobName>SERVER/200</jobName>
               <jobRate>11.25</jobRate>
               <timeOffHours>4.00</timeOffHours>
               <timeOffTypeCode>VAC</timeOffTypeCode>
            </item>
            <item>
               <clientId>408</clientId>
               <date>2016-05-10</date>
               <dayParts>
                  <dayPart>Dinner</dayPart>
                  <dayPart>Lunch</dayPart>
               </dayParts>
               <employeeFirstName>SAM</employeeFirstName>
               <employeeHrId>-1</employeeHrId>
               <employeeLastName>SMITH</employeeLastName>
               <employeePosId>142</employeePosId>
               <jobId>200</jobId>
               <jobName>SERVER/200</jobName>
               <jobRate>11.25</jobRate>
               <timeOffHours>0</timeOffHours>
               <timeOffTypeCode>VAC</timeOffTypeCode>
            </item>
         </return>
      </ns1:getApprovedPTOResponse>
   </soap:Body>
</soap:Envelope>
```

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
This method will take a concept ID, store number, start and end dates, volume type, and data type and return a list of total driver amount for each interval in the date range requested for that concept, store and labor type.

Intervals are configured during initial setup for the customer and are typically 30 minutes or 15 minutes.


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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>startDate</td><td>hsSimpleDate</td><td>Start date for the range of data requested</td></tr>
<td nowrap>endDate</td><td>hsSimpleDate</td><td>End date for the range of data requested</td></tr>
<td nowrap>volumeType</td><td>driverClass</td><td>Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, and “Products”.</td></tr>
<td nowrap>dataType</td><td>driverType</td><td>Type of driver requested. Allowed types are “ACTUAL”, “ADJ_FORECASTED”, and “PRE_ADJ_FORECASTED”.</td></tr>
</tr>
</tbody>
</table>

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
   <soapenv:Header/>
   <soapenv:Body>
      <vol:getDriversByInterval>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <startDate>
            <day>10</day>
            <month>5</month>
            <year>2017</year>
         </startDate>
         <endDate>
            <day>11</day>
            <month>5</month>
            <year>2017</year>
         </endDate>
         <volumeType>PRODUCTS</volumeType>
         <dataType>ACTUAL</dataType>
      </vol:getDriversByInterval>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:getDriversByIntervalResponse xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <item>
               <companyExtRef>260146</companyExtRef>
               <conceptExtRef>8436</conceptExtRef>
               <driverAmount>0.0</driverAmount>
               <driverClass>PRODUCTS</driverClass>
               <driverType>ACTUAL</driverType>
               <intervalEndDate>
                  <day>10</day>
                  <month>5</month>
                  <year>2017</year>
               </intervalEndDate>
               <intervalEndTime>
                  <hours>0</hours>
                  <militaryTime>true</militaryTime>
                  <minutes>30</minutes>
                  <seconds>0</seconds>
               </intervalEndTime>
               <intervalStartDate>
                  <day>10</day>
                  <month>5</month>
                  <year>2017</year>
               </intervalStartDate>
               <intervalStartTime>
                  <hours>0</hours>
                  <militaryTime>true</militaryTime>
                  <minutes>0</minutes>
                  <seconds>0</seconds>
               </intervalStartTime>
               <storeExtRef>23</storeExtRef>
            </item>
            </return>
      </ns1:getDriversByIntervalResponse>
   </soap:Body>
</soap:Envelope>
```







####getGuestCounts
This method will take a concept ID, store number, start and end dates and return a list of guest counts for the date range requested.

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>start</td><td>dateTime</td><td>Start date for the range of data requested. This is a basic dateTime object.</td></tr>
<td nowrap>end</td><td>dateTime</td><td>End date for the range of data requested. This is a basic dateTime object.</td></tr>

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
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsGuestCountsArray</td>
<td>Returns a wsGuestCountsArray object, which is an array of wsGuestCountsArray objects.
<br>
Each wsGuestCounts object contains<br>
- a businessDate<br>
- a dateTime<br>
- a guestCount<br>
- a rvcExtID which represents the numeric revenue center ID associated with the guest.
</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
  <soapenv:Header/>
  <soapenv:Body>
    <vol:getGuestCounts>
      <concept>1</concept>
      <storeNum>1</storeNum>
      <startDate>2014o09o24T00:00:00</startDate>
      <endDate>2014o09o25T00:00:00</endDate>
    </vol:getGuestCounts>
  </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getGuestCountsResponse
      xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
      <return>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:35:00o05:00</dateTime>
          <guestCount>1.0</guestCount>
          <rvcExtId>4</rvcExtId>
        </item>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:38:00o05:00</dateTime>
          <guestCount>1.0</guestCount>
          <rvcExtId>4</rvcExtId>
        </item>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:41:00o05:00</dateTime>
          <guestCount>1.0</guestCount>
          <rvcExtId>4</rvcExtId>
        </item>
```






####getVolumeCounts
This method will take a concept ID, store number, start and end dates and a volume type and return a list of volume counts for the date range requested.

Supported Volume Types are: "TABLE", "ENTRÉE", "GUESTS", "DELIVERIES", "PRODUCTS", and "TRANSACTIONS"

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>volumeType</td><td>volumeType</td><td>Supported Volume Types are: “TABLE”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS”</td></tr>
<td nowrap>start</td><td>hsSimpleDate</td><td>Start date for the range of data requested</td></tr>
<td nowrap>end</td><td>hsSimpleDate</td><td>End date for the range of data requested</td></tr>
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
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsVolumeCountsArray</td>
<td>Returns a wsVolumeCounts object, which is an array of wsVolumeCounts objects.
<br>
Each wsLaborJob object contains<br>
- a businessDate<br>
- a dateTime<br>
- a volumeType<br>
- a volumeCount<br>
- a rvcExtID which represents the numeric revenue center ID associated with the count.
</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
  <soapenv:Header/>
  <soapenv:Body>
    <vol:getVolumeCounts>
      <concept>1</concept>
      <storeNum>101</storeNum>
      <volumeType>GUESTS</volumeType>
      <startDate>2014o09o24T00:00:00</startDate>
      <endDate>2014o09o25T00:00:00</endDate>
    </vol:getVolumeCounts>
  </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ns1:getGuestCountsResponse
      xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
      <return>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:35:00o05:00</dateTime>
          <volumeType>GUESTS</volumeType>
          <volumeCount>1.0</volumeCount>
          <rvcExtId>4</rvcExtId>
        </item>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:38:00o05:00</dateTime>
          <volumeType>GUESTS</volumeType>
          <volumeCount>1.0</volumeCount>
          <rvcExtId>4</rvcExtId>
        </item>
        <item>
          <businessDate>2014o09o24T00:00:00o05:00</businessDate>
          <dateTime>2014o09o24T06:41:00o05:00</dateTime>
          <volumeType>GUESTS</volumeType>
          <volumeCount>1.0</volumeCount>
          <rvcExtId>4</rvcExtId>
        </item>
```

####setForecastDrivers
This method takes in a concept ID, store ID, workweek startdate and enddate , starttime and endtime, volume amount, volume type, and a revenue center for the purpose of submitting forecasted volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The serveroside logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change.

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>WorkWeekStartDate</td><td>hsSimpleDate</td><td>Day, Month and Year</td></tr>
<td nowrap>rvcExtID</td><td>int</td><td>Numeric ID for the revenue center associated with the transaction</td></tr>
<td nowrap>DriverAmount</td><td>Int</td><td>Value of the driver amount for the transaction</td></tr>
<td nowrap>volumeType</td><td>volumeType</td><td>Supported Volume Types are: “TABLE”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS”</td></tr>
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
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>WSReturn objects.</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
   <soapenv:Header/>
   <soapenv:Body>
      <vol:setForecastDrivers>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <workweekStartDate>
            <day>28</day>
            <month>8</month>
            <year>2017</year>
         </workweekStartDate>
         <driverData>
            <!--Zero or more repetitions:-->
            <item>
               <driverAmount>1000</driverAmount>
               <!--Optional:-->
               <intervalEndDate>
                  <day>28</day>
                  <month>8</month>
                  <year>2017</year>
               </intervalEndDate>
               <!--Optional:-->
               <intervalEndTime>
                  <!--Optional:-->
                  <amPm>1</amPm>
                  <hours>6</hours>
                  <militaryTime>false</militaryTime>
                  <minutes>30</minutes>
                  <seconds>0</seconds>
               </intervalEndTime>
               <!--Optional:-->
               <intervalStartDate>
                  <day>28</day>
                  <month>8</month>
                  <year>2017</year>
               </intervalStartDate>
               <!--Optional:-->
               <intervalStartTime>
                  <!--Optional:-->
                  <amPm>1</amPm>
                  <hours>6</hours>
                  <militaryTime>false</militaryTime>
                  <minutes>0</minutes>
                  <seconds>0</seconds>
               </intervalStartTime>
               <rvcId>4</rvcId>
               <!--Optional:-->
               <volumeType>SALES</volumeType>
            </item>
         </driverData>
      </vol:setForecastDrivers>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setForecastDriversResponse xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>1</successCount>
         </return>
      </ns1:setForecastDriversResponse>
   </soap:Body>
</soap:Envelope>
```



####setForecastDriversV2
This method takes in a concept ID, store ID, workweek, startdate, enddate, starttime, endtime, volume amount, volume type, and a revenue center for the purpose of submitting forecasted volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The server side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change.

**Input (Literal)**
The inputs of this method are the arguments defined by the following table.

Argument | Type   | Description
----------------|--------|------------
concept         | int | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | int | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | int | Day formatted dd
Month           | int | Month formatted mm
Year            | int | Year formated yyyy

**Output (Literal)**
The outputs of this method are the arguments defined by the following table.

Argument               | Type   | Description 
------------------|--------|-------------
concept           | int | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum          | int | Numeric (integer) identifier for the store. Must be unique within the concept.
workweekStartDate | hsSimpledate | Start date of the work week
driverAmount      | int | Quantity of driver for interval expressed in the record
intervalStartTime | dateTime | The hour, minutes, and seconds corresponding to the start of the interval expressed in the record. Interval times are local to the store’s time zone. 
intervalEndTime   | dateTime | The hour, minutes, and seconds corresponding to the end of the interval expressed in the record. Interval times are local to the store’s time zone. 
intervalStartDate | hsSimpledate | The date corresponding to the start of the interval expressed in the record
intervalEndDate   | hsSimpledate | The date corresponding to the end of the interval expressed in the record
rvcId             | int | Numeric ID for the revenue center associated with the location within the restaurant
volumeType        | String | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”.

> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
   <soapenv:Header/>
   <soapenv:Body>
      <vol:setForecastDriversV2>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <workweekStartDate>
            <day>28</day>
            <month>8</month>
            <year>2017</year>
         </workweekStartDate>
         <driverData>
            <!--Zero or more repetitions:-->
            <item>
               <driverAmount>500</driverAmount>
               <!--Optional:-->
               <intervalEndDate>
                  <day>28</day>
                  <month>8</month>
                  <year>2017</year>
               </intervalEndDate>
               <!--Optional:-->
               <intervalEndTime>
                  <!--Optional:-->
                  <amPm>1</amPm>
                  <hours>6</hours>
                  <militaryTime>false</militaryTime>
                  <minutes>30</minutes>
                  <seconds>0</seconds>
               </intervalEndTime>
               <!--Optional:-->
               <intervalStartDate>
                  <day>28</day>
                  <month>8</month>
                  <year>2017</year>
               </intervalStartDate>
               <!--Optional:-->
               <intervalStartTime>
                  <!--Optional:-->
                  <amPm>1</amPm>
                  <hours>6</hours>
                  <militaryTime>false</militaryTime>
                  <minutes>0</minutes>
                  <seconds>0</seconds>
               </intervalStartTime>
               <rvcId>4</rvcId>
               <!--Optional:-->
               <volumeType>GUESTS</volumeType>
            </item>
         </driverData>
      </vol:setForecastDriversV2>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setForecastDriversV2Response xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>1</successCount>
         </return>
      </ns1:setForecastDriversV2Response>
   </soap:Body>
</soap:Envelope>
```





####setGuestCounts
This method takes in a concept ID, store ID, business date, date time, guest count and a revenue center for the purpose of submitting actual guest count drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains guest counts for a range of dates, corresponding to the start and end dates. The serveroside logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>businessDate</td><td>hsSimpleDate</td><td>Business date of transaction</td></tr>
<td nowrap>dateTime</td><td>dateTime</td><td>Date Time of the transaction</td></tr>
<td nowrap>guestCount</td><td>Int</td><td>Number of guests for the transaction</td></tr>
<td nowrap>rvcExtID</td><td>int</td><td>Numeric ID for the revenue center associated with the transaction</td></tr>
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
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>WSReturn object</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
   <soapenv:Header/>
   <soapenv:Body>
      <vol:setGuestCounts>
         <concept>3714</concept>
         <storeNum>98</storeNum>
         <guests>
            <!--Zero or more repetitions:-->
            <item>
               <!--Optional:-->
               <businessDate>2017-03-05T00:00:00</businessDate>
               <!--Optional:-->
               <dateTime>2017-03-05T06:41:00-05:00</dateTime>
               <guestCount>18</guestCount>
               <rvcExtId>1</rvcExtId>
            </item>
         </guests>
      </vol:setGuestCounts>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setGuestCountsResponse xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>1</successCount>
         </return>
      </ns1:setGuestCountsResponse>
   </soap:Body>
</soap:Envelope>
```

####setVolumeCounts
This method takes in a concept ID, store ID, business date, date time, volume amount, volume type, and a revenue center for the purpose of submitting actual volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The serveroside logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>businessDate</td><td>hsSimpleDate</td><td>Business date of transaction</td></tr>
<td nowrap>dateTime</td><td>dateTime</td><td>Date Time of the transaction</td></tr>
<td nowrap>rvcExtID</td><td>int</td><td>Numeric ID for the revenue center associated with the transaction</td></tr>
<td nowrap>volumeAmount</td><td>Int</td><td>Value of the volume count for the transaction</td></tr>
<td nowrap>volumeType</td><td>volumeType</td><td>Supported Volume Types (UPPERCASE): “TABLE”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS”</td></tr>
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
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>WSReturn object</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
<soapenv:Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:vol="http://services.hotschedules.com/api/services/VolumeService">
  <soapenv:Header/>
  <soapenv:Body>
    <vol:setVolumeCounts>
      <concept>1</concept>
      <storeNum>1</storeNum>
      <volumeData>
        <item>
          <businessDate>2014o10o05T00:00:00</businessDate>
          <dateTime>2014o10o05T06:41:00o05:00</dateTime>
          <rvcExtId>4</rvcExtId>
          <volumeAmount>1</volumeAmount>
          <volumeType>GUESTS</volumeType>
        </item>
      </volumeData>
    </vol:setVolumeCounts>
  </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setVolumeCountsResponse xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>1</successCount>
         </return>
      </ns1:setVolumeCountsResponse>
   </soap:Body>
</soap:Envelope>
```

####setVolumeCountsV3
All behavior is the same as setVolumeCounts, however you can use a string value in either UPPER or lower case for the volumeTypeName object.

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
<td nowrap>All</td><td></td><td></td></tr>
<td nowrap>concept</td><td>int</td><td>The identifier for the location's concept. Must be unique within the company. Contact HotSchedules if you're not sure about this value.</td></tr>
<td nowrap>storeNum</td><td>int</td><td>Numeric (integer) identifier for the store. Must be unique within the concept.</td></tr>
<td nowrap>businessDate</td><td>hsSimpleDate</td><td>Business date of transaction</td></tr>
<td nowrap>dateTime</td><td>dateTime</td><td>Date Time of the transaction</td></tr>
<td nowrap>rvcExtID</td><td>int</td><td>Numeric ID for the revenue center associated with the transaction</td></tr>
<td nowrap>volumeAmount</td><td>Int</td><td>Value of the volume count for the transaction</td></tr>
<td nowrap>volumeTypeName</td><td>volumeType</td><td>Supported Volume Types: "Sales", "Guests", "Tables", "Entrees", "Deliveries", "Products", "Transactions", "Plates", "KitchenUnits", "LBW", "Items", "TFE", "Member Check In".
</td></tr>
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
<td>All</td>
<td></td>
<td></td>
</tr>
<tr>
<td>return</td>
<td>wsReturn</td>
<td>WSReturn object</td>
</tr>
</tbody>
</table>


> **EXAMPLE:**

```
<?xml version="1.0" encoding="UTF•8"?>
   <soapenv:Body>
      <vol:setVolumeCountsV3>
         <concept>8436</concept>
         <storeNum>23</storeNum>
         <volumeData>
            <!--Zero or more repetitions:-->
            <item>
               <businessDate>2017-10-05T00:00:00</businessDate>
               <dateTime>2017-10-05T06:41:00-05:00</dateTime>
               <rvcExtId>4</rvcExtId>
               <volumeAmount>4</volumeAmount>
               <volumeType>
                  <volumeTypeName>GUESTS</volumeTypeName>
               </volumeType>
            </item>
         </volumeData>
      </vol:setVolumeCountsV3>
   </soapenv:Body>
</soapenv:Envelope>
```

> **EXAMPLE RESPONSE:**

```
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <ns1:setVolumeCountsV3Response xmlns:ns1="http://services.hotschedules.com/api/services/VolumeService">
         <return>
            <failCount>0</failCount>
            <success>true</success>
            <successCount>1</successCount>
         </return>
      </ns1:setVolumeCountsV3Response>
   </soap:Body>
</soap:Envelope>
```

#HotSchedules Community

Do you have questions, comments or suggestions on improviements to this documentation? Please subscribe to the HotSchedules Community.

[HotSchedules Community] (https://help.hotschedules.com/hc/en-us/community/topics)



