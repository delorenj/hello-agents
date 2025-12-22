# N8N Installation Guide

Here we introduce the Docker-based local installation method used in the project, as it is the most stable and most beneficial for continued exploration of n8n usage.

First, visit the Docker official website: [Docker: Accelerated Container Application Development](https://www.docker.com/)

Select your device type for download. Here we use Windows as a demonstration.

![image-20250912025341155](./N8N_INSTALL_GUIDE/image-20250912025341272.png)

After downloading, you can switch the disk storage path, as images are generally very large, try not to store them on the C drive.

![image-20250912032540657](./N8N_INSTALL_GUIDE/image-20250912032540657.png)

Then open your command line and enter the following commands to pull n8n:

```
docker volume create n8n_data
docker run -d --restart unless-stopped --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

Now we can see n8n running in Docker!

![image-20250912033251997](./N8N_INSTALL_GUIDE/image-20250912033251997.png)

Click on 5678:5678 to enter n8n's startup interface.

![image-20250912033341666](./N8N_INSTALL_GUIDE/image-20250912033341666.png)

After entering the page, you can see the button to open a new project

![image-20250912034040656](./N8N_INSTALL_GUIDE/image-20250912034040656.png)

There are three main functions to be used:

![image-20250912234709064](./N8N_INSTALL_GUIDE/image-20250912234709064.png)

After opening the add new node button, you can search for nodes or select the nodes you need to add~

![image-20250912234748845](./N8N_INSTALL_GUIDE/image-20250912234748845.png)
