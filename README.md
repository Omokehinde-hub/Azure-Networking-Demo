# Azure-Networking-Demo
This repository was created to demonstrate VNET in Azure 

## 1.To start we need to create a resource group. Lets name it Demo

![Image](https://github.com/user-attachments/assets/2219f3d3-2767-4832-a984-ec51d64c360a)

## 2.Then we proceed to create a Virtual Network. For this , use the resource group that we created above

![Image](https://github.com/user-attachments/assets/108acb69-0429-41b0-a5e1-00dcc1b36283)

## 3.Then switch to the security tab, Check Azure bastion, name it . This will be used to connect to the VM later on.
- Also check Azure firewall . This is done to restrict access to the VM to only authorized people.
  
![Image](https://github.com/user-attachments/assets/2344254c-0171-4d07-a2c5-e524132a1df1)

## 4.Then proceed to the Ip address tab, for this example we want our subnet ip address to be 65,536 so we will leave the CIDR range at 16. 
- Note this can be changed by clicking on 16 and selecting the CIDR range you prefer. Also we will leave the default names as they are, this can also be changed by clicking on the pen icon.
  
![Image](https://github.com/user-attachments/assets/e0164322-5fde-4d80-9c22-821346528c34)

## 5.After that review and create and wait for it to deploy successfully

![Image](https://github.com/user-attachments/assets/a8f090fa-cf2f-4463-8216-69620b5f28f0)

## 6.Then proceed to create a Virtual machine. Make the resource group the same as the VNET i.e Demo
- Also name the VM , here we will use nginx-web
  
![Image](https://github.com/user-attachments/assets/a583282d-bbe6-4cf6-ab3c-7345abb0a255)

## 7.Continue downward , for the authentication type , enable SSH public key , name the user or use the defaukt , then enable generate new key pair

![Image](https://github.com/user-attachments/assets/ed099668-b1f2-4b05-b41e-d6be21682e95)

## 8.Then proceed to the networking tab , select the VNET we created and select the subnet as default
- Ensure to select public address as none  , as we dont want this VM accessible to all

![Image](https://github.com/user-attachments/assets/d64cac15-4086-4f33-8385-731453dfa88b)

## 9.Select the inbound port as 22, this will allow Bastion access the VM.
- Also select load balancing as None , we intend to access the VM through the fireway by giving access to a particular Ip address

![Image](https://github.com/user-attachments/assets/e90ab1e6-fd4d-4caf-bcd4-3832a0418471)

## 10.Then wait for the VM to validate and deploy successfully

![Image](https://github.com/user-attachments/assets/f7507fd0-d5d4-4e33-bca0-c0f2a4969017)

## 11.After it has successfully deployed, Go to Bastion and for authentication type, select SSH private key from local file, below it you will be directed to your folder to pick where the SSH key is located. Then click on connect

![Image](https://github.com/user-attachments/assets/53fc6c22-63ee-4ec3-8390-6d8c2b129e1d)

## 12.Bastion will automatically connect to the VM using the username and the SSH key you provide

![Image](https://github.com/user-attachments/assets/263f76f9-f185-4773-a21e-ae71597cb84a)

# Install and Configure Nginx on Ubuntu

## Step 1: Update Package Lists

Before installing any new software, it's a good practice to update the package lists to ensure you get the latest version.

```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install Nginx

Install Nginx using the following command:

```
sudo apt install nginx
```

## Step 3: Start Nginx Service

```
sudo systemctl start nginx
```

## Step 4: Create HTML File

```
sudo vim /var/www/html/index.html
```

Add the HTML content, for example.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo Page</title>
</head>
<body>
    <h1> I Learnt how networking works in Azure today</h1>
</body>
</html>
```

Save the file.

### Restart Nginx

```
sudo systemctl restart nginx
```

## 13.Then proceed to firewall policy, click on DNAT rule, this stands for Network Address Translation rule
- Click on add a rule collection, the type should be DNAT, the priority should be 100 , then click on add rule
  
![Image](https://github.com/user-attachments/assets/888ebed3-0b89-4c85-aa25-630d15ac4bdd)

## 14.After adding the rule collection, click on add rule
- Select the rule collection group , then select the rule collection we created
- Give the rule a name
- The source type should be ip address
- The source ip address should be ypur ip address. You can get this by searching for my ip on your browser
- The destination Ip address should be the firewall ip address since we intend accessing the App on the VM through firewall
- The protocol should be TCP
  
![Image](https://github.com/user-attachments/assets/d1366e0e-d791-4a89-a59f-33b9b1c3f7c9)

## 15.The destination port should be the port we want to access the app on . Here let's say 4000
- The translated type should be Ip address
- The translated address should be the private ip address of the VM
- The translated port should be the port that the app is accessible which in this scenario it's port 80
  
![Image](https://github.com/user-attachments/assets/c3188d35-55a2-4f06-86f1-d43d335ebde1)

## 16.After all that has been configured , copy the firewall ip address and open it to port 4000 which is our destination port defined above i.e firewallipadress:4000
- You should then be able to access the App
- If its not going through, go and configure the inbound port rule to allow your ip address on port 80

![Image](https://github.com/user-attachments/assets/30d51256-f89c-40cf-b7c0-787ea0aafef2)
