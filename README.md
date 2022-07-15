# Deploy a website on an Nginx server that runs on the EC2 instance and apply SSL.

#### Description:

- Create an EC2 server.
- Install Nginx in it.
- Create a sample index.html page and deploy it on that Nginx server.
- Create an elastic IP and attach it to the ec2 instance.
- Configure domain and apply SSL.
- Configure automation script for SSL renewal.
- Host a sample HTML website with multiple pages like about.html, contact.html, etc.
- Migrate Freenom DNS to Route53.

#### Step-1: Create an EC2 server

Firstly, log in to the AWS management console.

![Img-1](https://user-images.githubusercontent.com/74168188/178555843-f062573f-166c-4b06-b947-d2d11da46507.png)

After login, navigate to the search bar, type EC2, and select EC2

![Img-2](https://user-images.githubusercontent.com/74168188/178555883-5e169bfd-d205-4b99-9992-8dca7e957ff2.png)

Now, the EC2 dashboard will appear. Click Instances

![Img-3](https://user-images.githubusercontent.com/74168188/178555921-6213742a-726c-4532-923e-3edc4c4d1413.png)

Click the Launch instances button.

![Img-4](https://user-images.githubusercontent.com/74168188/178555939-529e74f0-6ece-43dc-aa1c-98d6b7f2deda.png)

To launch an EC2 instance, a few details are required, i.e., instance name, OS image (AMI), instance type, etc.

![Img-5](https://user-images.githubusercontent.com/74168188/178555964-f159e8e9-9b0e-40df-9d5b-7baa60613640.png)
![Img-6](https://user-images.githubusercontent.com/74168188/178556050-f90b180a-0dca-48fb-b30b-8365f9ac8f28.png)
![Img-7](https://user-images.githubusercontent.com/74168188/178556073-b0a18233-2e38-4dbd-926d-f7e411f7fa06.png)

Select a key pair to attach with the instance to log in with that key. If you do not have key pair, then create a new key pair by clicking Create a new key pair. Moreover, according to usage, download key pair in .pem or .ppk format.

![Img-8](https://user-images.githubusercontent.com/74168188/178556119-067cdf5b-023e-46ad-91f5-e9d536e048c4.png)

![Img-9](https://user-images.githubusercontent.com/74168188/178556147-35533b8a-5551-4386-84ea-e36e90c8e0b3.png)

Now, to allow traffic from the internet, we need to create a rule in network settings.

![Img-10](https://user-images.githubusercontent.com/74168188/178556169-37041f2e-e272-4d66-90f3-736fb5a0f726.png)

We are good to go to launch an instance for this. Click the Launch instance button. If everything is correctly set up, you will find a success message on the screen. Click on the instance id to navigate to the EC2 dashboard.

![Img-11](https://user-images.githubusercontent.com/74168188/178556301-ac2e5bdd-7efa-4ad4-99d9-b669e599eefd.png)

Now, take the public IP from the EC2 dashboard and use it to login inside the instance using ssh.

![Img-12](https://user-images.githubusercontent.com/74168188/178556348-e8cd639f-b6a0-422e-9a82-10575ee35ceb.png)

Finally, it will be logged in successfully if everything is configured correctly.

#### Step-2: Install Nginx in EC2 server

First, update the list of packages using ```sudo apt update```

![Img-13](https://user-images.githubusercontent.com/74168188/178556381-7181b99e-cf22-4749-9e5c-c66e4e1e2198.png)

Now, install Nginx using ```sudo apt install nginx```

![Img-14](https://user-images.githubusercontent.com/74168188/178556410-a0cb6304-f811-4b31-8350-29145a0476b5.png)

To check whether Nginx is successfully installed or not, use ```sudo nginx -v```

![Img-15](https://user-images.githubusercontent.com/74168188/178556440-a711a7c2-634d-448a-9712-6b3d4bf4697e.png)

#### Step-3: Create a sample index.html page and deploy it on that Nginx server

For this, navigate to document root, i.e.,/var/www/html, and create an index.html page using vim or nano.

![Img-16](https://user-images.githubusercontent.com/74168188/178556747-3f668348-a3b8-4849-97b0-8764a1fdc4fd.png)

Now, press i to insert text

![Img-17](https://user-images.githubusercontent.com/74168188/178556771-2495ac8f-78c4-4843-a9a4-71cc4f85b116.png)

Furthermore, press Esc to escape from insert mode, then type :wq! to write and quit forcefully.

Now, Let's hit the instance public IP from the chrome browser.

![Img-18](https://user-images.githubusercontent.com/74168188/178556797-d0cd37bd-9092-415f-a8df-8394fd3bdbb4.png)

As you can see, the content is displayed when the client hits IP.

#### Step-4: Create an elastic IP and attach it to an EC2 instance

For this, visit the AWS management console, navigate to the search box, type elastic IP, and then click Elastic IPs. It will redirect to a new page. Click on Allocate Elastic IP address to create an elastic IP.

![Img-19](https://user-images.githubusercontent.com/74168188/178556817-a34dcba0-8497-4ad4-a88b-36139c7116f8.png)

![Img-20](https://user-images.githubusercontent.com/74168188/178556839-91868ea4-e9c4-4beb-8c4f-1f590c444b76.png)

Click on Allocate to create an elastic IP.

Now, we have to attach this elastic IP to an EC2 instance. Select the unallocated elastic IP, click on Actions, then Associate Elastic IP address. Now, select the instance to attach with elastic IP, then select the private IP of the instance.

![Img-21](https://user-images.githubusercontent.com/74168188/178556870-09ea2eac-f67e-4fad-84d5-4843fdf966a4.png)

![Img-22](https://user-images.githubusercontent.com/74168188/178556894-94ca38f1-dfa3-4ffe-866b-b07465d8019d.png)

Now, hit the elastic IP to see the sample index.html page.

![Img-23](https://user-images.githubusercontent.com/74168188/178556932-47dec8e0-5474-4aed-80cc-25454fe112fc.png)

#### Step-5: Configure domain and apply SSL

Purchase a free domain from freenom.com. For this, search any domain and click select, then checkout and complete the order.

![Img-24](https://user-images.githubusercontent.com/74168188/178556964-db9c96e3-443e-4be7-88d1-0b450c5feb7b.png)
![Img-25](https://user-images.githubusercontent.com/74168188/178556984-c7d8378f-e7b4-452b-a4f1-3a24d90cd58b.png)
![Img-26](https://user-images.githubusercontent.com/74168188/178557005-4c881e54-da28-4ab4-8c7b-5b28939de62e.png)

Now, select My Domains inside Services.

![image](https://user-images.githubusercontent.com/74168188/178632468-d7ba16f6-37db-441a-8376-3aef7e3f6296.png)

Click the manage button of the domain that you want to configure.

![Img-29](https://user-images.githubusercontent.com/74168188/178655181-8b5d6421-d8b6-4f6c-a862-3ff0e7b3df05.png)

Now, click Manage Freenom DNS and add records, then click save changes.

![Img-30](https://user-images.githubusercontent.com/74168188/178658491-46e2084f-b0d6-47f6-a1ae-f420d8ee886b.png)

Now, let's create a server block file. For this, copy the default file and then edit accordingly.

![Img-31](https://user-images.githubusercontent.com/74168188/178662027-69d9ae76-7ee1-49ee-99f7-040ead894fad.png)

![Img-32](https://user-images.githubusercontent.com/74168188/178662337-9190ddee-4788-4605-8cf1-12119762d067.png)

Updated document root path, server_name, and remove default_server keyword in server block file and save by pressing Esc key then write :wq!

![Img-33](https://user-images.githubusercontent.com/74168188/178664005-4a23443e-6047-4652-8435-465fe2d2df3b.png)

Next, let's enable the file by creating a link from sites-available to the sites-enabled directory, which Nginx reads from during startup:

![Img-34](https://user-images.githubusercontent.com/74168188/178664866-57083e5c-4fb8-488c-873c-812c6c6ca726.png)

To check that there are no syntax errors in any of your Nginx files, use ```sudo nginx -t```

![Img-35](https://user-images.githubusercontent.com/74168188/178665348-8b1f8d2b-a434-484c-9d7e-5aeaecc53f55.png)

Time to restart Nginx server using "`sudo systemctl restart nginx` "

![Img-36](https://user-images.githubusercontent.com/74168188/178665788-5536d95a-afcf-46a3-a2e5-7eadd6927981.png)

Now, let's try to hit EC2 IP as well as domain mannan18.ml and www.mannan18.ml

![Img-37](https://user-images.githubusercontent.com/74168188/178666251-cbbce521-6d06-4f92-8785-4fa299f548ba.png)

![Img-38](https://user-images.githubusercontent.com/74168188/178666378-5e0019d1-1a1c-4396-92a4-8522c1b7c976.png)

![Img-39](https://user-images.githubusercontent.com/74168188/178666485-6cefbe2b-ac37-4520-89c4-44b97e3cc684.png)

As you can see, we have successfully hosted. We are now moving to the SSL part. To obtain an SSL certificate, we must install certbot software and the Nginx plugin.

```
sudo apt install certbot python3-certbot-nginx -y
```
![Img-40](https://user-images.githubusercontent.com/74168188/178668761-72b5f4fe-0041-4bd7-8042-2ea92eb1c9c4.png)

To obtain a certificate for a domain.

```
sudo certbot --nginx -d mannan18.ml -d www.mannan18.ml
```
It will prompt you to enter your email address and agree to the terms of service. 

![Img-41](https://user-images.githubusercontent.com/74168188/178669321-56dc0c19-796f-49f8-a3de-28f6ce15f7c0.png)
![Img-42](https://user-images.githubusercontent.com/74168188/178670579-be14977f-85d4-44dc-8c9a-007b30a71406.png)

As you see, certificate is saved at /etc/letsencrypt/live/mannan18.ml/fullchain.pem and key is saved at /etc/letsencrypt/live/mannan18.ml/privkey.pem

Also, Certbot has set up a scheduled task to renew the certificate in the background automatically.

#### Step-6: Configure automation script for SSL renewal

Certbot automatically creates the script to renew the certificate twice a day. This script is located at /etc/cron.d/certbot

![Img-43](https://user-images.githubusercontent.com/74168188/178673034-451825ba-7238-4266-85da-2ee782a6552c.png)

#### Step-8: Host a sample HTML website that has multiple pages like about.html, contact.html, etc

For this, I downloaded a sample website from **https://www.free-css.com/free-css-templates/page280/webwing**

To transfer downloaded pages to the EC2 instance, we used SCP.

![Img-44](https://user-images.githubusercontent.com/74168188/178695041-ddce4985-51d2-4868-8aa8-b54ff6388399.png)

Then copy all files and folders from /home/ubuntu/ to /var/www/html

![Img-45](https://user-images.githubusercontent.com/74168188/178695749-901b935d-3fe9-4225-9eb8-5649c410ea64.png)

Now, let's hit mannan18.ml and see the result.

![Img-46](https://user-images.githubusercontent.com/74168188/178696406-f57fad48-4532-4ecc-ab4e-29f3b45eb111.png)

#### Step-9: Migrate Freenom DNS to Route53

Firstly, we must create a hosted zone using the Route53 service of AWS.

![Img-47](https://user-images.githubusercontent.com/74168188/178700658-ba293416-af6e-4deb-aae0-9a328b9acd1c.png)

Fill in the domain name you want to route traffic, then click create a hosted zone.

![Img-48](https://user-images.githubusercontent.com/74168188/178701549-a95ca56b-1f4b-40d0-8a3a-775267ee18da.png)

![Img-49](https://user-images.githubusercontent.com/74168188/178701591-13e43594-3576-480f-98f8-93d6647fc3cb.png)

A hosted zone is now created. Create a record to route traffic to the IP address

![Img-50](https://user-images.githubusercontent.com/74168188/178714826-fa7dee3d-7def-414b-b8bf-971e5d957207.png)

![Img-51](https://user-images.githubusercontent.com/74168188/178715359-23008800-551d-4c18-8c7d-829d3f52d257.png)

![Img-52](https://user-images.githubusercontent.com/74168188/178716697-60d42097-7528-462c-b536-468e3a0fe222.png)

Now, copy the route53 nameservers from records and put in nameservers records of freenom, and click change nameservers.

![Img-53](https://user-images.githubusercontent.com/74168188/178716887-35330c14-be1e-4af9-9295-b5740e9eb422.png)

![Img-54](https://user-images.githubusercontent.com/74168188/178717035-d955e9f1-5c2e-4ca6-9549-535be46b7778.png)

Also, we have to create a new record.

![Img-55](https://user-images.githubusercontent.com/74168188/178740756-cba9fe89-e51e-4910-a8fb-709d8201e55e.png)

![Img-56](https://user-images.githubusercontent.com/74168188/178740922-09ef362b-a0d4-4442-9d14-99c28d44d9ac.png)

Now, all records will look as shown below.

![Img-57](https://user-images.githubusercontent.com/74168188/178743523-ba88a969-ce14-4d3a-a2df-9759fa605e0c.png)

After hitting, mannan18.ml & www.mannan18.ml we are getting the website.

![Img-58](https://user-images.githubusercontent.com/74168188/178744190-63aae10e-4dc3-42d7-a299-277c4f648e39.png)

So, we have successfully done the hosting, SSL, and migration to Route53 part.
