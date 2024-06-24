```jsx
Lab Name: Cloud Cost Management - Asure
Platform: INE
Lab No: 05
Exam: ICCA (INE Certified Cloud Associate)
```

## Estimate workload cost

For this task, you will estimate the cost to provision and operate specific resources in Azure. You can find the cost calculator at: https://azure.microsoft.com/en-us/pricing/calculator/.

1. Let's add the products to include in our estimate. In the Popular section you can see `Virual Machines`. Click on it to add. In the Databases section, click on `Azure Database for MySQL` to add it. Similarly click on `Storage Accounts` (also available in the Popular section) to add it as well.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1cc873ee-0695-4c2c-b911-616059be5380)

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/c84c689d-9bcd-4e53-9d7e-15367c1e29ab)

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/6d183b28-811d-497c-b0ce-b06f05a26eaa)

2. Scroll down the page. Under Virtual Machines, select operating system as `Linux`. Select `D4 v4` instance that includes 4 virtual CPUs and a minimum RAM of 16 GB.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1e0cfbdb-a749-47ba-b26b-9477cb9e3dbe)

3. Under Managed Disks, select `Standard SSD` tier and 1 disk with `128 GiB` disk size. Under Storage Transactions, we already have 100 units listed by default, we will use this.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/bc6f568a-6ab4-43ca-90f9-34826974285b)

4. Under Azure Database for MySQL, select the `Basic` tier, and the machine size with 2 processors.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/078a780f-c1e5-47e6-8172-d7b41605cfac)

5. Use `100 GiB` for Storage.
6. Under Storage Accounts, select the `Standard` tier and use `1 TB` for capacity.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/94ea18e7-6292-465b-aeaf-8fc0f5c51983)

7. For Write operations and Read operations use the value - `200` (x 10,000). For Data Retrieval use `10 GB`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/48527bf1-6d4d-4ed1-b6ea-567ba061a17c)

8. Scroll down further to check your total Estimated monthly cost.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/7700d18b-56ce-4282-8555-b18f5f9916fd)

## Conclusion

In this lab you used the cost calculator provided by Azure to estimate the cost to implement a workload in Azure.

---
