# OCI-Terraform
Simple infrastructure on OCI using Terraform
<p align="center">
  <img  src="https://github.com/Ahmed-Shoushaa/OCIxTerraform/blob/main/Images/oci-architecture.png">
</p>

## Prerequisites:

1. **Terraform installed**
    
    ```bash
    # cd to the script directory
    chmod 700 terraform_install.sh
    # For Debian/Ubuntu based images only
    ./terraform_install.sh
    ```
    
    For more details: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
    
2. **RSA Keys for authentication and add it’s public key to your user account**
    
    `Note: If you're using Oracle Cloud Shell, skip creating the RSA keys. You're already authenticated when you log in to the OCI Console.`
    
    ```bash
    # Run key-gen.sh script which generates RSA keys in ~/.oci
    chmod 700 key-gen.sh
    ./key-gen.sh
    ```
    
    Then Add the public key to your user account.
    
    - In the OCI Console's top navigation bar, click the **Profile** menu, and then go to **User settings**.
    - Click **API Keys** -> **Add API Key** -> **Paste Public Keys**
    - Paste value from previous step, including the lines with `BEGIN PUBLIC KEY` and `END PUBLIC KEY` then **Add**
4. **Add List Policy**
    
    If your username is in the Administrators group, then skip this step.
   
   Otherwise, ask your administrator to add the following policy to your tenancy
   
   For details to add policy: https://docs.oracle.com/en-us/iaas/developer-tutorials/tutorials/tf-provider/01-summary.htm
   
    
6. Prepare required data for authentication:
    1. Collect the following credential information from the **OCI Console**.
        - **Tenancy OCID:**
            - In the top navigation bar, click the **Profile** menu, go to **Tenancy:** *<your-tenancy>*  and copy OCID.
        - **User OCID:**
            - From the **Profile** menu, go to **User settings** and copy OCID.
        - **Fingerprint:**
            - From the **Profile** menu, go to **User settings** and click **API Keys**.
            - Copy the fingerprint associated with the **RSA public key** you made in section 2. The format is: `xx:xx:xx...xx`.
        - **Region:**
            - From the top navigation bar, find your region.
            - From the table in [Regions and Availability Domains](https://docs.oracle.com/iaas/Content/General/Concepts/regions.htm), Find your region's `<region-identifier>`. Example: `us-ashburn-1`.
    2. Collect the following information from **your environment**.
        - **Private Key Path:**
            - Path to the **RSA private key** you made in the **Create RSA Keys** section `~/.oci/RSA.pem`.
                

For More details: https://docs.oracle.com/en-us/iaas/developer-tutorials/tutorials/tf-provider/01-summary.htm

## Run Terraform Scripts:

We can run the terraform scripts with multiple methods choose one of them:
1. Run automation.sh which takes the required authentication data as Environmental variables and authenticate to oracle api with it then create or delete the infrastructure
    ```bash
    # cd to the script directory
    chmod 700 automation.sh
    ./automation.sh
    ```
<p align="center">
  <img width="600" height="450" src="https://github.com/Ahmed-Shoushaa/OCIxTerraform/assets/117172376/d75c34a0-11d7-42b4-8cd8-d65aa440e011">
</p>

2. Uncomment the <provider "oci"> section in provider.tf and add the required data values
<p align="center">
  <img  src="https://github.com/Ahmed-Shoushaa/OCIxTerraform/assets/117172376/a344c5ea-7d02-4a23-b28a-a5935b8a230d">
</p>

## Access Instance 
The Output of Terraform is the instance public Ip 

