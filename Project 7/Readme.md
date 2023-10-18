# IMPLEMENTATION OF LOAD BALANCING WITH NGNIX

## Introduction to load Balancing and Nginx

**What is a load balancer?**

A load balancer distributes workloads across multiple compute resources, such as virtual servers. Using a load balancer increases the availability and fault tolerance of your applications.

You can add and remove compute resources from your load balancer as your needs change, without disrupting the overall flow of requests to your applications.

The load balancer stands in front of the webserver and all traffic gets into it first, it then distribute the traffic evenly across the set of webservers. This ensures no webserver gets overworked,consequently improving performance.

Nginx is a versatile software it acts like a webserver,reverse proxy, and a load balancer etc.All that is needed is to configure it properly to server to your use case.


## Prerequisite 
- EC2 Instance running on ubuntu 22.4

## STEP 1

- Open Aws management Console and click on EC2 instances to launch

    ![Alt text](<Images/Launching Ec2 Instances.png>)


- Under name provide a unique name for each of your Webserver. In this case `Load-balancer Apache` and `Load-balancer Apache`


    ![Alt text](<Images/Load balance Nginx.png>)


    ![Alt text](<Images/Load Balance Apache.png>)

- Under Application and Os images,click on quick start and Ubuntu 22.4

    ![Alt text](<Images/Quick start.png>)


- Under key pair, click on create new key and use it for all the instances you provision. In this case we will create a key pair called `Universal-key`

    ![Alt text](Images/Universal-key.png)

- Finally, click on Launch Instances

    ![Alt text](<Images/Finally Launch Instances.png>)


## STEP 2

Open Port 8000, we will be running our webservers on port 8000 while the load balancers run port 80. we will need to open port 8000 to allow traffic from anywhere. To do this we need to add a rule to the security group of each of our webserver.

- Click On the instance ID to get of your EC2 instances.

  - Load-balancer Apache

  ![Alt text](<Images/security page.png>)

  - Load-balancer Apache-2

  ![Alt text](Images/esc.png)

  - ON the same page scroll and click on `Security`

    - Load-balancer Apache-2

        ![Alt text](<Images/page sex 1.png>)

    - Load-balancer Apache 

        ![Alt text](Images/try.png)

- Click on edit inbound rule.

    - Load-Balancer apache

         ![Alt text](<Images/Edit bound apache.png>)

    - Load-balancer Apache-2

        ![Alt text](<Images/Edit Inbound Nginx.png>)

- Add your rules; 

    - Load-Balancer Apache 

        ![Alt text](<Images/APache save rules.png>)

    - Load-Balancer Apache-2

         ![Alt text](<Images/Nginx Save rules.png>)

## STEP 3

After provisioning both servers and openeing the necessary port,Install apache servers on both servers.

To do this we must first connect to the servers via ssh , so that we can run the installation command on the Terminals 

- To connect the instance, click the instance Id and Click connect.

    - Load-balancer APache 

        ![Alt text](<Images/CnT 1.png>)

    - Load balancer Apache 2

        ![Alt text](Images/xnt.png)

- Copy the `shh client` and cd into download in  your Terminal
- paste the shh Client and hit enter

    - Load-balancer Apache 
    ![Alt text](<Images/Connected to Apache 1.png>)

    - Load balancer Apache 2

    ![Alt text](Images/CONNECYED.png)

- To install Apache server Run `sudo apt update -y &&  sudo apt install apache2 -y`

    - Load-balancer Apache 

    ![Alt text](<Images/Sudo install Apache -y.png>)

    - Load-balancer Apache 2

    ![Alt text](<Images/Sudo install appache2.png>)


- To verify if Apache is running on the system
    - Run `sudo systemctl status apache2`

        - Load-balancer Apache 

        ![Alt text](Verify.png)

        - Load-balancer Apache2

        ![Alt text](<Images/Verify 2.png>)

## STEP 4
Configuring Apache webservers to serve content on port 8000 instead of the default port which is port 80.
Then we will create new `index.html` file. The file contain code to display the public Ip address of the Ec2 instances . We will then override apache webserver default html file with the new file

- To configure Apache to serve content on port 8000.
.
    - Run `sudo vi /etc/apache2/ports.conf ` and use text editor to open /etc/apache2/ports.config

        - Load-balancer Apache 
        ![Alt text](Images/Port.conf.png)

        - Load-balancer Apache2 

        ![Alt text](Images/Port.conf2.png)


