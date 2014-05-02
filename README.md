Fuse Service Works Workshop
===========================

This repo will be updated to coincide with 5 blogs from ossmentor.com

[x] BLOG 1 - Environment Setup - 

Step 1. Download Fuse Service Works (FSW) from http://www.jboss.org/products/fsw.html  
Step 2. Install FSW according to the instructions at http://www.jboss.org/products/fsw.html  
Step 3. Setup the Database  
  
Launch the H2 db and console via the h2 jar in your FSW install  
```
java -jar modules/system/layers/base/com/h2database/h2/main/h2-1.3.168-redhat-2.jar  
```
At the login screen for the H2 console, use the following values. $FSW_HOME is where you have installed FSW; be sure to replace this with the actual directory for your installation.  
```
JDBC URL: jdbc:h2:file:$FSW_HOME/jboss-eap-6.1/standalone/data/h2/customer;mvcc=true  
User Name : sa  
Password : sa  
```
In the console, create a table:  
```sql
CREATE TABLE CUSTOMER(  
    SSN VARCHAR(11) PRIMARY KEY,  
    FIRSTNAME VARCHAR(50),  
    LASTNAME VARCHAR(50),  
    STREETADDRESS VARCHAR(255),  
    CITY VARCHAR(60),  
    STATE VARCHAR(2),  
    POSTALCODE VARCHAR(60),  
    DOB DATE,  
    CHECKINGBALANCE DECIMAL(14,2),  
    SAVINGSBALANCE DECIMAL(14,2));  
```
And insert some test data:  
```sql
INSERT INTO CUSTOMER VALUES   
    ('800559876', 'Joe', 'Deeppockets-existing', '345 Pine Ave', 'Springfield', 'MO', '65810', '1966-07-04', 14000.40, 22000.99);  
INSERT INTO CUSTOMER VALUES   
    ('610761010', 'Sally', 'Shortchange-existing', '456 Larch Lane', 'Springfield', 'MA', '99999', '1966-08-05', 9100.10, 2750.75);  
INSERT INTO CUSTOMER VALUES   
    ('680777098', 'Barbara', 'Borderline-existing', '567 Poplar Pkwy', 'Worcester', 'MA', '01604', '1976-09-06', 300.41, 11.01);  
```
Add the following datasource definition to standalone-full.xml:  
```xml
<datasource jndi-name="java:jboss/datasources/CustomerDS" pool-name="CustomerDS" enabled="true" use-java-context="true">  
    <connection-url>jdbc:h2:file:${jboss.server.data.dir}/h2/customer;mvcc=true</connection-url>    
    <driver>h2</driver>  
    <security>  
        <user-name>sa</user-name>  
        <password>sa</password>  
    </security>  
</datasource>  
```
Step 4. Setup JMS  
  
Add the JMS user  
```
${FSW_HOME}/bin/add-user.sh  
Application User  
Application Realm  
Username : guest  
Password : guestp.1  
Roles : guest  
```
Start the server:  
```
bin/standalone.sh -c standalone-full.xml  
```
In a separate terminal window, add a JMS queue:  
```
bin/jboss-cli.sh --connect --command="jms-queue add --queue-address=LoanIntake --entries=LoanIntake"  
```
  
Step 5. Download JBoss Developer Studio 7.1 from https://www.jboss.org/products/devstudio.html  
Step 6. Install JBDS according to the instructions at https://www.jboss.org/products/devstudio.html  
Step 7. Download JBoss Integration Stack 4.1.4 from http://tools.jboss.org/downloads/jbosstools_is/kepler/4.1.4.Final.html  
Step 8. Install JBIS according to the instructions at http://tools.jboss.org/downloads/jbosstools_is/kepler/4.1.4.Final.html  
  
Now your environment is ready for the next blog.  

[ ] BLOG 2 - Lab Introduction (5/5/2014) 
  
[ ] BLOG 3 - Lab 1 Switchyard  (Code added; 5/12/2014)
  
[ ] BLOG 4 - Lab 2 Service Lifecycle Management (Code added; 5/19/2014)
  
[ ] BLOG 5 - Lab 3 Business Activity Monitoring  (Code added; 5/26/2014)
  
Version 1 Fuse Service Works V6  
