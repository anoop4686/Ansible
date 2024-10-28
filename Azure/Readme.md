Azure CLI setup on Ansible master node
==============================

Requirnment
----------------------

1. Update the Linux package and install certificate

```
sudo apt-get update
```
```
sudo apt-get install ca-certificates curl apt-transport-https lsb-release gnupg -y

```

2.  Add Microsoft key in your repo
```
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.gpg REDIRECT /dev/null
```

3.  Update Microsoft package 
```
AZ_REPO=$(lsb_release -cs)
echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
```

4.  Install Azure cli
```
sudo apt-get update
sudo apt-get install azure-cli -y 
```

5. Install Ansible
```
sudo apt install ansible -y 
```

6. Install requird python plugin (Python plugin is used to intract with Ansible control node and Azure)

```
sudo apt install python3-pip
pip3 install ansible[azure] --user
```

7. Login Azure : Authenticate the Azure ID
```
az Login
```
or
```
az login --use-device-code
```

8. get the credental and copy all the credental with txt
```
az ad sp create-for-rbac --name ansible
```
```
az role assignment create --assignee < appID: past the AppId from above step > --role Contributor
````
If you getting error of scope. Use below 
```
az role assignment create --assignee b10402a4-c992-415a-9e54-5304ac4cbf11 --role Contributor --scope /subscriptions/subscriptions-ID
```

9. Get the subscriptions ID and Tennet IP. Copy the info to txt file

```
az account show --query '{tenantId:tenantId,subscriptionid:id}';
```

10. Get the Clinet. Copy the info to txt file
```
az ad sp list --display-name ansible --query '{clientId:[0].appId}'
```

11. Create file and enter the credental.

```
vi ~/.azure/credentials
```
File conetent : 
```
[default]
subscription_id=<subscription_id>
client_id=<service_principal_app_id>
secret=password
tenant=<service_principal_tenant_id>
```
Test Ansible is working  iwth Azure 
---------------------------
```
ansible localhost -m azure_rm_resourcegroup -a "name=test1234 location=uksouth"
```

Author 
----------------------
Anoop Maurya

Version
--------------------
Version 5
