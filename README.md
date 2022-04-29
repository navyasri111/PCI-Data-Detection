# PCI DATA DETECTION
************

# ABOUT

PCI stands for Payment Card Industry. Data that relates to Payment Card Industry and is unique for a person comes under PCI data. PCI DSS was launched on September 7, 2006, to manage PCI security standards and improve account security throughout the transaction process. The Payment Card Industry Data Security Standard (PCI DSS) is a set of requirements intended to ensure that all companies that process, store, or transmit credit card information maintain a secure environment.

In this project, we have built a website that takes input from users and helps to segregate the PCI and PCI-free information and stores them accordingly.

We have built the whole backend and frontend of the website using Amazon Web Services such as Textract for extracting text from images, Comprehend for PII entities identification, SES for email service, S3 for storage service, Cloud9 for frontend development, Cognito for authentication and authorization, Lambda a serverless function for the actual running of project.

Firstly, users need to register/login to our website. After login user can upload the Attachments of different input formats such as images formats (jpg, jpeg, png, gif, base64 encrypted form), and Pdf format. It extracts the text from all types of inputs and detects the PCI entities if present. In Amazon itself, the PCI and PCI-free data will get separately stored. Also, the admin receives an email regarding the information about the attachment (what PCI data is present).

This helps reduce the PCI compliance and audit cost, as we will be able to move the PCI zone to the non-PCI zone. The security that a PCI zone requires is of level-3 whereas for PCI-free the security oflevel-1 is enough. So, we can also reduce the security building cost.


## About
This repository contains the Open Source Software to demonstrate how to build a simple WebApp to users upload files to S3.  

### Built With

- [AWS Amplify Framework](https://docs.amplify.aws/)
- [Amazon S3](https://aws.amazon.com/s3/)
- [Amazon Cognito](https://aws.amazon.com/cognito/)
- [AWS UI](https://github.com/aws/awsui-documentation)
- [Node.JS](https://nodejs.org/en/)
- [React](https://reactjs.org/)
- [AWS Colud9](https://aws.amazon.com/cloud9/)
- [AWS TEXTRACT](https://aws.amazon.com/textract/)
- [AWS COMPREHEND](https://aws.amazon.com/comprehend/)
- [AWS SNS](https://aws.amazon.com/sns/)
- [AWS SES](https://aws.amazon.com/ses/)
- [AWS LAMBDA](https://aws.amazon.com/lambda/)
- [AWS LAMBDA LAYERS](https://aws.amazon.com/lambda-layers/)

### FRONT END : Simple S3 Web Application to upload multiple files


## Getting Started

First install AWS Amplify CLI
`npm install -g @aws-amplify/cli`

Inside the project folder, initialize Amplify:
`amplify init`
> Project name example: s3-uploader-ui

Add the authentication component
`amplify add auth`

Add the storage component
`amplify add storage`

> Select: Content (Images, audio, video, etc.)
> 
> Provide a label for this category or use the suggested one from the wizard.
>
> Select the option create/update from the list of actions

Add the application hosting
`amplify hosting add`

> Select Amazon CloudFront and S3. Define a new unique bucket name or use the suggested one.

Now, you can build the web app (front-end)

```bash
npm install
amplify push
amplify publish
```

The output of the `amplify publish` if all the deployment was done correctly is a URL
This URL is the web application URl where you can open from the browser to access your application.
By default, the front-end come with the sign-up UI disabled. To enable the sign-up UI you need to change the file: `App.css`

Comment or remove the following block:

```css
.amplify-tabs {
display: none;
}
```
> After this change you need to re-run `amplify publish`

Comming into the pipeline after the attachments

************

# IMAGES

1. After the login the attachments are being sent into the bucket
2. Then after the attachments are being uploadeda a trigger is being called where the lambda will work automatically.
3. Here the lambda will divide the images and non-image datatypes 
4. Now images will be stored in one folder and the remaining will be stored in another folder in a different attachments bucket.
5. As soon as the attachments eing stored in  different bucket the same attachment will be deleted in the previous bucket as it is waste of space.
6. Now two different triggers will be present in this bucket one for the images and the another for non-images folder.
7. The Images trigger will first take the images and then check if the image is of base64 encoded
8. If encoded then it will decode into normal format.
9. Then agan they will be of gif anf non gif formats.
10. gif fomats will be changed into non-gif forrmats.
11. Here all the images will now be sent into the AWS Textract where it will extract all the text from the images.
12. Next the extractd text will be sent to AWS comprehend where it will detect all the PII entities.
13. Out of the PII entities we will detect if we are having any PCI data.
14. Then it will send an email to the admin regarding the attachment and the details it is being found.
15. both the PCI and non-PCI data will  be stored separately.

**********

# NON- IMAGES

1. After the login the attachments are being sent into the bucket
2. Then after the attachments are being uploadeda a trigger is being called where the lambda will work automatically.
3. Here the lambda will divide the images and non-image datatypes 
4. Now images will be stored in one folder and the remaining will be stored in another folder in a different attachments bucket.
5. As soon as the attachments eing stored in  different bucket the same attachment will be deleted in the previous bucket as it is waste of space.
6. Now two different triggers will be present in this bucket one for the images and the another for non-images folder.
7. The NON-Images trigger will first take the PDF and then repeat the textract for each page
11. Here all the pages will now be sent into the AWS Textract where it will extract all the text from the images.
12. Next the extractd text will be sent to AWS comprehend where it will detect all the PII entities.
13. Out of the PII entities we will detect if we are having any PCI data.
14. Then it will send an email to the admin regarding the attachment and the details it is being found.
15. both the PCI and non-PCI data will  be stored separately.

#####################################################################################################

### Prerequisites

To build this solution you must have:
- AWS account
- Permissions to create resources in the AWS account
- Node.js 16.x or higher
- Python

################################################################################
 
