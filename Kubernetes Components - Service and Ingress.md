# Kubernetes Networking and Communication

Kubernetes provides robust networking and communication capabilities to ensure that applications can interact seamlessly, even in dynamic and changing environments. This document outlines key concepts such as virtual networks, ephemeral pods, and services. 
Let's see how these pods are communicating each other.  

# Virtual Network and Pod IP Addresses

<i><b>Virtual Network</b></i>  

  - Kubernetes offers a virtual network that assigns each pod its own unique internal IP address.
  - This allows for seamless internal communication between pods.

<i><b>Internal Communication</b></i>  

  - Pods communicate with each other using these internal IP addresses.
  - Example: An application container in one pod can communicate with a database container in another pod using the database pod's internal IP address.

# Ephemeral Nature of Pods  

<i><b>Ephemeral Pods</b></i>  

  - Pods in Kubernetes are ephemeral, meaning they can be created and destroyed frequently.
  - Causes of pod recreation include container crashes, node failures, or resource constraints.

<i><b>New IP Addresses</b></i>  

  - When a pod is recreated, it is assigned a new internal IP address.
  - Problem: Using the pod's IP address for communication can lead to issues as the IP changes each time the pod is restarted.

# Inconvenience of Changing IPs

<b><i>IP Address Changes</i></b>  

  - If your application communicates with the database using the pod's IP address, you would need to update the application with the new IP address each time the database pod is recreated.  
  - This is not practical and can lead to downtime or configuration issues.

# Solution: Kubernetes Service  

<b><i>Service Abstraction</i></b>  

  - Kubernetes introduces a component called a <b>Service</b> to address the problem of changing IP addresses.
  - A Service provides a stable IP address and DNS name that remain constant even if the pods behind the service are recreated with new IP addresses.
  - Static IP Address: The Service acts as a static or permanent IP address that can be attached to each pod.  Your application will have its own Service, and the database will have its own Service.

<b><i>Decoupled Lifecycle</b></i>  

  - The lifecycle of pods and services are not connected.
  - Persistent Services: Even if a pod dies and is recreated, the Service and its IP address remain unchanged.
  - No Endpoint Changes: You don't have to change the endpoint in your application because the Service IP address stays the same.  

<b><i>Load Balancing</i></b>  

  - The Service acts as a load balancer, distributing traffic among the pods it routes to.

<img width="364" alt="image" src="https://github.com/user-attachments/assets/3dd17516-7287-4a35-8692-650c16b53f1b">  

# Accessing Your Deployed Application Through a Web Server

What if you want to access your deployed application through a web server? How can you achieve that?  

To accomplish this, you need to create an External Service.  

<img width="467" alt="image" src="https://github.com/user-attachments/assets/33b40188-cf37-4c04-b3c0-0e11fd497937">  

External service is a service that opens the communication from external resources. But still we can't open the DB to public request and for that we will create something called Internal Service.

<b><i>Ingress for Real-World Applications</i></b>  

Even though the my-app service URL is suitable for testing the application, it won't be a good approach for real-world applications. If you want to access your application with a secure protocol and a domain name, Kubernetes offers another component named <b>Ingress</b>.  

<img width="467" alt="image" src="https://github.com/user-attachments/assets/7730ede5-5b6b-4891-8880-b647b4a45d66">  

Instead of the request going directly to the Service, the request first goes to Ingress, which then forwards it to the appropriate Service.  

<img width="469" alt="image" src="https://github.com/user-attachments/assets/e98f7364-b2ab-4901-84d9-659d2113b2a9">  







