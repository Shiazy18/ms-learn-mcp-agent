# ms-learn-mcp-agent

## Summary

We'll build an agent that connects to a cloud-hosted MCP server. The agent will use AI-powered search to help developers find accurate, real-time answers from Microsoft's official documentation. This is useful for building assistants that support developers with up-to-date guidance on tools like Azure, .NET, and Microsoft 365. The agent will use the available MCP tools to query the documentation and return relevant results.

---

## Pre-Req

### To run locally create a .env file and add the below values in it

``` env
PROJECT_ENDPOINT="your_project_endpoint"
MODEL_DEPLOYMENT_NAME="your_project_endpoint"
```

replace the 'your_project_endpoint' placeholder with the endpoint for your project (copy from the project Overview page in the Azure AI Foundry portal) and ensure that the MODEL_DEPLOYMENT_NAME variable is set to your model deployment name (which should be gpt-4o).

### Run the below command

```code
python -m venv mcpenv
./mcpenv/bin/activate
pip install -r requirements.txt --pre azure-ai-projects mcp azure-ai-agents
```

### To run

```code
python client.py
```

When prompted, enter a request for technical information such as:

```code
Give me the Azure CLI commands to create an Azure Container App with a managed identity.
```

Wait for the agent to process your prompt, using the MCP server to find a suitable tool to retrieve the requested information. You should see some output similar to the following:

```code 
Created agent, ID: <<agent-id>>
MCP Server: mslearn at https://learn.microsoft.com/api/mcp
Created thread, ID: <<thread-id>>
Created message, ID: <<message-id>>
Created run, ID: <<run-id>>
Run completed with status: RunStatus.COMPLETED
Step <<step1-id>> status: completed

Step <<step2-id>> status: completed
MCP Tool calls:
    Tool Call ID: <<tool-call-id>>
    Type: mcp
    Type: microsoft_code_sample_search


Conversation:
--------------------------------------------------
ASSISTANT: You can use Azure CLI to create an Azure Container App with a managed identity (either system-assigned or user-assigned). Below are the relevant commands and workflow:

---

### **1. Create a Resource Group**
'''azurecli
az group create --name myResourceGroup --location eastus
'''


{{continued...}}

By following these steps, you can deploy an Azure Container App with either system-assigned or user-assigned managed identities to integrate seamlessly with other Azure services.
--------------------------------------------------
USER: Give me the Azure CLI commands to create an Azure Container App with a managed identity.
--------------------------------------------------
Deleted agent
```
Notice that the agent was able to invoke the MCP tool microsoft_code_sample_search automatically to fulfill the request.


You can run the app again (using the command python client.py) to ask for different information, In each case, the agent will attempt to find technical documentation by using the MCP tool.

