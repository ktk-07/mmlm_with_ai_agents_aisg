# What we need to do?
Mission: Develop a Multimodality Large Language Model or Agent

Skills & Tools:
- Model Finetune
- Prompt Engineering
- Python Programming Language
- Any open-source resources or commercial model api to enable the development of the M-LLM or Agents.

Deliverables:
- One slider of the developed LLM-powered solution, including description of the design architecture.
- Video demonstration of the LLM-powered model or agent.
- Including a text description that should explain the features and functionality of the project. Text description should also include:
    - Solution architecture introduction
    - Development tools used to build the project
    - APIs used in the project
    - Assets used in the project, including models and datasets
    - Libraries used in the project
    - The relevant problem statement

Including a link to the team's public Github repository with Readme, and can rebuild the results of your solution on benchmark.
  * Results of the solution on benchmark.
  * Results are to be obtained by machine's execution and not by human intervention.

Timeline:
- Meet the Partners & Challenge Announcement - 11 March
- Final submission deadline by participants - 25 April
- Selection and announcement of finalists - 14 May (All selected finalists will receive an email from TikTok)
- Grand Finale - 9 May (Finalists will be invited to present and compete in person at the AI Student Developer conference)
- Eligibility: Students pursuing Bachelors Y2 and above, Masters and PhD.
- Team size: 2 to 5

Evaluation:
- Criteria for shortlisting for the final: The top performers with the highest correctness scores on the leaderboard will be selected
- Criteria for the final: The leaderboard score, along with the scores for innovation and feasibility of the solutions presented during the session, will be selected.
- * Including a link to the team's public Github repository with Readme, and rebuilding the results of your solution on benchmark would serve as an effective measure against cheating

How to make a submission on the platform:
Steps in the attached PDF.

# Output file to upload for testing the output
The results file contains two columns 'question_id' and 'pred'.
• 'qid' is the 'qid' of the sample in the benchmark.
• 'pred' is the prediction result of your solution for each sample.

# Analysing the Data input
In analysingdata-input.MD

# Issues Faced by models 
Are there papers on how we should tackle these issue for understanding video and answering question about the video? 

The issue of:
1.Content Recognition Issues
-Models fail at temporal precision (knowing when exactly something happens).
-They default to high-probability answers without exact video-specific grounding.

2.Cognitive Shortcomings
-Lack of causal/social reasoning (e.g., inferring the reason behind an action).
-Poor at answering “Why” and “How” based on nuanced video scenes.

3.Error Susceptibility
-Easily fooled by misleading or wrongly-led adversarial questions.

How do we know if its an adversarial question? use some agetn?


# Some tools to tackle problems
- do post-training
- use fine-tuning for down stream task
    - Link extraction
    - sentiment analysis
- AI Agents
    - Agent Types
        - Prompt Template Agent
        - Tool Agent
        - Grammar Agent
        - Web Scraper Agent
        - Transcript Agent
            - We can use this cause they ask about specific actions in that timestamp
        - Video Agent
            - compare betweem temporal and spatiotemporal Video Understanding Model
            - so we have the video already. 
            - use somesort of api
        - Youtube comment agent?
        - Down Stream Task Agents
            - For example small lm for extracting links
            - For example 
- prompt engineering technique
    - Prompt Templates
    - Retrieval-Augmented Generation ( RAG )
        - Contextual RAG for better retrieval
        - Agentic RAG on top of all the tools
Knowledge graphs help?

Think about it even if i get the questions i would keep replaying

Given a Question -> Plan what the workers should do (Reasoning models)

agents should be able to communicate with each other too

# Initial Ideation - Some Solutions I can think off.
Supervised finetuning + agentic workflow + prompt design + multimodal fusion
- Just improving on tool calling?
I mean the only thing i can think of is an Agentic Workflow following the Orchestrator-Workers Architecture.

