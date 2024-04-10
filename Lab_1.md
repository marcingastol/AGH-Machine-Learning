# Explore the Azure Machine Learning Workspace

Azure Machine Learning offers a robust platform for data science, enabling users to train and manage machine learning models efficiently. This lab serves as an introductory exploration into the Azure Machine Learning workspace, highlighting its core capabilities and the developer tools available. For those interested in a deeper understanding of these capabilities, additional labs are available for further exploration.

## Before You Start

- **Prerequisite**: Ensure you have an Azure subscription with administrative-level access.
- **Azure CLI with Azure Machine Learning Extension**: Ideal for automating infrastructure tasks through command-line instructions.
- **Azure Machine Learning Studio**: Offers a user-friendly interface for exploring workspace capabilities.
- **Python SDK for Azure Machine Learning**: Best suited for data scientists looking to submit jobs and manage models via Jupyter notebooks.

## Provisioning an Azure Machine Learning Workspace

The Azure Machine Learning workspace acts as a central hub for all resources and assets needed for model training and management. It can be provisioned through the Azure portal's interactive interface or via the Azure CLI, enhanced with the Azure Machine Learning extension. Automating provisioning through the CLI is recommended in production scenarios for integration into a DevOps workflow.

### Exercise: Provisioning through the Azure Portal

