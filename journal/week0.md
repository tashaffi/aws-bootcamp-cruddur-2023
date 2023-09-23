# Week 0 — Billing and Architecture

[Link Text](#destroy-your)

### Destroy Root Account, Set MFA, IAM Role

Steps for creating IAM account:
- Go to Identity and Access Management (IAM) dashboard
- Go to IAM > Users
- Go to `Create user`

I created an IAM user called `Tash IAM` with admin access. 

![IAM User](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/IAM%20user.png)

To enable MFA, go to IAM > Users > Tash_IAM, in the Summary section there will be options to enable MFA.
I used an authenticator app but there are other options. 

IAM > Users > Tash_IAM > Assign MFA device

![IAM MFA](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/TASH_IAM_MFA.png)


### Use EventBridge to hookup Health Dashboard to SNS and send notification when there is a service health issue.


### Review all the questions of each pillars in the Well Architected Tool (No specialized lens)
 
### Conceptual and logical diagram

[Conceptual Diagram Lucid Chart](https://lucid.app/lucidchart/0b5e96b6-adc4-451f-a5c4-e2219873b7dc/edit?invitationId=inv_2621bb6b-44d1-46ad-a9d2-12e63b0034d1&page=0_0#)

Screenshot of conceptual diagram:

![Conceptual Diagram](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Conceptual_Diagram.png)

[Logical Diagram Lucid Chart](https://lucid.app/lucidchart/64aead20-ef1b-473b-9d23-f3fe0867ebf9/edit?beaconFlowId=EFED65FF2B3FFEC5&invitationId=inv_89f06a26-4280-4840-8849-e38ca31c4f07&page=0_0#)

Screenshot of logical diagram:

![Logical Diagram](https://github.com/tashaffi/aws-bootcamp-cruddur-2023/blob/main/journal/Assets/Logical_Diagram.png)

### Research the technical and service limits of specific services and how they could impact the technical path for technical flexibility. 


### Open a support ticket and request a service limit
