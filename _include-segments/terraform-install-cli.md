## Step 1. Install the Terraform CLI
{: step}
{: #terraform-install-cli}

Complete the following steps to install the Terraform CLI:

1. Create a terraform folder on your local machine, and navigate to your terraform folder.

    ```terraform
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the Terraform version that you want. For example, you can download `terraform_1.12.2_darwin_amd64.zip` for a MacOS. See [Install Terraform](https://developer.hashicorp.com/terraform/install){: external}.

3. Extract the Terraform zip file and copy the files to your terraform directory. Run the following commands:

    ```text
    chmod +x terraform
    ```
    {: codeblock}

    ```
    sudo mv terraform /usr/local/bin/
    ```
    {: codeblock}

4. Verify that the installation is successful by using a terraform command to confirm the version.

    ```text
    terraform --version
    ```
    {: pre}
