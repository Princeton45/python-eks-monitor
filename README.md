#  Automating displaying EKS cluster information

In this project, I've put together a neat way to automatically fetch and d
isplay information about an Amazon EKS (Elastic Kubernetes Service) cluster. 
I used Python, along with the Boto3 library, to interact with AWS EKS and pulls out the details 
about the cluster status, kubernetes version and cluster endpoint. 

I also used Terraform to create the EKS Cluster itself.

Documentation: https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/eks.html
## What I Did

1.  **EKS Cluster Setup:** I created the EKS cluster using Terraform.

    ![eks](https://github.com/Princeton45/python-eks-monitor/blob/main/images/eks.png)

2.  **Wrote the Python Script:** I developed a Python script that uses Boto3 to connect to AWS. The script grabs all the  details about the EKS cluster, 
like its cluster status, kubernetes version and cluster endpoint.

```python
# Import the boto3 library, which is the AWS SDK for Python
import boto3

# Create an EKS (Elastic Kubernetes Service) client using boto3
client = boto3.client('eks', region_name="us-east-1")

"""Get a list of all EKS clusters in the region
   The list_clusters() method returns a dictionary, and we extract the 'clusters' key """
   
clusters = client.list_clusters()['clusters']

# Iterate through each cluster in the list
for cluster in clusters:
    
    """ For each cluster, call describe_cluster to get detailed information
        The 'name' parameter specifies which cluster to describe """
        
    response = client.describe_cluster(
        name=cluster
    )
    
    """Extract cluster information from the response
       The cluster details are nested under the 'cluster' key"""
       
    cluster_info = response['cluster']
    
    """Get specific cluster attributes:
        status: current state of the cluster (e.g., ACTIVE, CREATING, etc.)
        endpoint: the API server endpoint URL
        version: the Kubernetes version running on the cluster"""
        
    cluster_status = cluster_info['status']
    cluster_endpoint = cluster_info['endpoint']
    cluster_version = cluster_info['version']

    """Print the information for each cluster using f-strings
       This provides a formatted output of the cluster details """
       
    print(f"Cluster {cluster} status is  {cluster_status}")
    print(f"Cluster endpoint: {cluster_endpoint}")
    print(f"Cluster version: {cluster_version}")
```

![output](https://github.com/Princeton45/python-eks-monitor/blob/main/images/output.png)

Documentation: https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/eks.html