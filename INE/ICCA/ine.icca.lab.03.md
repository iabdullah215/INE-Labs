```jsx
Lab Name: Manage Cloud Resources - Asure
Platform: INE
Lab No: 03
Exam: ICCA (INE Certified Cloud Associate)
```

## Explore the portal

When you start lab, you will be provided with the username and password. Use it to login to the azure portal. After loggin in to the portal you will taken to an empty resource group.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/2.png)

Go to the menu in top left corner of the azure portal. Open `All services` here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/3.png)

Click on the `Virtual machines` service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/4.png)

You can see all of your virtual machines here and also you can manage them with the options provided to you. Explore the azure VM service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/5.png)

In the same manner go to the all services and open `Storage accounts` service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/6.png)

Storage accounts blade will open up to you. Explore the storage accounts service blade here.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/3b80917a-265e-4203-bda3-73d00589293e)

If you scroll down a little in the all services, under databases you can find the `Azure Cosmos DB` service. Open the cosmos db service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/8.png)

Just like the `VMs and Storage` account, you can manage the `Cosmos DB` here.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/9.png)

Now go to the search bar and search for `Virtual networks`, Click on the `Virtual network` service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/10.png)

This will open up the blade for virtual networks. Explore the options for virtual networks.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/11.png)

Search for resource groups in the search bar and open the `Resource groups` service.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/12.png)

Click on the pin icon as highlighted below to pin this service to an azure dashboard.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/13.png)

You can use an existing dashboard or create a new dashboard. You may name it anything you like.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1958d5cc-69e2-41c3-9d72-da3d40618726)

Go to the top left corner of azure portal, just over the all service, you may find Dashboard. Click on it to open the dashboard.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/5f023563-eacf-4450-98a9-1ef1afccf48d)

You can use the dropdown highlighted below to switch the dashboards. You may see the resource groups service is pinned to our new dashboard.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/391d2e59-0929-4e95-a4a0-436221a1c505)

## Provision Azure resources

For this requirement, you will provision two resources - a virtual machine and a storage account. You can run your custom compute workloads on the virtual machine. The storage account is a cloud storage space. You will primarily use standard options for each - the goal is to become familiar with the process of provisioning resources, not these two resources in particular.

## Provision the Azure virtual machine

Go to the home screen of azure portal, you can do that by clicking the `Microsoft azure` icon.

Click on `Create a resource`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/17.png)

Here you will find multiple quick starts. Click on `Create` under the `Ubuntu server`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/4b91a32c-cae9-410a-b54a-6209a29000a9)

Configure your VM as below.
- Use the resource group which is assigned to you.
- Name you virtual machine as myFirstAzureVM.
- Use any region you prefer.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/19.png)

Under the size of VM, click on `See all sizes` to select a size for your VM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/a016c5a2-70a1-4e39-8ab7-ec7c0a1b203c)

Here you can select the size for your VM, Select `B2s` size, and click on `Select`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/21.png)

Leave everthing as it is. You may explore all the option by clicking Next. But for this task, you can just click on `Review + Create`.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/22.png)

Azure will now validate the config for your VM. If you have configured everything properly, you will `Validation passed`. Click on `Create` to provision the VM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/d107d475-e002-440c-8ff4-e60637c1d80b)

A pop will appear to you for the key pair. Click on Download to download the key pair.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/89a49581-b1ad-4d27-9c4f-e685c4b1d5c9)

