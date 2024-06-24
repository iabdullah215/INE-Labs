```jsx
Lab Name: Cloud Cost Management - AWS
Platform: INE
Lab No: 04
Exam: ICCA (INE Certified Cloud Associate)
```

## Estimate workload cost

For this task, you will estimate the cost to provision and operate specific resources in AWS. You can find the cost calculator at: https://calculator.aws/#/.

1. Click on `Create estimate`.
2. Search for EC2 and click on `Configure` for `Amazon EC2`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/6c14ff23-4095-4749-ab62-1390c9b0f3b3)

3. Under `EC2 instance specifications`, we will use the default settings i.e. an instance with Linux operating system, 4 virtual CPUs and 16 GiB of RAM.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/f2c99fd9-c6e4-44db-9e4c-cf9b272a02b3)

4. Under `Amazon Elastic Block Storage (EBS)`, we will use the selected `General Purpose SSD (gp2)`. Type `100 GB` for storage amount. After that click on `Save and add service`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/aa7ee128-893c-4c20-92f1-7ee9f13a35e1)

5. Next, search for MySQL and click on `Configure` for `Amazon RDS for MySQL`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/31cbcc0b-da39-4183-bce0-230596388dec)

6. Under `MySQL instance specifications`, we will select one `db.t3.small` instance having 2 virtual CPUs and 2 Gib of RAM.

![image](https://assets.ine.com/content/labs/azure-course-labs/cloud-cost-management-aws/6.png)

7. Under `Storage`, we will use the selected `General Purpose SSD (gp2)`. Type `100 GB` for storage amount. After that click on `Save and add service`.

![image](https://assets.ine.com/content/labs/azure-course-labs/cloud-cost-management-aws/7.png)

8. Next search for `S3` and click on `Configure` for `Amazon Simple Storage Service (S3)`.
9. Under `Select S3 Storage classes and other features` , we will use the selected `S3 Standard` tier and `Data Transfer` service.

![image](https://assets.ine.com/content/labs/azure-course-labs/cloud-cost-management-aws/9.png)

10. Under `S3 Standard`, type `1 TB per month` for storage. Type `2000000` for amount of PUT, COPY, POST, LIST requests to S3 Standard. Type `2000000` for amount of GET, SELECT, and all other requests from S3 Standard. You can set other amounts to 0.

![image](https://assets.ine.com/content/labs/azure-course-labs/cloud-cost-management-aws/10.png)

11. Under `Data Transfer`, you can set Inbound Data Transfer details as you want. For Outbound Data Transfer details, select Internet and enter `10 GB per month` for amount. After that click on `Save and view summary`.
12. You can check the estimated monthly cost for each service, your total estimated monthly cost and total 12 months cost as well.

![image](https://assets.ine.com/content/labs/azure-course-labs/cloud-cost-management-aws/12.png)

## Conclusion

In this lab you used the cost calculator provided by AWS to estimate the cost to implement a workload in AWS.

---
