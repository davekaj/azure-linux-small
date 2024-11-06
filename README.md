# azure-linux-small
A small linux vm that can quickly be setup to test remote blockchain connecting

## Installation 

```bash
brew update && brew install azure-cli
which az
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
which terraform
```

# Setup Terraform
```bash
touch main.tf # then fill out the file with resources seen in this repo
terraform init
```

# Login to azure

```bash
az login
# will open browser for you to confirm, must login to azure in the browser
# press enter for default subscription
```

Copy subscription into main.tf:

```tf
provider "azurerm" {
  features {}
  subscription_id = "<your_subscription_id>"
}
```

Update sshkey if not already at the location below

```tf
  admin_ssh_key {
    username   = "azureuser"
    public_key = file("~/.ssh/id_rsa.pub")
  }
```

Then:

```bash 
terraform apply # wait about 2 mins, then enter yes
```

# Troubleshooting

Setting up quota increases for the vm size (use the search bar to find the resources):

To increase the quota for the standardBpsv2Family in the East US region, follow these steps:
1. Sign in to the Azure portal.
2. Navigate to your Azure subscription's Overview page.
3. Select "Usage + quotas" to view your current quotas.
4. Look for the option to request an increase for the specific VM family quota you need (in this case, standardBpsv2Family).
5. Follow the prompts to submit your request, specifying the desired increase.

Then I increased it to 4 cpus, i.e. new limit = 4, and it didn't work. 
Then I sent a support request, and now I am waiting.
