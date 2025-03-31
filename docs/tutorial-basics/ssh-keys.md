---
sidebar_position: 6
---

# SSH Keys

SSH keys are a pair of public and private cryptographic keys used for secure authentication and encrypted communication when accessing remote systems using the Secure Shell (SSH) protocol. This provides a more secure alternative to password-based authentication.

Bitbucket Pipelines uses an SSH key pair (private and public) to securely connect with other services without the need for user/password authentication. These SSH keys can be generated in Bitbucket or you can provide your own SSH key.

## Creating Your SSH Key for Pipelines

Follow these steps to create and configure an SSH key pair for Bitbucket Pipelines:

### Step-by-Step Process

1. **Go to Your Repository**  
   Navigate to the repository in Bitbucket where you want to set up your pipeline.

2. **Open the Settings Page**  
   In the left sidebar, click on **Settings** to open the repository's settings.

3. **Navigate to Pipelines/SSH Keys**  
   In the settings menu, find and go to the `Pipelines/SSH Keys` section.

4. **Generate the SSH Key Pair**  
   Click on the **Generate keys** button. This will create an SSH key pair for your pipeline. 

5. **Copy the Public Key**  
   After the key pair is generated, the **public key** will be displayed. Copy this public key and add it to the `~/.ssh/authorized_keys` file on your server. This allows Bitbucket Pipelines to securely connect to the server.

   The **public key** should look similar to this:

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCpdxzPfACRBRSI8G7p3VhksluL4E/zyrXuLXF03P4Dz99PN02KQwdZRuxVsJbFZ6UWDuF8h+zaxHPdSVaLhtD6B9QLF7SNmzmmBcQtUmeUg0SxCI31x7PyZTGJZFXavDv+bsl7FK5HNhNyn/TXsXIBbD9CqWKPmgGFP97P2Gvyi1ez8Jr49ieP3CRE/bkz5TIzUS8JyfAoAvKagvAA64OL00mYfJsJGO/HyopCsNXGo3cfoprTTa+l8Dlwa30mcqRcLthCN65ercM2p8GMm7PFPfjpxjoP51KSEFEYH9b5gz6i5wfzTDyySQbg2ohOiwGcezbqED8UYC7fVzHfL8jJEr/aLjtT1i/CKPKYBkMTQtPf66xqkBqaxTIE7XcAVcrzVAMzRFXJG3eg/Vyu/LgLCav/7JoiMuWbSMiHxYn4bVgEtD4kAIyTOVl7KLwxQY51ZKK0P3TMtBn0oQ9PJNjxh/HmzsoxcjpjDPRz54Xbd3Jxgj+NNjsFVi561O2iC/s=

6. **Add the Public Key to Your Server**  
On your server, append the public key to the `~/.ssh/authorized_keys` file. Ensure that the `.ssh` directory has proper permissions (`700`), and the `authorized_keys` file has the correct permissions (`600`).

You can use the following command to add the public key to the `authorized_keys` file:

```bash
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCpdxzPfACRBRSI8G7p3VhksluL4E/zyrXuLXF03P4Dz99PN02KQwdZRuxVsJbFZ6UWDuF8h+zaxHPdSVaLhtD6B9QLF7SNmzmmBcQtUmeUg0SxCI31x7PyZTGJZFXavDv+bsl7FK5HNhNyn/TXsXIBbD9CqWKPmgGFP97P2Gvyi1ez8Jr49ieP3CRE/bkz5TIzUS8JyfAoAvKagvAA64OL00mYfJsJGO/HyopCsNXGo3cfoprTTa+l8Dlwa30mcqRcLthCN65ercM2p8GMm7PFPfjpxjoP51KSEFEYH9b5gz6i5wfzTDyySQbg2ohOiwGcezbqED8UYC7fVzHfL8jJEr/aLjtT1i/CKPKYBkMTQtPf66xqkBqaxTIE7XcAVcrzVAMzRFXJG3eg/Vyu/LgLCav/7JoiMuWbSMiHxYn4bVgEtD4kAIyTOVl7KLwxQY51ZKK0P3TMtBn0oQ9PJNjxh/HmzsoxcjpjDPRz54Xbd3Jxgj+NNjsFVi561O2iC/s=" >> ~/.ssh/authorized_keys
```

# Providing Your Own SSH Key for Bitbucket Pipelines

In some cases, you may want to use your own pre-existing SSH key pair for Bitbucket Pipelines instead of generating a new one within Bitbucket. This allows you to maintain control over your SSH keys and ensures consistency across different services.

## Steps to Provide Your Own SSH Key

### 1. **Generate an SSH Key Locally (if needed)**

If you don't already have an SSH key pair, you can generate one locally using the `ssh-keygen` command. 

Run the following command in your terminal (make sure to replace `your_email@example.com` with your actual email address):

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
