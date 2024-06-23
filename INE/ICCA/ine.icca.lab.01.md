```jsx
Lab Name: Manage Cloud Resources - AWS
Platform: INE
Lab No: 01
Exam: ICCA (INE Certified Cloud Associate)
```

## Explore the console

_**Note:** By the time you are solving this lab, interface of the AWS might change. But the procedure will remain same._

When you start the lab, you will be provided with the credentials. Click on login url and the use username and password for login.

After loggin in, go to the right upper corner and click on region drop down and select your prefered region.

![image1](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/3.png)

Now go to the `services` on the upper hand corner of the AWS console. You can find out all the services here.

![image2](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/6.png)

We will navigate to these three services.

- EC2
- S3
- Athena

Click on the service name to access these services.

![image3](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/7.png)

Upon clicking on `EC2`, you will see all the informations and options for your `EC2` instances.

![image4](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/8.png)

Click on `S3` will show you all the options for `S3` buckets and in same manner you can see the options for `Athena`.

## Provision AWS resources

For this requirement, you will provision two resources - an EC2 instance and a S3 bucket. The EC2 instance is a virtual machine that you can run compute workloads on. The S3 bucket is a cloud storage space. You will primarily use standard options for each - the goal is to become familiar with the process of provisioning resources, not these two resources in particular.

Go to all the services and click on `EC2`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/12.png)

This will open the page for EC2 service. Click on `Launch instance` to start creating an EC2 instance.

![iamge](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/13.png)

Select the `Amazon Linux AMI` as the image for EC2 instance.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/14.png)

Select instance type as `t2.micro`, it's a free tier type from _t2_ family.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/15.png)

Scroll down to the `Key pair` and click on `Create new key pair`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/16.png)

Give your key pair a name as demo and click on Create key pair.

This will create a key pair and the pem file will also be downloaded.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/17.png)

You can checkout the networks settings, leave all these to default. 

Check for the storage settings also, leave these to default also.

Scroll all the way up to the `Name and tags` and give it a name as `myFirstEC2`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/20.png)

At the right side of all the settings, you can see the summary for your EC2 instance. Click on `Launch instance` to start provisioning the EC2 instance. After a few seconds you will see the success message, that means EC2 instance is provisioned.

## Provision the S3 bucket

Go to the services and click on `S3`.

Here somewhere on the page you will see an option to `Create bucket`, click on it.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/24.png)

Give a unique name for the bucket and set a region of your choice.

By default, you can see that public access is blocked for this bucket. Leave it as it is.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/26.png)

You can go and check for all the advance settings for the bucket. Don't changes anything.

Click on `Create bucket` to provision the S3 bucket.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-aws/27.png)

After a few seconds you will see our bucket is created.

_**I have skipped the Managing resources and terminating resources part as it was very easy.**_
