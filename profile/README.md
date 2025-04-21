
## YAFAI-Yet Another Framework for Agentic Interfaces  🚀

### YAFAI-Core : Define and Deploy Agentic interfaces. 
#### Consume YAFAI's multi agent system on any platform mobile,web,desktop or even terminal via YAFAI Link.

**What is an Agentic Workspace?** <br>
YAFAI's agentic workspaces are a collection of purpose built agents working together to achieve a common goal.Think of this like a team of helpful assistants that can solve tasks for you using available integrations.

![Yafai Workspaces](https://github.com/YAFAI-Hub/core/blob/main/assets/yafai-workspaces.png)

### What is YAFAI?

**Yafai** is a lightweight, high-performance multi-agent orchestrator built for power users. It’s designed to be a **drop-in executable** that exposes a fully customizable, config-driven agentic interface — no extra setup, no boilerplate.

Yafai follows an **opinionated orchestration flow**, but gives you **complete control** over what happens within it. Everything is defined through **declarative YAML**, making the system easy to configure, extend, and integrate — all from a single binary.

Read more about the design choice at [Design Doc](https://github.com/YAFAI-Hub/core/blob/main/assets/design.md).

One binary. Full control. Declarative multi-agent orchestration made simple.

---

# Setup Instructions

## Installation
 ```bash

    brew tap yafai-hub/yafai
    brew install yafai-core

    # when prompted enter the Groq API key.
    # create YAFAI config files and place them under ~/.yafai/configs/ , checkout samples under smaples/recipes.
    # WIP - to allow provider selection and setup through UI.
 ```

## Running YAFAI

### With TerminalUI [ Experimental ]

```bash
    #Terminal UI mode

    yafai-core -m tui 

    # try yafai-core -h for more options.
    # above command runs the link service and starts a TUI process for easy use.
    
```

<img src="https://github.com/YAFAI-Hub/core/blob/main/assets/tui-mode.png" width=800 height=480>


### Run YAFAI Link - No TerminalUI
```bash

    # brew install yafai-core as an executable run it

    yafai-core --mode link 

    # try yafai-core -h for more options.
    # above command exposes the link service and exposes the YAFAI workspace.
    # workspace can be integrated with any client - mobile/meb/desktop or terminal.

```

![Yafai Link](https://github.com/YAFAI-Hub/core/blob/main/assets/link-mode.png)



## Config-Driven Agentic Service Layer

Yafai exposes a config-driven agentic service layer. Pass a configuration file, and it exposes agentic interfaces ready to use. This approach allows for dynamic agent definition and connection, making it easy to adapt to different use cases.

1.  Sample configuration is available at samples/recipes.

    Sample for `config.yaml` structure:

    ```yaml
    # Example configuration
    name: "media_publisher" #workspace_name
    scope: "content_creation" #workspace_creation
    planner: #planner definition
        model: "deepseek-r1-distill-llama-70b"
        provider: "groq"
    orchestrator: # orchestrator definition
        name: "editor_in_chief"
        description: "Oversees content planning, publishing flow, and quality checks."
        scope: "Help user plan, create, edit, and publish media content efficiently."
        model: "llama-3.1-8b-instant"
        provider: "groq"
        goal: "Streamline end-to-end media content publishing."
        team: #team of agents
            content_creator:
                name: "content_creator"
                capabilities: "generate articles, scripts, and media content"
                description: "Creates engaging content for publishing."
                model: "llama-3.2-1b-preview"
                provider: "groq"
                goal: "Produce high-quality media-ready content."
                depends: "editor_in_chief"
                responds: "editor_in_chief"
                status: "Initialised"
            content_editor:
                name: "content_editor"
                capabilities: "edit and enhance generated content"
                description: "Improves clarity, grammar, tone, and formatting."
                model: "llama-3.2-1b-preview"
                provider: "groq"
                goal: "Ensure publication-ready quality."
                depends: "content_creator"
                responds: "editor_in_chief"
                status: "Initialised"
        vector_store: "none"
    ```

---
---

# YAFAI Skills 🚀 - Tools and integrations for YAFAI.

## Yafai Skills is the Tools Framework for YAFAI Agents

### Description

YAFAI skills is the tools framework for extending capabilities to YAFAI agents.

### Features

- REST API based
- Auth supported through API token, can piggy back on exisiting RBAC.

### Installation

```bash
brew tap yafai-hub/yafai
brew install yafai-skill

```

### Parameters to Skill Engine

Run the binary with the following parameters to start Skill Engin

```
//run the skill engine with below params

yafai-skill -m [manifest file path] -k [api key for the service]
yafai-skill -h //for help on parameters.

```

### Skill Manifest File

Skill manifest file is the center point for defining the skill server, below is the v0.0.1 version of the manifest file

```yaml
name: ServiceName
description: YAFAI skills for ServiceName
actions:
  ACtion1:
    desc: Action Description
    base_url: Service URL with place holders Eg. service.com/{url_path}/{query_param}
    method: POST
    params:
      - {name: test-param1, type: string, in: path, desc: "Param1.", required: true}
      - {name: test-param2, type: string, in: query, desc: "Param2.", required: true}
      - {name: test-param3, type: string, in: body, desc: "Param3", required: true}
    response_template: #golang text templates for preparing response
      success: "Completed action with {{.response}}'"
      failure: "Failed to complete action : {{.Error}}"

```

### Pre build Manifests Coming Soon!!

### License

Apache 2.0 License - see LICENSE.md for details

###
