# Running Google Colab Notebooks in Visual Studio Code: A Step-by-Step Guide

![Installing Jupyter Extension in VS Code](/assets/img/howtoruncolabcodeinvscode/img/overview.gif)


## Introduction

Google Colab has become a popular platform for data scientists, machine learning engineers, and researchers due to its free access to GPU resources and easy-to-use interface. However, Colab has limitations, especially in its free version. Many developers prefer working in Visual Studio Code (VS Code) for its rich set of plugins and AI automation capabilities.

This blog post will guide you through the process of running your Colab notebooks in VS Code, allowing you to leverage your local resources and take advantage of VS Code's powerful features.

## Why Run Colab Notebooks in VS Code?

Before we dive into the steps, let's briefly discuss why you might want to run your Colab notebooks in VS Code:

1. **Enhanced Development Environment**: VS Code offers a more comprehensive set of tools and extensions for coding, debugging, and version control.

2. **Local Resource Utilization**: You can use your local machine's resources, which can be beneficial if you have a powerful setup.

3. **Customization**: VS Code allows for extensive customization of your development environment.

4. **Offline Work**: You can work on your notebooks without an internet connection.

5. **Integration with Other Tools**: VS Code integrates well with various development tools and workflows.

## Prerequisites

Before we begin, ensure you have the following:

- Visual Studio Code installed on your local machine
- Python installed on your system
- Basic familiarity with Jupyter notebooks and Google Colab

## Step-by-Step Guide

### 1. Exporting the Jupyter Notebook from Google Colab

The first step is to export your notebook from Google Colab:

1. Open your notebook in Google Colab.
2. Go to "File" in the top menu.
3. Select "Download" and then choose "Download .ipynb".

![Exporting Jupyter Notebook from Colab](/assets/img/howtoruncolabcodeinvscode/img/image_0.png)

This will download your notebook as an .ipynb file to your local machine.

### 2. Installing the Jupyter Extension in VS Code

If you haven't already installed the Jupyter extension in VS Code, follow these steps:

1. Open VS Code.
2. Click on the Extensions icon in the left sidebar (it looks like four squares).
3. Search for "Jupyter" in the extensions marketplace.
4. Find the official Jupyter extension and click "Install".

![Installing Jupyter Extension in VS Code](/assets/img/howtoruncolabcodeinvscode/img/image_1.png)

This extension allows VS Code to work with Jupyter notebooks seamlessly.

### 3. Importing the Notebook into VS Code

Now that you have the Jupyter extension installed, you can import your notebook:

1. In VS Code, go to "File" > "Open Folder" and select the folder where you saved your exported notebook.
2. Your notebook should appear in the file explorer on the left side of VS Code.
3. Click on the notebook file to open it.

### 4. Activating the Jupyter Python Runtime

To run your notebook, you need to activate a Python runtime:

1. With your notebook open in VS Code, look for the "Select Kernel" button in the top right corner of the notebook.
2. Click on it and select "Python Environments".
3. Choose the Python environment you want to use. If you don't see your preferred environment, you may need to install it or configure VS Code to recognize it.

![Activating Jupyter Python Runtime](/assets/img/howtoruncolabcodeinvscode/img/image_2.png)

### 5. Running Your Notebook

Now you're ready to run your notebook:

1. You can run individual cells by clicking the play button next to each cell or by using the keyboard shortcut Shift+Enter.
2. To run all cells, you can use the "Run All" button at the top of the notebook or in the command palette (Ctrl+Shift+P, then search for "Run All").

## Differences Between Colab and Local Execution

While running your notebook locally in VS Code, keep in mind some key differences from Colab:

### Resource Limitations

When running on your local machine, you're limited to your own hardware resources. This means:

- You won't have access to Colab's free GPUs.
- The execution speed will depend on your local machine's capabilities.
- You may need to install additional libraries that were pre-installed in Colab.

### File System Access

In VS Code, you have direct access to your local file system. This can be both an advantage and a potential issue:

- You can easily work with local files and directories.
- You may need to modify file paths in your code that were specific to Colab's file system.

### Library Management

Managing libraries locally requires a bit more effort:

- You'll need to install required libraries manually using pip or conda.
- Be mindful of version conflicts and dependencies.

## Tips for a Smooth Transition

To make your transition from Colab to VS Code smoother, consider the following tips:

1. **Create a Virtual Environment**: It's a good practice to create a virtual environment for your project to manage dependencies effectively.

2. **Install Required Libraries**: Review your notebook and install all necessary libraries in your local environment.

3. **Check for Colab-Specific Code**: Look for any Colab-specific code (like mounting Google Drive) and remove or replace it as needed.

4. **Adjust File Paths**: Update any file paths to work with your local file system.

5. **Consider Using Git**: VS Code has excellent Git integration. Consider using version control for your notebooks.

6. **Explore VS Code Extensions**: Look for extensions that can enhance your workflow, such as code formatters, linters, or AI assistants.

## Advanced: Connecting VS Code to Colab's Resources

While this tutorial focuses on running notebooks locally, it's worth noting that it's possible to connect VS Code to Colab's resources, including their GPUs. This process is more complex and involves:

1. Setting up SSH access to the Colab VM.
2. Configuring port forwarding.
3. Using VS Code's remote development features.

This advanced setup allows you to use Colab's powerful resources while working in VS Code's environment. However, it requires more technical knowledge and setup time.

## Conclusion

Running Google Colab notebooks in Visual Studio Code opens up new possibilities for your data science and machine learning projects. By following this guide, you can leverage the power of VS Code's extensive feature set while working with your familiar Jupyter notebooks.

Remember that while local execution gives you more control and customization options, it also means you're responsible for managing your environment and resources. Take the time to set up your local development environment properly, and you'll enjoy a powerful and flexible workflow for your projects.

Whether you choose to run your notebooks locally or explore advanced setups to connect to Colab's resources, VS Code provides a robust platform for your data science and machine learning endeavors. Happy coding!