1. Sign in to [Azure Portal](https://portal.azure.com/).

![Alt text](.img\1\1.png)

![Alt text](.img\1\2.png)

2. Create a new Azure Machine Learning resource with the following configurations:

| **Resource Group**  | **Workspace Name**  | **Region**  | **Storage Account**  | **Key Vault**  | **Application Insights** | **Container Registry** |
|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |

   - **Subscription**: `Subskrypcja programu Visual Studio Enterprise`
   - **Resource Group**: `rg-dp100-labs`
   - **Workspace Name**: `mlw-dp100-labs`
   - **Region**: Choose the geographical region closest to you
   - **Storage Account**: Note the default new storage account created for your workspace
   - **Key Vault**: Note the default new key vault created for your workspace
   - **Application Insights**: Note the default new application insights resource created for your workspace
   - **Container Registry**: Set to None (automatically created upon first model deployment to a container)

![Alt text](.img\1\3.png)

![Alt text](.img\1\4.png)

![Alt text](.img\1\5.png)

![Alt text](.img\1\6.png)

3. Await the creation of the workspace and its associated resources, typically around 5 minutes.
   - **Note**: Advanced options for private endpoint access and custom data encryption keys are available but not utilized in this exercise.

# Explore the Azure Machine Learning Studio

Azure Machine Learning Studio is a web-based portal that provides access to the Azure Machine Learning workspace, allowing for the management of all assets and resources.

## Getting Started

1. Navigate to the resource group created by you.

![Alt text](.img\1\7.png)
![Alt text](.img\1\8.png)

2. Ensure the resource group includes your Azure Machine Learning workspace, Application Insights, a Key Vault and a Storage Account.

![Alt text](.img\1\9.png)

3. Select your Azure Machine Learning workspace.

## Launching the Studio

1. Click on `Launch studio` from the Overview page. This action will open a new tab in your browser to access the Azure Machine Learning Studio.

![Alt text](.img\1\10.png)

2. Close any pop-ups that may appear in the studio.

## Navigating the Studio

1. Observe the various pages displayed on the left side of the studio. If you see only symbols, click the ☰ icon to expand the menu and reveal the names of the pages.
2. Explore the **Authoring** section, which includes:
   - Notebooks
   - Automated ML
   - Designer
   
   These tools provide three distinct methods for creating your own machine learning models within the studio.

3. Examine the **Assets** section, encompassing:
   - Data
   - Jobs
   - Models
   
   Assets can be either utilized or generated during the training or scoring of a model. They serve to train, deploy, and manage your models, and can be versioned for historical tracking.

4. Review the **Manage** section, which includes Compute among other resources. These are essential infrastructural components required for training or deploying a machine learning model.

![Alt text](.img\1\11.png)

# Authoring a Training Pipeline

Exploring asset and resource use within the Azure Machine Learning workspace can be achieved by training a model. The Designer offers a straightforward method to author a model training pipeline.

> **Note:** Throughout your time in the studio, pop-ups may appear to guide you. These can be closed and ignored to focus on the lab instructions.

## Using the Designer

1. Navigate to the **Designer** page via the menu on the left side of the studio.

![Alt text](.img\1\12.png)

2. Select the **Regression - Automobile Price Prediction (Basic)** sample.

![Alt text](.img\1\13.png)

This action generates a new pipeline. Initially, a component loads raw automobile price data. Subsequently, the pipeline processes this data and employs a linear regression model to forecast prices for each automobile.

## Configuring and Submitting the Pipeline

1. Click **Configure & Submit** at the top of the page to initiate the *Set up pipeline job* dialogue.

![Alt text](.img\1\14.png)

2. On the **Basics** page, opt to **Create new** and designate the experiment's name as `train-regression-designer`, then click **Next**.

![Alt text](.img\1\15.png)

3. Proceed to **Next** on the **Inputs & outputs** page without altering any settings.

![Alt text](.img\1\16.png)

4. Upon reaching the **Runtime settings** page, you might encounter an error due to the absence of a default compute required to execute the pipeline.

![Alt text](.img\1\17.png)

# Creating a Compute Target

To execute any workload in the Azure Machine Learning workspace, a compute resource is essential. Azure Machine Learning enables the creation of cloud-based compute resources, allowing for scalable experiments and training scripts.

## Steps to Create a Compute Target

In the Azure Machine Learning studio:

1. Navigate to the **Compute** page via the menu on the left side.

![Alt text](.img\1\18.png)


### Types of Compute Resources

Azure Machine Learning supports four types of compute resources:

- **Compute Instances:** Managed virtual machines perfect for development phases, data exploration, and model experimentation.
- **Compute Clusters:** Scalable clusters of virtual machines designed for on-demand experiment code processing, suitable for production or automated jobs.
- **Kubernetes Clusters:** Utilized for training and scoring, these clusters are ideal for large-scale, real-time model deployment.
- **Attached Compute:** Allows for the attachment of existing Azure compute resources, like Virtual Machines or Azure Databricks clusters, to the workspace.

### Provisioning a Compute Instance or Cluster

For training a model using the Designer, select either a compute instance or cluster:

1. Go to the **Compute instances** tab.

![Alt text](.img\1\19.png)

2. Add a new compute instance with the following configurations:
   - **Compute Name:** Enter a unique identifier.
   - **Location:** Set automatically to match your workspace.
   - **Virtual Machine Type:** CPU
   - **Virtual Machine Size:** Standard_DS11_v2
   - **Available Quota:** Shows the number of dedicated cores available.
   - **Show Advanced Settings:** Observe but do not select the following options:
     - **Enable SSH Access:** Leave unselected unless you need SSH client access to the VM.
     - **Enable Virtual Network:** Typically unselected unless required for enhanced network security in an enterprise setting.
     - **Assign to Another User:** Unselected, unless assigning a compute instance to a specific data scientist.
     - **Provision with Setup Script:** Unselected, but useful for running a script on the remote instance upon creation.
     - **Assign a Managed Identity:** Unselected, but available for attaching system assigned or user assigned managed identities to access resources.

![Alt text](.img\1\20.png)

3. Click **Create** and wait for the compute instance to initialize and transition to **Running** state.

![Alt text](.img\1\21.png)

![Alt text](.img\1\22.png)


# Running Your Training Pipeline

After setting up a compute target, you are ready to execute your sample training pipeline using the Designer.

## Steps to Run the Training Pipeline

1. **Access the Designer**:
   - Navigate to the **Designer** page within the Azure Machine Learning studio.

![Alt text](.img\1\12.png)

2. **Select the Pipeline**:
   - Choose the **Regression - Automobile Price Prediction (basic)** pipeline draft from the list.

![Alt text](.img\1\13.png)

3. **Configure & Submit**:
   - Click on **Configure & Submit** at the top of the page to initiate the *Set up pipeline job* dialogue.

![Alt text](.img\1\14.png)

4. **Set Experiment Details**:
   - On the **Basics** page, click **Create new** and name the experiment `train-regression-designer`, then select **Next**.
   - Proceed by selecting **Next** on the **Inputs & outputs** page without altering any settings.

![Alt text](.img\1\15.png)

5. **Select Compute Target**:
   - In the **Runtime settings** section, use the **Select compute type** drop-down to choose **Compute instance**.
   - From the **Select Azure ML compute instance** drop-down, pick the compute instance you previously created.

![Alt text](.img\1\23.png)

6. **Submission**:
   - Click **Review + Submit** to overview the pipeline job settings.
   - Confirm by selecting **Submit** to initiate the training pipeline execution.

![Alt text](.img\1\24.png)

The submission triggers the training process on the specified compute instance, expected to conclude in roughly 10 minutes. While waiting, consider exploring additional features and pages within the studio.


# Using Jobs to View Your History

In the Azure Machine Learning workspace, every script or pipeline execution is recorded as a job. These jobs facilitate tracking and comparing various workloads, all while being grouped under experiments for organized analysis.

## Accessing Jobs

1. **Navigate to Jobs**:
   - Use the menu on the left side of the Azure Machine Learning studio to find and click on the **Jobs** page.

![Alt text](.img\1\25.png)

2. **Select an Experiment**:
   - Choose the `train-regression-designer` experiment to review its job runs. This provides an overview of all jobs within the experiment, offering a comparison point for multiple training pipelines to determine the most effective one.

3. **Review Job Details**:
   - Click on the most recent job listed under the `train-regression-designer` experiment to examine its components, identifying which have succeeded or failed. For ongoing jobs, you can track current progress.

![Alt text](.img\1\26.png)

4. **Expand Job Overview**:
   - For detailed insights, select the **Job overview** button at the top right to access the Pipeline job overview.

## Insights from Job Overview

- The **Overview parameters** section reveals critical job details such as the job’s status, the creator of the pipeline, creation date, and the total runtime, among others.

## Benefits of Using Jobs

- **Historical Analysis**: Jobs are a powerful tool for retrospectively understanding the actions taken by you or your team.
- **Experimentation**: They provide a means to monitor various model training sessions, aiding in the identification of the most effective model.
- **Production Monitoring**: In a production environment, jobs serve as a checkpoint to ensure automated processes are executing as intended.
- **Component Detailing**: Post-completion, each component's run details, including outputs, are available for review, enhancing understanding of the model's training process.

Jobs in Azure Machine Learning offer a comprehensive way to document, compare, and analyze the multitude of tasks executed within the workspace, serving both developmental and operational needs.