Workers Would be :
2 Video Agent to describe the video probably some video understanding agent
    - Powered By what?
    1 Video agent for spatiotemporal understanding 空间时间理解
        - Vit + Resnet
        - SLOWFAstT,INFLATED 3 da
        - analyse dynamic and spatial relationship of objects in video
        - how actions change over time ( event detection and action recogntion)
        - Powered by
            - Vid2Seq (Temporal Understanding Model)
    2 Video agent for temporal understanding
        - focus on analysing sequence and duration of event
        - order in which action occur
        - Powered by
            - SlowFast / TimeSformer (Spatiotemporal Model)
    
    CLIP / Flamingo (Multi-Modal VLM)


Transcript Agent 
    - Task
        - to get the transcript cause video models do not understand the video 
    - Powered By what?
        - 
Prompt template agent 
    - Task 
        - input tasks

Tool Agent
    - Task
    - Powered By what?
    
Synthesizer 
    - Task
        - would just be combining the multi-modal reasoning model with a prompt template (dynamic prompt template with each prompt template catering to a specific problem type).  

    - Powered By what

The reason why we use a Reasoning model is due to the reasoning capabilities.

Final solution: 
Have multiple orchestrator then try to combine the results



Fine-tuning on general-purpose reasoning, causal, or multi-hop QA datasets (VCR, SocialIQa, TVQA, etc.)
Fine-tuning small lightweight modules (e.g., link extraction, temporal event detection for frames)
Light PEFT (LoRA / QLoRA) on task-specific "worker" agents only

# How should i go about implementing this?
2 ways to go about it
1. FineTuning on each task first.
Make sure all the worker agents (basics just tool calls) does their job well
Video Agent can describe the video properly.(Can use a reasoning model for this so we can utilise the reasoning outputs)
Transcript Agent can generate transcript accurately. (But what if its have no audio or )
Prompt template agent uses the right prompt template after all the aggregated outputs.

2. Test raw architectures first meaning we just go straight into building the architectures first
orchestrator - workers immediately.
Need not make sure each task does what it does find just use basic models with no fine-tuning on the specific task
This is cause fine-tuning might not even be necessary. However this is rarely gonna be the case.

I think im gonna go with 2 then fine-tune, cause i feel i am fine-tuning prematurely if i do 1 first


# Some Chatgpt suggestion
What you could add:
Self-Consistency Validator Agent

After the Reasoning Model answers:
Check for contradictions.
Validate across adversarial questions (e.g., wrongly-led, rephrased).
Why?
This could help you score better on the robustness metric (batch-level correctness).

Context Compression Module

Before sending fused inputs to the Reasoning Model, compress using:
Dense captioning (summarize long transcripts)
Caption de-duplication (avoid redundant frame captions)


Is there any reason to do fine-tuning? if we fine-tune it seems like we are just overfitting to the dataset
Unless we are fine-tuning to something else?

# What are some metrics i should consider?
Not very relevant?
Bilingual Evaluation Understudy (BLEU)
Recall-Oriented Understudy for Generating Evaluation (ROUGE)  
Metric for Evaluation of Translations System with Ordering (METEOR)


# Some problems I found and my solution
1. We dont have enough compute/ data so theres no point training a model from scratch

Solution 1 
- do post-training / fine-tuning small LMs to run / prompt engineering technique

2. Problem 2 ( Lack of External Tool Awareness + Incomplete Text Parsing )
Basically what i found was that even with given system prompt, the openai/gemini/closed-sourced model were still not able to do a specific task.

For example i gave it a link but it still did not do very well . so it didnt search the link nor did find any related to the link.

Solution to Problem 1:
I was thinking of fine-tuning a small lm to do a downstream task to detect whether there is a link 
then somehow call another lm to keep on trying to extract a link

Some queries about this Problem
I guess this might be one of the deficienies of a model.
But im not sure if this is due to my large context cause im observing this with the chat instead of the API


# Brief Description of My Solution (Full and Finalise Description go into SOLUTION.MD)
    - Make Multi-modal Agent to be solve the solution
    We are using a Parallelized Agentic Workflow instead of an Autonomous Agent

# Objective
    - Reduce as much cost as possible

# Key High-level Technicals Tasks to do
- Setting up Tests to run the API for model
- Solution Architecture Design
    - Multi-architectural Design

# Tasks to Do ( Breaking the high-level tasks into low-level tasks )
- Setting up tests to run THE APIs for models

- Solution Architecture Design
    - 

