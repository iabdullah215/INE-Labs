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

It will take some time to deploy the virtual machine, you can move to next task in mean time.

## Provision the Azure storage account

Go to the home screen of azure portal and click on `Create a resource` just like you did for the virtual machine.

Under storage accounts, click on `Create` to create a storage account.

![image](https://assets.ine.com/content/labs/azure-course-labs/manage-cloud-resources-azure/25.png)

Configure your storage account as below:

- Use the resource group which is assigned to you.
- Give your storage account a unique name.
- Choose a region as you like.
- Leave everything else as it is, you can click on `Next` to check out all the options for storage account.

But for this task, click on `Review` to provision the storage account.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/3b17a52a-a8a1-4c50-86a4-5d8b78194486)

In review section you can check all the config for your storage account, click on `Create` to provision the storage account.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/5c88051d-3dd3-4f5d-8115-8db19209e434)

## Manage Azure resources

For this requirement you will navigate to the management blade for the virtual machine and restart the instance. You will also add a container to the storage account.

## Restart the Azure virtual machine

You can go to the blade for the virtual machine service from home screen of portal, all services or you can just search for the service. You can do however you like it, open the Virtual machines service.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/f1328db5-3a10-4c91-9ff0-53a204950203)

Here you will see that there is a virtual machine we created earlier. Click on it to open the azure blade for this virtual machine.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/fb8e5ed9-8ac2-4f2f-bf38-576066f8ef79)

You will see an option to restart the virtual machine. Click on it.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/b8f293a6-b3ca-45b3-a9af-34cb3bc59315)

Azure will prompt you for the confirmation, click on `Yes` to restart the VM.

## Add a storage container

Open the service blade for storage account from any of the ways mentioned earlier.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/add17d1f-88cd-4f8b-b8bf-0d7d70ba2279)

You will see the storage account we created earlier, click on it to open the azure blade for this storage account.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/55c281a0-d4eb-4fc5-a0b8-92c612e4719d)

Here go to the `Containers` and click on `+ Container` to create a container in this storage account.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/56a0bb55-e1f1-4460-a481-872e84bcf571)

Name this container as public and allow public access to `Blob`. Click on `Create` to create the container.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/88f7166d-4da8-43b2-8edf-8f051eaddf7e)

You can see the public container is created.

## Delete Azure resources

Go to the azure resource group which is assigned to you.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/bb21973b-d9fa-434e-a1dc-00e23474d4ad)

Select all the resource which are created there and click on `Delete` option as highlighted below.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/3c38e808-e774-4f96-960c-94743d7e9c5a)

Type `ye`s in the confirmation box and you can also check the box for `force delete`. Click on `Delete` button to delete all the resource you created.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/729ca02f-f836-4d73-80f3-761b9adcf47b)

---
