# Interview-Task
## Routing without a public IP 

## Establish how one can route traffic to local HTTP (or more generally TCP) interfaces in the absence of a public IP.

Currently it was known that the ipv4 are not enough to identify all computers publicly in the internet. The Routers were made to be an agent giving out local ip addresses mostly (eg: 192.168) prefixes to identify each device under each router making all of the devices identifyable. By this the only way to route traffic in a local area network LAN is to have a software that will identify each computer uniquely by it Local area network IP address  and route the requests to  them accordingly.

## What out-of-the-box, free applications can be used to achieve this proxying?
-Nginx
-Apache
-Ngrok and Pagekite to enable cloud access localhost via an url link.

## Provide a solution using one of these applications (if you found one).
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
```
cd /etc/nginx/sites-enabled
sudo "${EDITOR:-vi}" default
 ```
 ```
location /site X {
        proxy_pass http://site X;
        proxy_buffering off;
        proxy_set_header X-Real -IP $remote_addr;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Port $server_port;}
 ```

 
## What does it take to implement a proxying application of this kind?
-It requires one server like eg nginx that will reroute traffic to another appropetiate server providing a level of abstraction. Has to have two or more servers.

## Implement a solution.
location /sitex {
            	proxy_pass http://192.168.43.211/;
        	proxy_buffering off;
        	proxy_set_header X-Real-IP $remote_addr;
        	proxy_set_header X-Forwarded-Host $host;
        	proxy_set_header X-Forwarded-Port $server_port;} 
 
 
                ![IMG-20230110-WA0010](https://user-images.githubusercontent.com/87112355/211549899-403ce142-c278-4f66-84b9-4d8efade3189.jpg)
                ![IMG-20230110-WA0009](https://user-images.githubusercontent.com/87112355/211549939-69fec7aa-2a37-40d0-ac2c-aef5d6a39619.jpg)
                ![IMG-20230110-WA0008](https://user-images.githubusercontent.com/87112355/211549978-c986f4a0-de5f-4787-a841-0b3bd06a30c2.jpg)
                ![IMG-20230110-WA0011](https://user-images.githubusercontent.com/87112355/211550049-b8578913-a1bc-4249-a729-9e20b143b1cc.jpg)



## Document results
- ngrok link, made cloud user access a computer in  the local area network and in turn that computer rerouted its requests to site X in the Local area network.

## Security concerns
 -access to nginx port 80 server via website is http protpcol and not https protocol which is encrypted and secure.
-access through http is a security threat as data isn't encrypted

