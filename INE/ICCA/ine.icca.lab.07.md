```jsx
Lab Name: Provision a Compute Instance - AWS
Platform: INE
Lab No: 07
Exam: ICCA (INE Certified Cloud Associate)
```

## Provision an AWS EC2 instance

- Use your credentials and login to the AWS account.
- Start searching for the EC2 in the search box.
- Select `EC2 instance`.
- Click on _Instances_ and click on `Launch instances`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/1f04e544-824d-4efc-bb02-74e91e843d6e)

- Name: `lab-vm`
- Scroll down to _Application and OS Images_, Choose Amazon Linux as shown in image.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/308b66da-5494-4755-966d-a234eff98451)

- Instance type to be `t2.micro`.
- Click on `Create new key pair`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/299a3521-1f71-4cd5-90f5-f9344ce45654)

- A window will be popped up, now create a key pair with name `lab-vm-key-pair`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/3c38da5e-5449-4d5f-a4eb-c356a18355e9)

- Go to _Network Settings_ and click on `Edit` to add `Security group`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/72b58e9e-8913-44d3-9d6a-1d15f42ba442)

- Click on `Add security group rule`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/ec44036f-1cf1-4aad-a52c-c1bd6a6c70ac)

- Type: `HTTP` and Source Type: `Anywhere`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/4e7455b6-322d-44de-8248-1a072c2974da)

- Go to summary and click on `Launch instance`.
- Once, it is success then click on `View all instances`.
- Check for the `Instance State` Status, refresh the page to update the status. Click on the `Instance ID` to open it.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/a7006230-fed3-4a0b-bcd0-2615eb0e07ad)

- Click on `Connect`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/293a4720-3cc8-49aa-aa6c-588c9b03f053)

- Click on the tab `EC2 instance Connect` and press the button `Connect`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/4c203172-cdba-4e28-9a2b-e2e71606cc47)

- A new tab will be opened on the browser. So, run the below command in the terminal.

```console
sudo amazon-linux-extras install nginx1
```

- Press: `y` to continue.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/52dc59d1-0235-4a57-aeb7-b82c0dc45261)


- Now start `nginx` by running the below command.

```console
sudo systemctl start nginx
```

- Now verify it by running the below command.

```console
curl localhost
```

- Now, logout from terminal.

```console
exit
```

- Come back to the summary page and copy the External `Public IPv4 address`.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/ef4cbc05-e420-4124-8404-dfc3c8aad4a0)

- Open a new browser tab and navigate to the IP address - Verify that a welcome page is returned.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/dc4ac607-430c-44f3-a07e-1e9eb9198cfd)

- Terminate the insance.

![image](https://github.com/iabdullah215/WriteUps/assets/121729444/958bb803-e72d-4774-8916-f70e716df6ae)


_**Successfully we have completed our Task.**_

---