- To open the file `/etc/apache2/sites-available/000-default.conf` and change port;80 on the virtual host to port;8000.

    - Run `sudo vi /etc/apache2/sites-available/000-default.conf`

        - Load-balancer Apache 

            ![Alt text](Vi-Host.png)

        - Load-balancer Apache2 

           ![Alt text](<Images/Vi- Host 2.png>)


- To Reload or Restart Apache to the new configuration using the command Below 

    - Run `sudo systemctl restart apache2`

        - Load-balancer Apache

            ![Alt text](<Images/restart apache 2.png>)

        - Load-balancer Apache2

        ![Alt text](<Images/Restart apache 1.png>)


### Creatiing a new index.html file 

- To open a new index.html file 

 - Run `sudo vi index.html`

-  paste the code below and get the public Ip address to replace the placeholder text for Ip address in the html file.
```        <!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>Welcome to my EC2 instance</h1>
            <p>Public IP:54.90.172.75</p>
        </body>
        </html>


```
- Load-balancer apache 

  ![Alt text](<Images/new HTML.png>)

- Load-balancer apache2

![Alt text](<Images/New HTml (2).png>)


- To change the file ownership of index.html

    - Run `sudo chown www-data:www-data ./index.html`

        - Load-balancer apache

         ![Alt text](Images/chmod.png)  

        - Load-balancer apache2 

        ![Alt text](Images/chown2.png)

**Overriding the default HTML file of the apache webserver**

- To replace the the default html file with our new html 

    - Run `sudo cp -f ./index.html /var/www/html/index.html`

        - Load-balancer apache
        ![Alt text](<Images/last part.png>)

        - Load-balancer apache2

        ![Alt text](<Images/Apache 2.png>)


- To restart webserver and laod new configuration 

    - Run `sudo systemctl restart apache2`

- RESULT on web browser

    - Load-balancer apache
        ![Alt text](<EC2 page.png>)

    - Load-balancer apache2

        ![Alt text](Images/chrome_nhTdVmKZ7I.png)

## STEP 5
**CONFIGURING NGINX AS LOAD BALANCER**
Prerequisite: 
- EC2 Instance running Ubuntu 22.4
- Port 80 open to allow trafic from anywhere
- SSH into the instance via the Terminal 

**INSTALLING NGINX**
- To Install Nginx Run `sudo apt update -y && sudo apt install nginx -y`

    ![Alt text](Images/&&.png)

- TO Verify that Nginx is installed successfully 

    - Run `sudo systemctl status nginx`

       ![Alt text](Images/mintty_q9OWiChEAI.png)

- Open a configuration file where you are going to paste the code for nginx to act as a `load-balancer`

    - Run `sudo vi /etc/nginx/conf.d/loadbalancer.conf`

    - Paste 
       ```        
        upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server 127.0.0.1:8000; # public IP and port for webserser 1
            server 127.0.0.1:8000; # public IP and port for webserver 2

        }

        server {
            listen 80;
            server_name <your load balancer's public IP addres>; # provide your load balancers public IP address

            location / {
                proxy_pass http://backend_servers;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }
        }
    

       ```

![Alt text](Images/mintty_IY0lWgJEYw.png)


- **Upstream backend_servers :** Define a group of backend servers
- The *server* lines inside the *upstream* block list the addresses and the ports of your backend-servers.
- **Proxy_pass** inside the **location block** sets up the load balancing, passing the request to the backend servers.
- **The proxy_set_header** lines pass necessary header to the backend servers to correctly handled the request.

**TESTING CONFIGURATION**

- To test Configuration, Run `sudo nginx -t`

    ![Alt text](Images/T0l8m07.png)

- To restart Nginx to load the configuration

    - Run `sudo systemctl restart nginx`

        ![Alt text](Images/oQ0eF2Z.png)

- In the web browser  paste the `Ip-address` of the Nginx load paste and hit enter
- RESULT
 
    - Load-balancer apcahe 
        ![Alt text](Images/chrome_N0pY3D4bsi.png)

    - Load-balancer apache2
    
    ![Alt text](Images/chrome_08nSLhHFn8.png)


# END OF PROJECT 7








  
   

  














