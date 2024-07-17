---
layout: post
title: "Integrating Remote GPUs into Your Local Development Environment with VSCode"
published: true
date: 2024-07-16
excerpt: "As developers, we often find ourselves in situations where our local machines just don't have enough power for resource-intensive tasks like fine-tuning machine learning models. While solutions like Google Colab or SSH connections to remote servers exist, they often lack the comfort and familiarity of our favorite development environments. What if we could harness the power of remote resources while still enjoying the rich ecosystem of Visual Studio Code? In this tutorial, we'll explore how to do just that using a cloud provider that offers virtual machines with powerful CPUs and GPUs."
---

# Integrating Remote GPUs into Your Local Development Environment with VSCode

![Demo of VSCode remote GPU integration](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/demo.gif)

As developers, we often find ourselves in situations where our local machines just don't have enough power for resource-intensive tasks like fine-tuning machine learning models. While solutions like Google Colab or SSH connections to remote servers exist, they often lack the comfort and familiarity of our favorite development environments. What if we could harness the power of remote resources while still enjoying the rich ecosystem of Visual Studio Code? In this tutorial, we'll explore how to do just that using a cloud provider that offers virtual machines with powerful CPUs and GPUs.

For this guide, we'll be using [RunPod](https://runpod.io?ref=7su8gs12) as our primary example. RunPod is a cloud computing platform that specializes in providing GPUs for machine learning and AI tasks. However, it's worth noting that there are several alternatives in the market:

1. [Vast.ai](https://cloud.vast.ai/?ref_id=145250): A marketplace for renting and lending GPUs, offering competitive prices for GPU compute power.
2. [DigitalOcean](https://www.digitalocean.com/pricing): A cloud infrastructure provider that offers a range of virtual machines, including some with GPUs, though their GPU offerings are more limited compared to specialized providers.

Each of these platforms has its strengths, and the choice depends on your specific needs and budget. This approach can be adapted to work with any of these providers or similar services.

## Prerequisites

- Visual Studio Code installed on your local machine
- Basic familiarity with SSH and cloud computing concepts
- An account with a cloud provider (we'll be using [RunPod](https://runpod.io?ref=7su8gs12) in this tutorial)

Let's dive in!

## Step 1: Create an SSH Key

The first step is to create an SSH key that will allow secure access to your remote machine.

1. If you haven't already, generate an SSH key pair on your local machine.
2. Log in to your [RunPod](https://runpod.io?ref=7su8gs12) account (or your chosen cloud provider).
3. Navigate to the account settings or SSH key management section.
4. Add your public SSH key to authorize terminal access to your pods.

![RunPod SSH key management interface](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_0.png)

## Step 2: Create a Suitable Virtual Machine

Next, we'll set up a virtual machine (VM) with the computational resources we need.

1. In your cloud provider's dashboard, navigate to the section for creating new VMs or pods.
2. Choose between GPU and CPU options based on your requirements.
3. Select a configuration that suits your needs and budget.

For GPU-intensive tasks:
![RunPod GPU configuration options](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_1.png)

For CPU-focused work:
![RunPod CPU configuration options](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_2.png)

## Step 3: Note the SSH Connection Information

Once your VM is created, you'll need to note down the SSH connection details.

1. Locate the SSH connection information for your newly created VM.
2. Make note of the IP address and the SSH port number.

![RunPod SSH connection information](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_3.png)

## Step 4: Configure Visual Studio Code

Now that we have our remote machine set up, let's configure VSCode to connect to it.

1. Install the "Remote - SSH" extension in VSCode if you haven't already.

![VSCode Remote SSH extension](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_4.png)

2. Open your SSH config file (usually located at `~/.ssh/config`) and add an entry for your new VM:

```
Host myrunpod
    HostName <the IP of the VM>
    User root
    Port <the port of the VM>
    IdentityFile ~/.ssh/<YOUR SSH PRIVATE KEY>
```

Replace the placeholders with your actual VM IP, port, and the path to your SSH private key.

## Step 5: Connect to Your Remote VM from VSCode

With everything set up, you're now ready to connect to your remote VM directly from VSCode.

1. Open the Remote Explorer in VSCode (usually found in the left sidebar).

![VSCode Remote Explorer](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_5.png)

2. Click on "Connect to Host..." in the dropdown menu.

![VSCode Connect to Host option](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_6.png)

3. Select your configured SSH host from the list (in our example, it would be "myrunpod").

![VSCode SSH host selection](/assets/img/integrating-remote-gpus-into-your-local-development-environment-with-vscode/image_7.png)

4. VSCode will now connect to your remote VM. This might take a moment for the first connection as it sets up the necessary components on the remote machine.

## Step 6: Start Developing!

Congratulations! You're now connected to your remote VM through VSCode. You can start working on your projects, leveraging the power of your cloud-based resources while enjoying the familiar VSCode interface and extensions.
Happy coding, and may your remote development adventures be both productive and exciting!