#  Automating displaying EKS cluster information

In this project, I've put together a neat way to automatically fetch and d
isplay information about an Amazon EKS (Elastic Kubernetes Service) cluster. 
I used Python, along with the Boto3 library, to interact with AWS EKS and pulls out the details 
about the cluster status, kubernetes version and cluster endpoint. 

I also used Terraform to create the EKS Cluster itself.

## What I Did

1.  **EKS Cluster Setup:** I created the EKS cluster using Terraform.

    ![eks](https://github.com/Princeton45/python-eks-monitor/blob/main/images/eks.png)

2.  **Wrote the Python Script:** I developed a Python script that uses Boto3 to connect to AWS. The script grabs all the  details about the EKS cluster, 
like its cluster status, kubernetes version and cluster endpoint.
    *   **Suggested Picture:** A screenshot of the script's output showing the cluster information.

4.  **Displayed the Information:** Finally, the script presents this information in a clear and readable format.
    *   **Suggested Picture:** A screenshot of the neatly formatted output in the terminal.