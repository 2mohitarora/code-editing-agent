## Core Principles 

### What is an agent

Agents are systems that independently accomplish tasks on your behalf.

### Difference between agent and traditional software

While conventional software enables users to streamline and automate workflows, agents are able to perform the same workflows on users’ behalf with a high degree of independence.

Applications that integrate LLMs but don’t use them to control workflow execution, such as simple chatbots, single-turn LLMs are not agents.

### Core characteristics of agents

1. It leverages an LLM to manage workflow execution and make decisions. It recognizes when a workflow is complete and can proactively correct its actions if needed. In case of failure, it can halt execution and transfer control back to the user.

2. It has access to various tools to interact with external systems, both to gather context and to take actions. It can dynamically select the appropriate tools depending on the workflow’s current state, always operating within clearly defined guardrails.

### When should we build an agent

Building agents requires rethinking how your systems make decisions and handle complexity. Unlike conventional automation, agents are uniquely suited to workflows where traditional deterministic and rule-based approaches fall short.

Example: Payment Fraud Analysis
A traditional rules engine works like a checklist, flagging transactions based on preset criteria. In contrast, an LLM agent functions more like a seasoned investigator, evaluating context, considering subtle patterns, and identifying suspicious activity even when clear-cut rules aren’t violated. This nuanced reasoning capability is exactly what enables agents to manage complex, ambiguous situations effectively

Few inputs to consider before you decide to build an agent:

1. Complex decision-making: Workflows involving nuanced judgment, exceptions, or 
context-sensitive decisions, for example refund approval in customer service workflows.
2. Difficult-to-maintain rules: Systems that have become unwieldy due to extensive and intricate rulesets, making updates costly or error-prone, for example performing vendor security reviews. 
3. Heavy reliance on unstructured data: Scenarios that involve interpreting natural language, extracting meaning from documents, or interacting with users conversationally, for example processing a home insurance claim. 

### Agent design foundations

1. Model: The LLM powering the agent’s reasoning and decision-making
2. Tools: External functions or APIs the agent can use to take action
3. Instructions: Explicit guidelines and guardrails defining how the agent behaves

```
weather_agent = Agent(
    name="Weather agent",
    instructions="You are a helpful agent who can talk to users about the weather",
    tools=[get_weather]
)
```

#### Tools: 
Tools extend your agent’s capabilities by using APIs from underlying applications or systems. For legacy systems without APIs, agents can rely on computer-use models to interact directly with those applications and systems through web and application UIs, just as a human would.

Broadly speaking, agents need three types of tools:

1. Data: Enable agents to retrieve context and information necessary for executing the workflow. `Query transaction databases or systems like CRMs, read PDF documents, or search the web.`    
2. Action: Enable agents to interact with systems to take actions such as adding new information to databases, updating records, or sending messages. `Send emails and texts, update a CRM record, hand-off a customer service ticket to a human.`   
3. Orchestration: Agents themselves can serve as tools for other agents (covered in separate section)

#### Instructions:
High-quality instructions are essential for any LLM-powered app, but especially critical for agents. Clear instructions reduce ambiguity and improve agent decision-making, resulting in smoother workflow execution and fewer errors.

Best practices for agent instructions

1. Use existing documents
2. Prompt agents to break down tasks
3. Define clear actions
4. Capture edge cases

#### Orchestration:
Orchestration enable agents to execute workflows effectively.

1. Single Agent systems, where a single model equipped with appropriate tools and
instructions executes workflows in a loop.
2. Multi-Agent systems, where workflow execution is distributed across multiple
coordinated agents

General recommendation is to use a Single Agent system

#### Guardrails:
