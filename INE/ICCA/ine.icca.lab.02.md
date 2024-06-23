```jsx
Lab Name: Manage Cloud Resources - Asure
Platform: INE
Lab No: 02
Exam: ICCA (INE Certified Cloud Associate)
```

## Explore the Google Cloud console

When you start the lab, you will be provided with the GCP's credentials. Use these to login on given login url.

After loggin in you will at the home screen of GCP.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/0a46223b-e773-4f14-9882-2c6369fa89d1)

From the top left menu, navigate to the `API & Services`. Open the `Enabled APIs & services` option.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/f3ac16b9-e054-4f64-a79c-2b236bfa11d3)

You can check all the APIs here, but for now open the `Compute Engine API`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/4.png)

Make sure the API is enabled, if not enable the API from here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/5.png)

Now from the top left menu of GCP, navigate to the `Cloud storage` service. Open the buckets here.

You can check out all the options related to the GCP buckets here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/7.png)

In the same manner navigate to the `VPC network service`. Open the `VPC networks`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/8.png)

You can note down all the options for the VPC networks in GCP from here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/9.png)

## Provision a Google Cloud virtual machine

For this requirement, you will provision a virtual machine. The details specific to a virtual machine are not critical - the goal is simply to provision a resource in Google Cloud.

Go to the top left menu, navigate to the `Compute engine` service. Open the `VM instanceS` here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/12.png)

Now click on `Create INSTANCE` button to create a VM instance on GCP.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/14.png)

Configure your VM instance as below:

- Name your VM instance as my-first-gcp-vm
- Use a region you prefer
- Select the series as E2
- Set the machine type to e2-micro
- You can check the cost for your instance at the right side.

You can check all the other options that GCP offers, click on `Create` to provision the VM instance.

![image[]()](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/15.png)

After a few time you will see that the instance is successfully deployed.

## Manage a Google Cloud virtual machine

For the next requirement, you will reboot your virtual machine.

Open your VM instance you just created on GCP. You can check the status for instance is `Running`. Navigate to the upper right corner at three dots.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/17.png)

Click on the dots, it will open a little menu here. Click on `Stop` to stop the VM instance.

GCP will prompt you to verify the action. Click on Stop to stop the instance. It will take some time to actually stop the VM.

Now after the VM is stopped, click on `START / RESUME` button to start the virtual machine.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-gcp/20.png)

GCP will prompt you to verify the operation, click on Start to start the VM.

_**Note:** At the time you are attempting this lab, GCP interface might change but the procedure will remain same._

## Delete a Google Cloud virtual machine

Open the VM instance on GCP, go to the upper right corner and navigate to 3 dots, just like you did for stopping the instance. Click on `DELETE` to delete the VM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/52cf5e2f-077d-4acd-914e-248bb7bee268)

GCP will prompt you to verify the action, click on `DELETE` to actually delete the VM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/a6cbbe18-c182-42d7-9bc5-06ecf8949b5c)

---
