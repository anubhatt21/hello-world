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
1. PDXC Onboarding Cloud Services

### Sub-flows Used: 
1. PDXC Onboarding Domain Creation/ConnectNow Sub-flow
2. PDXC Onboarding Load Client Data Sub-flow
3. PDXC Onboarding Cloud Business Services Sub-flow
4. PDXC Onboarding Client Catalog Config Sub-flow
5. a) PDXC Onboarding Cloud Services AWS Configuration Sub-flow
   b) PDXC Onboarding Cloud Services Azure Configuration Sub-flow
   
1.1  PDXC Onboarding Cloud Services
For either of the Cloud Services selected on the intake form, a standard Domain Creation sub-flow runs in order to facilitate DXC’s domain separation criteria. In this sub-flow, client’s unique domain and account are created for each client.

The sub-flow is created in compliance with OOSS standards. The first time this sub-flow runs in Dev, it makes a call to DMAR to check whether an account has already been created for that client for error handling. Once the Domain, Client Account, and Language records are created and validated it moves on to run the sub-flow in various environments - dev, sandbox and prod.
Failure at any step in the sub-flow is handled by a Catalog Task where steps or actions required to solve those errors are provided.

5.a) PDXC Onboarding Cloud Services AWS Configuration Sub-flow

After completing the first 4 sub-flows and depending on the Cloud Service selected on the intake form, if the client is being on-boarded for an AWS service, the sub-flow for AWS configuration will run. In this sub-flow, the three major steps are,
 
 - AWS Client Account Configuration 
 - AWS Credential Setup
 - AWS Client Discovery Setup
 
 * In the AWS sub-flow, the first step will be to provide the client’s AWS account. In the initial setup we have allowed up to 5 AWS accounts to be set up.
   - For each account, you will need the following three key values which are configured in Account Configuration and Credentials Setup steps
     - Account ID
     - Access Key ID
     - Secret Key ID
     
 * After the Account and Client Credentials set up, a scan takes place to set up a Discovery Schedule dependent on (DXC or AWS client’s requirements). In this sub-flow we have set Discover field on the discovery_schedule table to ‘Web Service’ to run Daily for 5 hours. 
   - Once the AWS configuration sub-flow is complete, the instance is ready for client hand-off. 
   
 * Onboarding and OD&T teams are involved in managing the manual tasks needed for validating errors that come from the workflows and then get directed to the concerned assignment groups and necessary action could be taken. 
 
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




