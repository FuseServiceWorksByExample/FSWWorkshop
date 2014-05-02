Fuse Service Works Workshop
===========================

This repo will be updated each week to coincide with the 5 blogs.

BLOG 1 - Environment Setup - 

1. Download the product at http://www.jboss.org/products/fsw.html
2. Install the product according to the instructions at http://www.jboss.org/products/fsw.html
3. Setup the Database
3a. Launch the H2 db and console via the h2 jar in your FSW install 
java -jar modules/system/layers/base/com/h2database/h2/main/h2-1.3.168-redhat-2.jar 
3b. At the login screen for the H2 console, use the following values. $FSW_HOME is where you have installed FSW; be sure to replace this with the actual directory for your installation.
JDBC URL: jdbc:h2:file:$FSW_HOME/jboss-eap-6.1/standalone/data/h2/customer;mvcc=true
User Name : sa
Password : sa
3c. In the console, create a table:
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
3d. And insert some test data:
INSERT INTO CUSTOMER VALUES 
    ('800559876', 'Joe', 'Deeppockets-existing', '345 Pine Ave', 'Springfield', 'MO', '65810', '1966-07-04', 14000.40, 22000.99);
INSERT INTO CUSTOMER VALUES 
    ('610761010', 'Sally', 'Shortchange-existing', '456 Larch Lane', 'Springfield', 'MA', '99999', '1966-08-05', 9100.10, 2750.75);
INSERT INTO CUSTOMER VALUES 
    ('680777098', 'Barbara', 'Borderline-existing', '567 Poplar Pkwy', 'Worcester', 'MA', '01604', '1976-09-06', 300.41, 11.01);
3e. Add the following datasource definition to standalone-full.xml:
<datasource jndi-name="java:jboss/datasources/CustomerDS" pool-name="CustomerDS" enabled="true" use-java-context="true">
    <connection-url>jdbc:h2:file:${jboss.server.data.dir}/h2/customer;mvcc=true</connection-url>
    <driver>h2</driver>
    <security>
        <user-name>sa</user-name>
        <password>sa</password>
    </security>
</datasource>
4. Setup JMS
4a. Add the JMS user
${FSW_HOME}/bin/add-user.sh
  - Application User
  - Application Realm
  - Username : guest
  - Password : guestp.1
  - Roles : guest
4b. Start the server:
bin/standalone.sh -c standalone-full.xml
4c. In a separate terminal window, add a JMS queue:
bin/jboss-cli.sh --connect --command="jms-queue add --queue-address=LoanIntake --entries=LoanIntake"

BLOG 2 - Lab Introduction

BLOG 3 - Lab 1 Switchyard

Blog 4 - Lab 2 Service Lifecycle Management

Blog 5 - Lab 3 Business Activity Monitoring

Version 1 Fuse Service Works V6
