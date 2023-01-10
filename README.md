# Interview-Task
Routing without a public IP 

Establish how one can route traffic to local HTTP (or more generally TCP) interfaces in the absence of a public IP.

Currently it was known that the ipv4 are not enough to identify all computers publicly in the internet. The Routers were made to be an agent giving out local ip addresses mostly (eg: 192.168) prefixes to identify each device under each router making all of the devices identifyable. By this the only way to route traffic in a local area network LAN is to have a software that will identify each computer uniquely by it Local area network IP address  and route the requests to  them accordingly.

What out-of-the-box, free applications can be used to achieve this proxying?
-Nginx
-Apache
-Ngrok and Pagekite to enable cloud access localhost via an url link.

Provide a solution using one of these applications (if you found one).
Any Computer In the LAN with site X access.

Install ngrok ubuntu

snap install ngrok

// activate token
ngrok config add-authtoken <token>

ngrok http 80

Linux ubuntu example of installing nginx
sudo apt update
sudo apt install nginx
 
Configure nginx to reverse proxy all routes to site  X to real site in locahost X

By editing config files.

cd /etc/nginx/sites-enabled
sudo "${EDITOR:-vi}" default
location /site X {
        proxy_pass http://site X;
        proxy_buffering off;
        proxy_set_header X-Real -IP $remote_addr;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Port $server_port;

What does it take to implement a proxying application of this kind?
-It requires one server like eg nginx that will reroute traffic to another appropetiate server providing a level of abstraction. Has to have two or more servers.

Implement a solution.
location /sitex {
            	proxy_pass http://192.168.43.211/;
        	proxy_buffering off;
        	proxy_set_header X-Real-IP $remote_addr;
        	proxy_set_header X-Forwarded-Host $host;
        	proxy_set_header X-Forwarded-Port $server_port;
        }
        
        ![WhatsApp Image 2023-01-10 at 14 57 32](https://user-images.githubusercontent.com/87112355/211546556-ab646177-b0b1-4511-a046-f726a714a129.jpg)
        ![WhatsApp Image 2023-01-10 at 14 57 32](https://user-images.githubusercontent.com/87112355/211546882-5b327827-e603-418c-b9f7-34e1032d2e0b.jpg)
        ![WhatsApp Image 2023-01-10 at 14 57 32](https://user-images.githubusercontent.com/87112355/211546957-f54dc31b-9ef9-48d7-9702-8fe80bbf199e.jpg)
        ![WhatsApp Image 2023-01-10 at 14 57 33](https://user-images.githubusercontent.com/87112355/211547068-cdac6422-0e58-4b11-9321-dddc6a37e5fe.jpg)
        ![IMG-20230110-WA0011](https://user-images.githubusercontent.com/87112355/211548791-c1aa2d2a-35a1-47a9-b75a-d03f41bc5ad9.jpg)



Document results, perhaps address security concerns.
-access to nginx port 80 server via website is http protpcol and not https protocol which is encrypted and secure.
-access through http is a security threat as data isn't encrypted

