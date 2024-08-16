# Cloudflare Tunnel Docker Compose Configuration  

A sample Docker Compose file and brief advice for Cloudflare Zero Trust Tunnels.  

## Important Details  
 
* The Docker Compose file assumes you have already created a Docker network called ```CloudflareTunnel``` that is already connected to any containers/services you wish to tunnel.  
  * You can create a network before starting the container by executing the following command: ```docker network create CloudflareTunnel```  
* You must create a file called ```.env``` in the same directory as the ```docker-compose.yml``` that contains a key value pair ```TUNNEL_TOKEN=<YOUR_CLOUDFLARE_TUNNEL_TOKEN>  ```  

## Starting the container  

In your terminal, ```cd``` to the directory containing the ```docker-compose.yml``` and ```.env``` files. Run the following command: ```docker compose up -d```  
Your container should be up and running and your Cloudflare Dashboard configured tunnels should be live!  

## Post Container Startup  

* You can attach other containers to this network by executing the following command: ```docker network connect CloudflareTunnel <CONTAINER_NAME>```  
  * After you start the container, this allows you to configure a tunnel with a service URL that is the name of the container you want to tunnel:  
      ![Cloudflare Dashboard Tunnel configuration](images/TunnelConfiguration.png)
  * If using a reverse proxy, simply use the name of your reverse proxy container and add the HTTP Host Header like in the following example:  
      ![Cloudflare Dashboard Tunnel configuration for reverse proxy](images/TunnelConfigurationReverseProxy.png)
* No ports need are exposed to the host in ```docker-compose.yml``` because Cloudflare Tunnel connects to your services via Docker Networks.  

### Disclaimer  

This repository is provided as-is and is intended for informational and reference purposes only. The author assumes no responsibility for any errors or omissions in the content or for any consequences that may arise from the use of the information provided. Always exercise caution and seek professional advice if necessary.  
