# Build Agent
```
mkdir code-editing-agent
cd code-editing-agent
go mod init agent
go mod tidy
```
# Run Base Version

```
export ANTHROPIC_API_KEY="NOT COMMITTED"
go run ch01/main.go
```
# Prompts for base version

```
Hey! I'm Mohit! How are you?

....Wait for response 

Can you come up with any nicknames that make fun of my first name?
```

# Explain the hypothesis and run the hypothesis
The basic idea is, you send a prompt to the model that says it should reply in a certain way if it wants to use “a tool”. Then you, as the receiver of that message, “use the tool” by executing it and replying with the result. 

```
You are a weather expert. When I ask you about the weather in a given location, I want you to reply with `get_weather(<location_name>)`. I will then tell you what the weather in that location is. Understood?

....Wait for response 

Hey, what's the weather in Munich?

....Wait for response 

Hot and humid, 28 degrees celcius

....Wait for response 
```

# What’s an agent? 
An LLM with access to tools, giving it the ability to modify something outside the context window. It gets some inputs, it decides based on that input, if it should use some tool, and which tool it should use, and use that tool  

Client Tools:
- https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/overview
- https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/computer-use-tool
- https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/text-editor-tool 

Server Tools:
- https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/web-search-tool 

# First tool - readFile
```
cd ch02
go run main.go
```
# Prompts for version with first tool
```
...Explain what's in secret-file.txt

Claude, buddy, help me solve the riddle in the secret-file.txt file

...Pretty cool right. You just give LLM a tool and it uses it when it thinks it’ll help solve the task. Remember: we didn’t say anything about “if a user asks you about a file, read the file”. We also didn’t say “if something looks like a filename, figure out how to read it”. No, none of that. We say “help me solve the thing in this file” and Claude realizes that it can read the file to answer that and off it goes.

what's in main.go?

What's going on in main.go? Be brief!
```
# Second Tool - List files 

```
cd ch03
go run main.go
```
# Prompts for version with first and second tool

```
what do you see in this directory?

Tell me about all the Go files in here. Be brief!

...Pretty cool - It's combining tools now 

```
--------------------------
# Third Tool - Edit files 
```
cd ch04
go run main.go
```

# Prompts for version with first, second and third tool
```
hey claude, create fizzbuzz.js that I can run with Nodejs and that has fizzbuzz in it and executes it

... In a seperate window run - node fizzbuzz.js

Please edit fizzbuzz.js so that it only prints until 15

... Editing works

Create a thankyou.js script that rot13-decodes the following string ‘Gunax lbh sbe nggraqvat Feninan naq Fureva, obgu bs lbh ner nznmvat!’ and prints it

... In a seperate window run node thankyou.js

Create a closing.js script that rot13-decodes the following string ‘Pbatenghyngvbaf ba ohvyqvat n pbqr-rqvgvat ntrag!’ and prints it

... In a seperate window run node closing.js
```
# Recap
- RAG vs Fine Tuning vs Function calling 
- Most of multi agent control logic is done by LLM itself 
    - If not, you can define a workflow 
- MCP in context of tools 
    -MCP  is a standardized protocol that defines how LLMs interact with tools