```jsx
Lab Name: Cloud Cost Management - GCP
Platform: INE
Lab No: 06
Exam: ICCA (INE Certified Cloud Associate)
```

## Estimate workload cost

For this task, you will estimate the cost to provision and operate specific resources in GCP. You can find the cost calculator at: https://cloud.google.com/products/calculator/.

1. On the `COMPUTE ENGINE` tab and under `Instances`, set number of instances to 1. We will use the free operating system Linux and select machine type as `e2-standard-4` having 4 virtual CPUs and 16 GB RAM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/c2f9dbfb-4cf4-4d01-b7ca-fe214851e3cf)

2. Select `SSD persistent disk` for boot disk type and set `100 GiB` for boot disk size.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/6cb15ae9-08df-4942-bd33-cfe83d20b4d7)

3. You can set the number of instances using ephemeral public IP to 1. After that click on `ADD TO ESTIMATE`. You can view the pricing on the right hand side.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/fe58d06f-c795-4c9e-a4ed-e65f3113c88c)

4. Next search for and go to `CLOUD SQL`. On the `CLOUD SQL FOR MYSQL` tab, set number of instances to 1 and select SQL instance type as `db-lightweight-2` having 2 virtual CPUs and 3.75 GB RAM. Also select `Enable High Availability Configuration` checkbox.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/f7cf78ba-a66a-4738-9a9b-08a50f59ab4c)

5. Set `100 GiB` SSD for storage and directly click on `DD TO ESTIMATE`. You can check the pricing on the right hand side.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/10599ff6-60ef-4382-a0a5-f4303bde2354)

6. Next search for and go to `CLOUD STORAGE`. Under `Cloud Storage` select `Standard Storage` as the storage class and type `1 TiB` for storage amount. Set Class A operations and Class B operations to 2 million per month.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1dc16394-469f-4e00-bba0-8133942b7f3a)

7. Under `Network Egress`, with the `Region` set to default, set inter-region, multi-region, and intra-region egress to `10 GiB`. After that click on `ADD TO ESTIMATE`. You can view the pricing on the right hand side.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/9cac2f24-2807-418b-a92c-0a941a9e393b)

8. You can check your total monthly estimate on the right hand side.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/ac077316-2525-4fef-b68b-aec2bc7d112c)

## Conclusion

In this lab you used the cost calculator provided by Google cloud to estimate the cost to implement a workload in GCP.

---
