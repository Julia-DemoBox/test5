# 🤖 User Journey: I want to build an AI Agent

> **Note**
>
> We recommend opening another browser tab to work through the following activities so you can keep these instructions open for reference.

> If you'd wish to reset your progress and select a different user journey, you can do so by clicking this button:
>
> [![Reset Progess](https://img.shields.io/badge/Reset--Progress-ff3860?logo=mattermost)](/issues/new?title=Reset+Journey&labels=reset-journey&body=🔄+I+want+to+reset+my+AI+learning+journey+and+start+from+the+beginning.%0A%0A**Please+click+on+Create+below,+then+wait+about+15+seconds.+Your+progress+will+be+reset,+this+issue+will+automatically+close,+and+you+will+be+taken+back+to+the+Welcome+step+to+select+a+new+user+journey.**)

## 📋 Pre-requisites

1. A GitHub account
2. [Visual Studio Code](https://code.visualstudio.com/) installed
3. [Node.js](https://nodejs.org/en) installed
4. An Azure subscription. Use the [free trial](https://azure.microsoft.com/free/) if you don't have one, or [Azure for Students](https://azure.microsoft.com/free/students/) if you are a student.
5. [Azure Developer CLI](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/install-azd?tabs=winget-windows%2Cbrew-mac%2Cscript-linux&pivots=os-windows) installed


## 📝 Overview

In this step, you will learn how to build a basic AI agent using the AI Foundry VS Code extension. An AI agent is a program powered by AI models that can understand instructions, make decisions, and perform tasks autonomously.

## Step 1️⃣: Create an Agent

These steps assume that you have completed the previous steps - installing the AI Foundry VS Code extension and setting your default AI Foundry project with a model deployed. 

> **Important**
>
> Agents are only supported in the following regions: **australiaeast, centraluseuap, eastus, eastus2, francecentral, japaneast, norwayeast, southindia, swedencentral, uksouth, westus, westus3**
> 
> At a later stage, you will add **bing grounding** to your agent, a service that works with all Azure OpenAI models except _gpt-4o-mini, 2024-07-18_. We therefore recommend using the _gpt-4o_ model for this journey
>
> If you are using a different region, please create a new Azure AI Foundry project, _(On the AI Foundry portal)_, in one of the supported regions and deploy a model there.

1.  **Update your working directory** 

    Create a new folder called `agent` in the `packages` directory of your project. This folder will contain the configuration files for your agent.

2.  **Create & configure an Agent** 

    Click on the AI Foundry icon in the Activity Bar. Under resources, ensure your default AI Foundry project is selected. Hover over the "Agents" section title and click the "+" (Create Agent) icon that appears.

    ![Create Agent Button](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/create-agent.png?raw=true)

    You'll be prompted to save the agent's configuration file. Assign the name `my-agent.yaml` and save the file in the agents folder you created earlier. Once saved, the yaml file and the Agent Designer will open for you to configure your agent.
    
    On the Agent Designer, 
    - Give your agent a name. i.e `my-agent` 
    - Enter a foundation model for your agent from your model list. This model will power the agent's core reasoning and language capabilities. _Example. gpt-4o_
    - System instructions for your agent. This tells the agent how it should behave. Enter the following:

      ```
      You are a helpful agent who loves emojis 😊. Be friendly and concise in your responses.
      ```
    - Parameters, i.e _temparature: 0.7_ 

    The yaml configuration file should look like this:
    
      ````yaml
      version: 1.0.0
      name: my-agent
      description: Description of the agent
      id: ''
      model:
        id: gpt-4o-mini
        options:
          temperature: 0.7
          top_p: 1
      instructions: >-
        You are a helpful agent who loves emojis 😊. Be friendly and concise in your
        responses.
      tools: [] # We'll add tools later
      ````
3.  **Deploy Agent** 

    Click on the **Deploy to Azure AI Foundry** button in the Agent Designer to deploy your agent to Azure AI Foundry Once created, the agent will pop up in the AI Foundry extension under the "Agents" section.

    ![Deploy to Azure AI Foundry Button](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/deploy-to-ai-foundry.png?raw=true)

## Step 2️⃣: Test the Agent in the Playground

Now that you've created and deployed your agent, you can test it in the Playground - an interface that allows you to interact with your agent and see how it responds to different inputs.

1.  **Open the Playground** 

    Right-click on the agent you just created in the "Agents" section and select **Open Playground**. Alternatively, you can expand the "Tools" section and click on "Agent Playground", then select your agent from the list.

    ![Agent Playground in tools](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/agent-playground-in-tools.png?raw=true)

2.  **Test the Agent** 

    In the Playground, you can start chatting with your agent. Try sending it a few messages to see how it responds. For example:
    - "Hi there!" 
    - Expect a friendly response with emojis 😎.

      ![Agent Playground](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/agent-playground.png?raw=true)

    - Then, try a prompt like _"What's the weather in Nairobi right now?"_
    - Expect a response like "I can't check live weather, but you can check a weather website for the latest updates! 🌤️"

      ![Agent Playground - weather response](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/agent-weather-response.png?raw=true)

The agent currently has limitations including not being able to access real-time information or perform specific tasks. It can only respond based on the instructions and the model's knowledge.

So in the next step, we will add a tool to the agent to make it more useful.

## Step 3️⃣: Add a Tool to the Agent

Tools calling is a powerful feature that allows your agent to perform specific tasks or access external data. In this step, we will add a tool to our agent that can use Bing Search to fetch real-time information. This will enable the agent to provide more accurate and up-to-date responses.

### Create a Bing Search resource

On the Azure portal, [create a bing resource](https://portal.azure.com/#create/Microsoft.BingGroundingSearch) (Grounding with Bing Search). Follow the prompts to create the resource. 

### Option 1: Connect to Bing Search via the AI Foundry Portal

Open the [AI Foundry portal](https://ai.azure.com/) and navigate to the "Agents" section. Click on the agent you created earlier to open its setup page, and click on the "+ Add" next to the **Knowledge** section.

![Add knowledge](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/add-knowledge.png?raw=true)

Add a new knowledge source by selecting the **Grounding with Bing Search** option under "Data Source".

![Select data source](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/add-data-sources.png?raw=true)

Create a new connection, select your bing resource, and select the **API Key** authentication method. Click on the **Connect** button to create the connection. 

Back on VS Code, refresh the "Resources" section in the AI Foundry extension and select your agent. You should see the new Bing Grounding tool listed under the "Tools" section.

![Bing grounding connection via portal](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/binggrounding-via-portal.png?raw=true)

### Option 2: Connect to Bing Search via the Extension

Create a tool configuration .yaml file called `bing.yaml` in the same directory as your agent configuration file (the agent folder). Paste the following code into the `bing.yaml` file:

```yaml
type: bing_grounding
id: bing_search
options:
  tool_connections:
    - /subscriptions/<Azure Subscription ID>/resourceGroups/<Azure Resource Group name>/providers/Microsoft.MachineLearningServices/workspaces/<Azure AI Foundry Project name>/connections/<Bing connection name>
```

  Replace the placeholders in the connection string under the tool_connections section with your information:

  - Azure Subscription ID
  - Azure Resource Group name
  - Azure AI Foundry Project name
  - Bing connection name

Save the `bing.yaml` file.

On the Agent Designer, click on the + icon next to the "Tools" section. This will prompt you to select a yaml file for the tool. Select the `bing.yaml` file you created earlier. Click on **Deploy to Azure AI Foundry** to deploy your updated agent with the new tool to Azure AI Foundry.

<!-- ![Add bing tool via extension](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/add-bing-tool.png?raw=true) -->

Now that we have added the Bing Search API tool to our agent, we can test it in the Playground. Open the "Agent Playground" and send the agent a message like _"What's the weather in Nairobi right now?"_ The agent should use the Bing Search API tool to fetch the current weather information and respond with a friendly message.

![Weather with Bing](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/weather-with-bing.png?raw=true)


## Step 4️⃣: Agent playground to Code

The Agent Playground is a great way to test your agent's capabilities, but it's not the only way to interact with it. In this step, we will update our application to use the agent we just created. This will allow us to use the agent in our application and make it more useful.

### Add API

> Coming soon!

<!-- Install
In the terminal, navigate to the `webapp` directory and install the required packages:

```bash
npm install @azure/ai-projects @azure/identity
```

Update the `server.js` with code to interact with the agent. Add import statements to the top of the file:

```javascript
import {
  AIProjectsClient,
  DoneEvent,
  ErrorEvent,
  isOutputOfType,
  MessageStreamEvent,
  RunStreamEvent,
  ToolUtility,
} from "@azure/ai-projects";
import { DefaultAzureCredential } from "@azure/identity";
```

Then, add the following code to the `server.js` file to create a new instance of the AIProjectsClient and set up the necessary credentials: -->


### Update Chat UI

First, modify the ChatInterface class in `webapp/src/components/chat.js` Add a new property for mode (basic vs agent) 

```javascript
chatMode: { type: String } // Add new property for mode
```

In the constructor, set the default mode to "basic":

```javascript
this.chatMode = "basic"; // Set default mode to basic
```

In the render method, between the `Clear Chat button` and the `RAG-toggle component`, add a model-selector component. 

```javascript
  <div class="mode-selector">
    <label>Mode:</label>
      <select @change=${this._handleModeChange}>
        <option value="basic" ?selected=${this.chatMode === 'basic'}>Basic AI</option>
        <option value="agent" ?selected=${this.chatMode === 'agent'}>Agent</option>
      </select>
  </div>
```

Let's make the placeholder text conditional based on the selected mode

```javascript
  <input 
    type="text" 
    placeholder=${this.chatMode === 'basic' ? 
      "Ask about company policies, benefits, etc..." : 
      "Ask Agent"}
    .value=${this.inputMessage}
    @input=${this._handleInput}
    @keyup=${this._handleKeyUp}
  />
```

and the message sender display to show 'Agent' instead of 'AI' when the mode is set to 'agent':

```javascript
<span class="message-sender">${message.role === 'user' ? 'You' : (this.chatMode === 'agent' ? 'Agent' : 'AI')}</span>
```

![Agent mode placeholder]()

Add a new method `_handleModeChange` to handle the mode change event after the render method:

```javascript
_handleModeChange(e) {
  const newMode = e.target.value;
  if (newMode !== this.chatMode) {
    this.chatMode = newMode;
    clearMessages();
    this.messages = [];
  }
}
```

Let's improve the styling of the mode selector. Add the following CSS to `webapp/src/components/chat.css` after `.rag-toggle` styles:

```css
.mode-selector {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 1rem;
  background: rgba(50,50,50,0.5);
  padding: 6px 12px;
  border-radius: 18px;
  margin-right: auto;
}

.mode-selector label {
  color: #e0e0e0;
  white-space: nowrap;
}

.mode-selector select {
  background: #18191a;
  color: #fff;
  border: 1px solid #444;
  border-radius: 8px;
  padding: 4px 8px;
  font-size: 0.9rem;
  outline: none;
}

.mode-selector select:focus {
  border-color: #1e90ff;
}
```

![Mode selected is agent](https://github.com/juliamuiruri4/JS-Journey-to-AI-Foundry/blob/assets/js-ai-journey-assets/mode-agent.png?raw=true)


## ✅ Activity: Push your updated code to the repository

>**Note**
>
> To complete this user journey and **AUTOMATICALLY UPDATE** your progress, you MUST push your code to the repository as described below.
>
> Checklist:
> - [ ] Have a `agent` folder in the packages directory

> If you'd wish to jump to another step without completing this user journey, you can do so by clicking this button
>
> [![Skip to another journey](https://img.shields.io/badge/Skip--to--another--journey-ff3860?logo=mattermost)](/issues/new?title=Skip+Journey&labels=reset-journey&body=🔄+I+want+to+reset+my+AI+learning+journey+and+start+from+the+beginning.%0A%0A**Please+click+on+Create+below,+then+wait+about+15+seconds.+Your+progress+will+be+reset,+this+issue+will+automatically+close,+and+you+will+be+taken+back+to+the+Welcome+step+to+select+a+new+user+journey.**)

1.  **Push your changes to the repository:** In the terminal, run the following commands to add, commit, and push your changes to the repository:

    ```bash
    git add .
    git commit -m "Add agent"
    git push
    ```

2.  **Refresh the repo page:** After pushing your changes, **wait about 20 seconds then refresh your repository landing page. [GitHub Actions](https://docs.github.com/en/actions) will automatically update to the next step.**

## 📚 Further Reading

Here are some additional resources to help you learn more about building AI agents and extending their capabilities with tools:
- [Azure AI Agents JavaScript examples](https://github.com/Azure-Samples/azure-ai-agents-javascript)