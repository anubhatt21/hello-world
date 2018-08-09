## PDXC Getting Started with Customer Onboarding Automation

As part of the client on-boarding offering for cloud services, a number of sub-flows are built to help automate a modular and non-duplicate process for DXC. 

### Required Parameters for Intake

To facilitate cloud services offering for clients, a few details are required from the client. The data captured on the intake form with those details then triggers the necessary automated steps to get the clients on-boarded. 

* Values needed on the form
  - Cloud Service:
    - Name of the Cloud Service client is being on-boarded for
    - Type : Select Box 
    - Options: 'AWS' or 'Azure'
    
  - Company Name : 
    - Name of the client being on-boarded
    - Type: Single Line Text
    
  - Salesforce ID: 
    - Salesforce ID of the client 
    - Type: Single Line Text 

  - Stock Ticker: 
    - Client’s Stock Ticker 
    
  - Contract ID: 
    - Contract ID for that client

  - Company Description:
    - Short Description for client’s company or any additional information

  - Company Address
    - Type: Single Line Text [All]
    - Street:
    - City
    - State/Province
    - Zip/Postal Code
    - Country

  - User Information: List of users who would utilize the cloud service assigned from client’s company. Currently the form has ability to add three users on the form. 
    - Type: Single Line Text [All]
    - First Name:
    - Last Name:
    - Department:
    - Email: Email address of the users
      - Type: Email
      
  - Administrators: Administrators who would utilize the cloud service from client’s company. Currently the form has the ability to add two admins on the form using their email address. 
    - Email- Type: Email - Email address of the admins 
    
### Main Workflow:
PDXC Onboarding Cloud Services
![screen shot 2018-08-09 at 11 25 17 am](https://user-images.githubusercontent.com/18390433/43913727-74375eea-9bcb-11e8-9b4c-6144a3306d21.png)

### Sub-flows Used: 
1. PDXC Onboarding Domain Creation/ConnectNow Sub-flow

 For either of the Cloud Services selected on the intake form, a standard Domain Creation sub-flow runs in order to facilitate
 DXC’s domain separation criteria. 
  - Vendor/Manufacturer Validation: Validate that the company being onboarded is not a Vendor or a Manufacturer.
  - MDM Validation: Making sure the Stock Ticker is unique and does not have another client with the same Stock Ticker ID.
  - Manual Task to Validate MDM accounts: A manual task is added to ensure the information for MDM acccounts is accurate.
  - Operations Approval validation: Successful account creation is validated via Operations Approval.
  - Domain, Company and Language Creation/Validation

 Failure at any step in the sub-flow is handled by a Catalog Task where steps or actions required to solve those errors are
 provided.

2. PDXC Onboarding Load Client Data Sub-flow

 Once the domain, company and language records are created and validated, the next step of the workflow sets up foundational
 data for that client. 
  - Validate Inputs: This step ensures the data returned from the previous activity is true.
  - Department and Location data: This step is responsible for inserting new entires in the Department and Location tables for
  the company. 
  - Users and Groups:  New Customer User and Admin records are created.
  - Give Admins Domain Visibility: Admins are added to Domain Visibility Group. 

3. PDXC Onboarding Cloud Business Services Sub-flow

 Once the foundation data is loaded and depending on the Cloud Service selected on the Intake Form,the next step is to add
 services.
  - Business Services: This activity takes a list of business service names and creates new records in the Business Services
  table for the onboarding client
  - Type Relationships: It then creates the Type Relationships.
  - Assignment Rules: Visbility and Assignment rules for those new services are created. 
  - End User Group: The End User Group responsible for these Business Services is also created at this point. 

4. PDXC Onboarding Client Catalog Config Sub-flow

 This workflow is then responsible for creation of company styling record in Customer company. 
  - Company Stylings Update: The Company Stylings are updated as per the client company.
  - Record Producers and Catalog items: New records are added, Catalog items are passed, and made Available for Companies.
  
5. a) PDXC Onboarding Cloud Services AWS Configuration Task

   b) PDXC Onboarding Cloud Services Azure Configuration Task (Handled by a different team)
  
 ### List of Errors handled using **Catalog Tasks**: Manual Intervention 
 
Catalog tasks have been added at every failure step to ensure intervention and investigation from associated assignment groups. 
  1. Domain Creation Failure – Remediate Failure Catalog Task
  2. Rejected Approval – Remediate Failure Catalog Task
  3. Client Error – DMAR Client Validation Failed Catalog Task
  4. Account Error – Client with Existing Accounts Catalog Task
  5. Load Client Data Failure – Data Load Errors Catalog Task
  6. Cloud Business Services Failure – Business Service Errors Catalog Task
  7. Client Catalog Configuration - Catalog Configuration Errors Catalog Task
  
#### Note : 
The workflow then can be leveraged for other onboarding offerings. 




