# Agentic AI — Complete Exam + Interview Preparation

## 0. First: The Big Picture

You should be able to explain Agentic AI in one diagram:

```text
                    AGENTIC AI
                        │
        ┌───────────────┼────────────────┐
        │               │                │
     Reasoning       Planning          Memory
        │               │                │
   CoT / ReAct      Decomposition    Short-term
   Reflection       Plan-Execute      Long-term
   Self-consistency Dynamic replanning Episodic/Semantic
        │               │                │
        └───────────────┼────────────────┘
                        │
                      Tools
                        │
              ┌─────────┼─────────┐
              │         │         │
            APIs      Search     Code
              │         │         │
              └─────────┼─────────┘
                        │
                    Action
                        │
                     Result
                        │
                    Feedback
                        │
                  Correction
                        │
                    Final Goal
```

The fundamental idea:

> **LLM generates language. An agent uses an LLM as part of a system that can reason, plan, use tools, maintain state/memory, observe results, and take actions toward a goal.**

---

# PART 1 — INTRODUCTION TO AGENTIC AI

## 1. What is Agentic AI?

**Agentic AI** refers to AI systems designed to pursue a goal through a loop of:

```text
Goal
 ↓
Understand
 ↓
Plan
 ↓
Reason
 ↓
Act
 ↓
Observe result
 ↓
Evaluate
 ↓
Correct/replan
 ↓
Act again
 ↓
Goal achieved
```

Unlike a simple chatbot that produces one response, an agent can perform **multiple steps autonomously**.

### Example

User:

> "Find the cheapest flight from Delhi to Mumbai next Friday and prepare an itinerary."

A normal LLM might explain how to search flights.

An agent can:

1. Understand the request.
2. Determine the date.
3. Search flight APIs.
4. Compare prices.
5. Check timings.
6. Search hotels.
7. Construct an itinerary.
8. Ask for approval before booking.

---

# 2. LLM vs Agentic AI

This is one of the **most important exam/interview questions**.

| Feature                 | LLM                            | Agentic AI                 |
| ----------------------- | ------------------------------ | -------------------------- |
| Main purpose            | Generate content               | Achieve goals              |
| Reasoning               | Usually within one interaction | Can span multiple steps    |
| Planning                | Limited                        | Explicit planning possible |
| Tools                   | May have tool calling          | Core capability            |
| Memory                  | Usually context-based          | Can have persistent memory |
| Autonomy                | Low                            | Potentially high           |
| Environment interaction | Limited                        | Can observe and act        |
| Feedback loop           | Usually absent                 | Central                    |
| State                   | Mostly conversation context    | Explicit state possible    |
| Example                 | Chatbot answering question     | AI research agent          |

### Key difference

**LLM = brain/model**

**Agent = complete system using a model + tools + memory + planning + control loop**

This distinction is extremely important.

### Interview question

**Q: Is ChatGPT an agent?**

Best answer:

> A language model itself is not necessarily an agent. An agentic system can use an LLM as its reasoning component while adding tools, memory, planning, state management, execution and feedback loops.

---

# 3. Reactive vs Autonomous Systems

## Reactive System

A reactive system responds directly to the current input.

```text
Input → Response
```

Example:

```text
User: What is 2 + 2?
System: 4
```

It doesn't necessarily maintain a long-term objective.

### Characteristics

* Immediate response
* Limited planning
* Low autonomy
* Usually stateless or minimally stateful

---

# 4. Autonomous System

An autonomous system can pursue a goal with limited human intervention.

```text
Goal
 ↓
Plan
 ↓
Action
 ↓
Observation
 ↓
Decision
 ↓
Action
```

Example:

> "Monitor server health and resolve common failures."

The system could:

```text
Monitor
 ↓
Detect failure
 ↓
Diagnose
 ↓
Restart service
 ↓
Verify
 ↓
Escalate if unsuccessful
```

### Important distinction

**Reactive ≠ necessarily non-intelligent**

**Autonomous ≠ necessarily fully independent**

Autonomy exists on a spectrum.

---

# 5. Agents vs Workflows vs Pipelines

Very important interview topic.

## Pipeline

A pipeline is usually a fixed sequence.

```text
Input
 ↓
Step A
 ↓
Step B
 ↓
Step C
 ↓
Output
```

Example:

```text
Document
 ↓
OCR
 ↓
Text extraction
 ↓
Classification
 ↓
Database
```

The path is predetermined.

---

# 6. Workflow

A workflow can have branching and conditions.

```text
Input
 ↓
Classification
 ├── Type A → Process A
 └── Type B → Process B
```

It can contain:

* Sequential steps
* Parallel steps
* Conditional branching
* Events
* Human approval

But the workflow structure is generally predefined.

---

# 7. Agent

An agent can dynamically decide what to do next.

```text
Goal
 ↓
Reason
 ↓
Choose action
 ↓
Tool
 ↓
Observe
 ↓
Reason again
 ↓
Choose next action
```

### Core distinction

> **Workflow follows predefined logic; an agent dynamically determines the next action based on state, observations and goals.**

---

# 8. Types of Agents

Possible classification:

### 1. Simple/Reactive Agents

Respond to current input.

### 2. Goal-based Agents

Choose actions based on goals.

### 3. Planning Agents

Create multi-step plans.

### 4. Tool-augmented Agents

Use external tools/APIs.

### 5. Memory-enabled Agents

Maintain information across interactions.

### 6. Reflection Agents

Evaluate and improve their own outputs.

### 7. Hierarchical Agents

Use multiple levels of planning.

### 8. Multi-Agent Systems

Multiple specialized agents cooperate.

---

# PART 2 — AGENT ARCHITECTURES

# 9. What is Agent Architecture?

Agent architecture defines how the components of an agent interact.

A generic architecture:

```text
             Goal
              ↓
         ┌──────────┐
         │ Planner  │
         └────┬─────┘
              ↓
         ┌──────────┐
         │ Reasoner │
         └────┬─────┘
              ↓
         ┌──────────┐
         │  Tools   │
         └────┬─────┘
              ↓
         Environment
              ↓
         Observation
              ↓
           Memory
              ↓
          Feedback
              └──────→ Reasoner
```

---

# 10. ReAct Architecture

**ReAct = Reason + Act**

One of the most important architectures.

The agent alternates between reasoning and action.

```text
Thought/Reason
     ↓
Action
     ↓
Observation
     ↓
Thought
     ↓
Action
     ↓
Observation
```

### Example

Question:

> What is the current USD → INR rate?

Agent:

```text
Reason:
I need current exchange rate.

Action:
Call exchange-rate API.

Observation:
1 USD = ₹...

Reason:
Now I can answer.

Final answer
```

### Why ReAct?

Because the model doesn't have to produce the final answer immediately.

It can:

* reason
* use tool
* observe
* reason again

### Advantages

* Flexible
* Good for tool usage
* Handles dynamic environments
* Supports iterative reasoning

### Disadvantages

* More expensive
* More latency
* Can get stuck in loops
* Tool failures need handling
* Reasoning can still be incorrect

---

# 11. Plan-and-Execute

Instead of deciding each action independently, the agent first creates a plan.

```text
Goal
 ↓
Planner
 ↓
Plan
 ├── Step 1
 ├── Step 2
 ├── Step 3
 └── Step 4
       ↓
    Executor
       ↓
    Results
```

### Example

Goal:

> "Create a report about India's renewable energy sector."

Plan:

```text
1. Find recent data
2. Find government reports
3. Analyze trends
4. Compare years
5. Write report
6. Verify citations
```

Executor performs each step.

### Advantages

* Better organization
* Good for complex tasks
* Easier debugging
* Explicit planning

### Weaknesses

* Initial plan can be wrong
* Environment can change
* Requires replanning
* Planning itself costs tokens/time

---

# 12. ReAct vs Plan-and-Execute

| ReAct                            | Plan-and-Execute                   |
| -------------------------------- | ---------------------------------- |
| Interleaves reasoning and action | Plans first                        |
| Dynamic                          | More structured                    |
| Good for uncertain environments  | Good for predictable complex tasks |
| Replans naturally                | May require explicit replanning    |
| Can be simpler                   | Better for long tasks              |

### Interview question

**Q: Which is better?**

Correct answer:

> Neither is universally better. ReAct is useful when actions depend heavily on observations, while Plan-and-Execute is useful when the task has a meaningful multi-step structure that can be planned ahead.

---

# 13. Reflection-Based Agents

Reflection means an agent evaluates its own output.

```text
Generate
 ↓
Critique
 ↓
Identify problems
 ↓
Improve
 ↓
Final output
```

Example:

```text
Writer Agent
     ↓
Draft
     ↓
Critic Agent
     ↓
"Missing evidence"
     ↓
Writer
     ↓
Improved draft
```

### Common pattern

```text
Generator → Critic → Generator → Critic → Final
```

### Advantages

* Better quality
* Error detection
* Self-improvement

### Problems

* More computation
* Critic may make incorrect judgments
* Can repeatedly refine unnecessarily

---

# PART 3 — ADVANCED ARCHITECTURES

# 14. Tree of Thoughts — ToT

Tree of Thoughts explores **multiple reasoning paths** instead of following one reasoning chain.

Normal reasoning:

```text
A → B → C → D
```

Tree of Thoughts:

```text
             A
          /  |  \
         B   C   D
        / \      / \
       E   F    G   H
```

The system:

1. Generates candidate thoughts.
2. Evaluates them.
3. Expands promising branches.
4. Prunes poor branches.
5. Selects a solution.

### Useful when

* Search space is complex
* Multiple possible approaches exist
* Backtracking is useful

### Cost

Potentially much more expensive than a single reasoning path.

---

# 15. Graph of Thoughts — GoT

Tree structures are restrictive because a tree doesn't naturally allow arbitrary connections between thoughts.

Graph of Thoughts represents reasoning as a graph.

```text
A → B → D
↓   ↘   ↑
C → E → F
```

Thoughts can:

* combine
* branch
* merge
* revisit
* depend on multiple previous thoughts

### ToT vs GoT

| ToT                    | GoT                     |
| ---------------------- | ----------------------- |
| Tree                   | Graph                   |
| Branching              | Arbitrary relationships |
| Parent-child structure | General dependencies    |
| Easier to reason about | More flexible           |
| Less expressive        | More expressive         |

---

# 16. Hierarchical Agents

A hierarchical system has multiple levels.

```text
High-level Manager
       ↓
   Sub-planners
   ↓    ↓    ↓
Agent Agent Agent
   ↓    ↓    ↓
 Tools Tools Tools
```

### Example

Travel planning:

```text
Travel Manager
 ├── Flight Agent
 ├── Hotel Agent
 ├── Restaurant Agent
 └── Itinerary Agent
```

The manager coordinates specialized agents.

### Advantages

* Specialization
* Scalability
* Better decomposition

### Challenges

* Coordination overhead
* Communication cost
* Failure propagation
* State synchronization

---

# 17. Tool-Augmented Agents

An agent becomes significantly more capable when it can use tools.

Examples:

* Search API
* Calculator
* Database
* Code interpreter
* Weather API
* Email
* Browser
* Payment API

Architecture:

```text
User
 ↓
LLM
 ↓
Tool selection
 ↓
Tool
 ↓
Result
 ↓
LLM
 ↓
Response
```

### Important concept

**Tool calling ≠ agent by itself.**

A tool-calling model can simply call one predefined function.

An agent usually involves a broader control loop involving:

* goal
* state
* reasoning
* action
* observation
* feedback

---

# PART 4 — MEMORY ARCHITECTURES

# 18. Why Do Agents Need Memory?

Without memory:

```text
Interaction 1 → forgotten
Interaction 2 → forgotten
Interaction 3 → forgotten
```

With memory:

```text
Interaction
 ↓
Store
 ↓
Retrieve relevant information
 ↓
Use in future reasoning
```

---

# 19. Short-Term Memory

Short-term memory is information available within the current context.

Usually:

```text
Conversation history
+
Current instructions
+
Tool results
```

The LLM's context window acts as working memory.

### Advantages

* Fast
* Easy
* Directly available

### Limitations

* Context window limits
* Token cost
* Old information may be truncated
* Not ideal for long-term persistence

---

# 20. Long-Term Memory

Long-term memory persists beyond the current conversation/session.

A common implementation:

```text
Information
 ↓
Embedding
 ↓
Vector DB
 ↓
Similarity search
 ↓
Relevant memories
 ↓
LLM
```

Examples:

* User preferences
* Previous decisions
* Historical events
* Knowledge

---

# 21. Episodic vs Semantic Memory

Extremely important.

## Episodic Memory

Stores **events/experiences**.

Example:

> "On September 20, the user asked about React interview preparation."

Think:

**What happened?**

---

## Semantic Memory

Stores **facts/knowledge**.

Example:

> "React uses a component-based architecture."

Think:

**What do I know?**

### Comparison

| Episodic                     | Semantic         |
| ---------------------------- | ---------------- |
| Experiences                  | Facts            |
| Events                       | Knowledge        |
| "What happened?"             | "What is true?"  |
| Often time/context dependent | More generalized |

---

# 22. Persistent Memory Systems

Persistent memory survives beyond a single execution/session.

Typical architecture:

```text
Agent
 ↓
Memory Manager
 ↓
┌───────────────┐
│ Vector DB     │
│ SQL DB        │
│ Document DB   │
└───────────────┘
```

### Important design issue

Never blindly store everything.

A good memory system needs:

```text
Write policy
+
Storage
+
Retrieval
+
Ranking
+
Update
+
Deletion
+
Privacy
```

---

# PART 5 — PLANNING & REASONING

# 23. Chain-of-Thought

Chain-of-Thought refers to reasoning through intermediate steps before reaching an answer.

Conceptually:

```text
Problem
 ↓
Intermediate reasoning
 ↓
Intermediate reasoning
 ↓
Conclusion
```

Example:

```text
Problem:
A = 10
B = 20
What is A+B?

Reasoning:
10 + 20 = 30

Answer:
30
```

### Why useful?

Complex tasks often benefit from decomposing the problem.

### Important interview point

Chain-of-thought is a **reasoning technique**, not an agent architecture.

---

# 24. Self-Consistency

Self-consistency generates multiple reasoning paths and chooses the answer that is most consistent.

```text
Problem
 ├── Reasoning path 1 → Answer A
 ├── Reasoning path 2 → Answer A
 ├── Reasoning path 3 → Answer B
 ├── Reasoning path 4 → Answer A
 └── Reasoning path 5 → Answer A

                    ↓

             Answer A
```

It is particularly useful when multiple reasoning paths can be sampled.

### Difference

**CoT:**

```text
One reasoning path
```

**Self-consistency:**

```text
Multiple reasoning paths
+
Aggregation
```

---

# 25. Task Decomposition

A large task is divided into smaller tasks.

Example:

```text
Build e-commerce website
        ↓
 ┌──────┼────────┐
Auth   Product   Payment
 │       │         │
Login   CRUD      Gateway
Signup  Search    Refund
```

### Why?

Smaller tasks are:

* easier to execute
* easier to verify
* easier to retry
* easier to parallelize

---

# 26. Step-by-Step Planning

Instead of solving everything at once:

```text
Goal
 ↓
Step 1
 ↓
Step 2
 ↓
Step 3
 ↓
Step 4
```

This is useful when each step depends on previous results.

---

# 27. Dynamic Replanning

This is a major agentic concept.

Suppose:

```text
Plan:
1. Search API
2. Fetch data
3. Analyze
4. Generate report
```

But API fails.

A static system:

```text
FAIL
```

An agent:

```text
API fails
 ↓
Observe failure
 ↓
Replan
 ↓
Use alternate source
 ↓
Continue
```

Therefore:

> **Dynamic replanning means modifying the execution plan based on new information, failures, or environmental changes.**

---

# PART 6 — DECISION MAKING

# 28. Action Selection

The agent must determine:

> "What should I do next?"

Possible actions:

```text
Search
Calculate
Ask user
Call API
Use database
Generate answer
Retry
Stop
```

The decision can depend on:

* goal
* current state
* observations
* tool availability
* constraints
* previous actions

---

# 29. Error Correction

An agent should detect failures.

Example:

```text
Tool call
 ↓
Error
 ↓
Analyze error
 ↓
Retry / modify input / alternate tool
 ↓
Verify
```

### Three common strategies

**Retry**

Same action again.

**Repair**

Change parameters/input.

**Fallback**

Use another method.

---

# 30. Feedback Loops

Feedback is central to agentic behavior.

```text
Action
 ↓
Result
 ↓
Evaluation
 ↓
Feedback
 ↓
Correction
 ↓
Action
```

Without feedback, an agent may continue making the same mistake.

---

# PART 7 — AGENT DESIGN PATTERNS

# 31. Tool-Calling Pattern

```text
User
 ↓
LLM
 ↓
Determine tool
 ↓
Tool call
 ↓
Result
 ↓
LLM
 ↓
Answer
```

Example:

```text
"Convert $100 to INR"

LLM → currency_converter(100, USD, INR)
API → ₹...
LLM → answer
```

---

# 32. Planner–Executor Pattern

```text
             Goal
              ↓
           Planner
              ↓
          Task Plan
              ↓
           Executor
              ↓
        Tool/Action
              ↓
            Result
              ↓
          Evaluation
```

Good for:

* Research
* Long tasks
* Complex workflows

---

# 33. Reflection / Self-Improvement Pattern

```text
Generate
   ↓
Evaluate
   ↓
Critique
   ↓
Improve
   ↓
Evaluate again
```

Can be implemented using:

* same LLM
* separate critic model
* rule-based validator
* another specialized agent

---

# 34. Sequential Workflow

```text
A → B → C → D
```

Example:

```text
Extract text
 ↓
Summarize
 ↓
Translate
 ↓
Format
```

Simple and deterministic.

---

# 35. Parallel Agents

Independent tasks execute simultaneously.

```text
             Manager
          /     |      \
       Agent A Agent B Agent C
          \     |      /
             Results
                ↓
             Aggregator
```

Example:

Research:

```text
Agent A → News
Agent B → Papers
Agent C → Market data
Agent D → Government data
```

Then aggregate.

### Benefit

Lower total latency when tasks are independent.

---

# 36. Event-Driven Agents

The agent responds to events.

```text
Event
 ↓
Trigger
 ↓
Agent
 ↓
Action
```

Example:

```text
Payment failed
 ↓
Event
 ↓
Agent
 ↓
Investigate
 ↓
Notify customer
```

Another example:

```text
Server CPU > threshold
 ↓
Monitoring event
 ↓
Agent
 ↓
Diagnose
 ↓
Remediate
```

---

# PART 8 — SAFETY PATTERNS

# 37. Guardrails

Guardrails constrain agent behavior.

Examples:

* Don't access unauthorized data.
* Don't execute dangerous commands.
* Don't send emails without permission.
* Don't expose secrets.
* Don't exceed budget.

Architecture:

```text
Input
 ↓
Guardrail
 ↓
Agent
 ↓
Action
 ↓
Guardrail
 ↓
Output
```

---

# 38. Validation Layers

Validation verifies whether an action/result is acceptable.

Example:

```text
Agent generates SQL
 ↓
SQL validator
 ↓
Safe?
 ├── Yes → Execute
 └── No → Reject
```

Types:

### Input validation

Check incoming data.

### Tool validation

Check tool arguments.

### Output validation

Check generated result.

### State validation

Ensure system state remains valid.

---

# 39. Human Approval Loops

Some actions should require humans.

```text
Agent
 ↓
Proposed action
 ↓
Human approval
 ├── Approve → Execute
 └── Reject → Replan
```

Especially important for:

* Financial transactions
* Legal decisions
* Production deployments
* Account deletion
* Sensitive communications

This is called **Human-in-the-loop (HITL)**.

---

# PART 9 — MOST IMPORTANT COMPARISONS

## LLM vs Agent

**LLM**

```text
Input → Generate
```

**Agent**

```text
Goal
 ↓
Reason
 ↓
Plan
 ↓
Act
 ↓
Observe
 ↓
Reason
 ↓
Act
```

---

## Agent vs Workflow

**Workflow:**

> predefined process

**Agent:**

> dynamic decision-making system

---

## ReAct vs Reflection

**ReAct**

> Think → Act → Observe

**Reflection**

> Generate → Critique → Improve

---

## ReAct vs Plan-and-Execute

**ReAct:**

> Decide action dynamically.

**Plan-and-Execute:**

> Create plan first, then execute.

---

## ToT vs GoT

**ToT:**

> Tree of reasoning paths.

**GoT:**

> Graph of reasoning relationships.

---

## Episodic vs Semantic Memory

**Episodic:**

> Events/experiences.

**Semantic:**

> Facts/knowledge.

---

## Short-Term vs Long-Term

**Short-term:**

> Current context.

**Long-term:**

> Persistent storage.

---

## Sequential vs Parallel Agents

**Sequential:**

```text
A → B → C
```

**Parallel:**

```text
A ─┐
B ─┼→ Aggregator
C ─┘
```

---

# PART 10 — HIGH-FREQUENCY INTERVIEW QUESTIONS

## Q1. What is an AI agent?

> An AI agent is a system that uses reasoning, planning, memory, tools and feedback to autonomously or semi-autonomously pursue a goal by interacting with its environment.

---

## Q2. What makes an agent different from an LLM?

> An LLM primarily generates predictions or responses, whereas an agentic system adds components such as state, planning, tool use, memory, action execution and feedback loops around the model.

---

## Q3. What is the agent loop?

```text
Observe
 ↓
Reason
 ↓
Plan
 ↓
Act
 ↓
Observe
```

---

## Q4. Why do agents need tools?

Because the LLM's internal knowledge is insufficient for many real-world tasks.

Tools provide:

* current information
* computation
* external data
* real-world actions
* database access

---

## Q5. Can an agent work without tools?

Yes.

An agent can reason and operate using internal knowledge and memory, but tools significantly increase its ability to interact with external environments.

---

## Q6. Why is memory important?

Memory allows an agent to maintain relevant information across steps or sessions instead of treating every interaction as completely independent.

---

## Q7. What is vector database memory?

Information is converted into embeddings and stored. Similarity search retrieves relevant memories later.

```text
Text
 ↓
Embedding
 ↓
Vector DB
 ↓
Similarity Search
 ↓
Relevant Memory
```

---

## Q8. What is hallucination?

Hallucination is when an AI system produces information that is unsupported, incorrect, or fabricated.

### Agent mitigation

* Retrieval
* Tool verification
* Validation
* Critic agents
* Grounding
* Human approval

---

## Q9. What is dynamic replanning?

> Changing the original plan when new observations, failures, constraints or environmental changes make the original plan unsuitable.

---

## Q10. What is reflection?

> Reflection is the process where an agent evaluates its own generated result or actions and uses the evaluation to improve subsequent output.

---

## Q11. What is self-consistency?

> Generating multiple reasoning paths and selecting an answer based on agreement or another aggregation strategy.

---

## Q12. What is hierarchical agent architecture?

> An architecture in which high-level agents or managers decompose goals and delegate subtasks to lower-level specialized agents.

---

## Q13. Why use multiple agents?

Specialization.

For example:

```text
Manager
├── Research Agent
├── Coding Agent
├── Testing Agent
└── Documentation Agent
```

Each agent can have specialized tools/prompts/constraints.

---

## Q14. What are the disadvantages of multi-agent systems?

Important:

* Higher latency
* Higher token/API cost
* Coordination complexity
* Shared-state problems
* Error propagation
* Harder debugging
* Potential infinite loops
* Security risks

---

# PART 11 — SCENARIO QUESTIONS

These are particularly useful for interviews.

## Scenario 1

**You need to build an AI research assistant. What architecture would you choose?**

Good answer:

```text
User
 ↓
Planner
 ↓
Research tasks
 ├── Web Search
 ├── Academic Search
 ├── Database
 └── Document Retrieval
       ↓
Parallel execution
       ↓
Aggregator
       ↓
Critic
       ↓
Final answer
```

Potential additions:

* citation validation
* memory
* human approval for sensitive actions

---

# Scenario 2

**An agent repeatedly calls a failing API. How do you fix it?**

Use:

```text
Failure detection
 ↓
Retry limit
 ↓
Backoff
 ↓
Alternative tool
 ↓
Replanning
 ↓
Human escalation
```

Never allow unlimited retries.

---

# Scenario 3

**An agent generates incorrect SQL.**

Architecture:

```text
LLM
 ↓
SQL Generator
 ↓
SQL Validator
 ↓
Permission Checker
 ↓
Read-only sandbox
 ↓
Execute
```

For destructive queries:

```text
Human approval
```

---

# Scenario 4

**You need to send emails automatically. Should the agent always send them?**

No.

Use risk-based approval:

```text
Low risk → automatic
Medium risk → validation
High risk → human approval
```

This is a practical application of guardrails and HITL.

---

# PART 12 — EXAM MCQs

## Q1. ReAct stands for:

A. Reason and Calculate
B. Retrieve and Act
C. Reason and Act
D. React and Analyze

**Answer: C**

---

## Q2. Which architecture explicitly separates planning and execution?

A. ReAct
B. Plan-and-Execute
C. Reflection
D. Reactive system

**Answer: B**

---

## Q3. Episodic memory primarily stores:

A. General facts
B. Events and experiences
C. Model weights
D. Tool definitions

**Answer: B**

---

## Q4. Semantic memory primarily stores:

A. Events
B. General knowledge/facts
C. Current context only
D. API logs only

**Answer: B**

---

## Q5. Which is persistent?

A. Context window only
B. Long-term memory
C. Temporary reasoning
D. Current prompt

**Answer: B**

---

## Q6. ToT uses:

A. Linear reasoning
B. Tree-structured reasoning
C. Database reasoning
D. Only tool calls

**Answer: B**

---

## Q7. GoT differs from ToT because GoT:

A. Cannot branch
B. Uses only one thought
C. Supports more general graph relationships
D. Doesn't use reasoning

**Answer: C**

---

## Q8. Which pattern generates → critiques → improves?

A. Reflection
B. Pipeline
C. Parallel execution
D. Event-driven architecture

**Answer: A**

---

## Q9. Which architecture is naturally suitable for independent subtasks?

A. Parallel agents
B. Sequential workflow
C. Single reactive agent
D. Linear pipeline

**Answer: A**

---

## Q10. Human approval is an example of:

A. Memory
B. HITL
C. Vector retrieval
D. Self-consistency

**Answer: B**

---

# PART 13 — VERY TRICKY MCQs

### Q11

A system receives an email and always performs:

```text
Extract → Classify → Store
```

without dynamically changing its process.

This is primarily:

A. Autonomous agent
B. Fixed pipeline
C. Reflection agent
D. ToT

**Answer: B**

---

### Q12

An agent decides:

> "The search API failed, so I'll use another API."

This demonstrates:

A. Static execution
B. Dynamic replanning
C. Semantic memory
D. Self-consistency

**Answer: B**

---

### Q13

Which memory answers:

> "What happened during the previous interaction?"

A. Semantic
B. Episodic
C. Procedural
D. Short-term only

**Answer: B**

---

### Q14

Which memory answers:

> "What is the capital of France?"

A. Episodic
B. Semantic
C. Event memory
D. Action memory

**Answer: B**

---

### Q15

Multiple independent agents research different sources simultaneously.

This is:

A. Sequential orchestration
B. Parallel orchestration
C. Reflection
D. ReAct

**Answer: B**

---

# PART 14 — 2-MARK QUESTIONS

Prepare these definitions almost word-for-word.

### Define Agentic AI.

AI systems capable of pursuing goals through reasoning, planning, tool use, memory, action and feedback.

### Define ReAct.

An agent architecture that interleaves reasoning with actions and observations.

### Define Plan-and-Execute.

An architecture where a planner creates a multi-step plan and an executor performs the planned tasks.

### Define reflection.

Self-evaluation of an agent's output or actions followed by improvement.

### Define ToT.

A reasoning approach that explores multiple branches of possible thoughts in a tree structure.

### Define GoT.

A reasoning approach that models thoughts and their relationships as a graph.

### Define short-term memory.

Information maintained within the current interaction/context.

### Define long-term memory.

Persistent information stored outside the immediate context and retrieved when required.

### Define episodic memory.

Memory of events and experiences.

### Define semantic memory.

Memory containing generalized facts and knowledge.

### Define guardrails.

Constraints and checks that restrict unsafe or invalid agent behavior.

### Define HITL.

Human-in-the-loop systems where humans participate in or approve important decisions/actions.

---

# PART 15 — 5-MARK QUESTIONS

## "Explain ReAct architecture."

Write:

1. Definition
2. Reasoning
3. Action
4. Observation
5. Iterative loop
6. Example
7. Advantages
8. Limitations

Diagram:

```text
        Goal
         ↓
      Reason
         ↓
       Action
         ↓
    Observation
         ↓
      Reason
         ↓
       Action
         ↓
      Result
```

---

## "Explain memory architecture."

```text
                   Agent
                     │
             ┌───────┴───────┐
             │               │
       Short-term       Long-term
             │               │
       Context window   Persistent DB
                             │
                    ┌────────┴───────┐
                    │                │
                Episodic         Semantic
```

Explain each.

---

# PART 16 — 10-MARK QUESTION

## "Explain complete Agentic AI architecture."

Use this answer structure:

```text
                       USER GOAL
                           ↓
                     ┌───────────┐
                     │  PLANNER  │
                     └─────┬─────┘
                           ↓
                     ┌───────────┐
                     │  REASONER │
                     └─────┬─────┘
                           ↓
              ┌────────────┼────────────┐
              ↓            ↓            ↓
            Search       Database       API
              │            │            │
              └────────────┼────────────┘
                           ↓
                        ACTION
                           ↓
                     ENVIRONMENT
                           ↓
                       OBSERVE
                           ↓
                       MEMORY
                           ↓
                      EVALUATOR
                           ↓
                  ┌────────┴────────┐
                  │                 │
                Good              Bad
                  │                 │
                Stop             Replan
                                    │
                                    └──→ Reason
```

Then explain:

* Planning
* Reasoning
* Tool use
* Memory
* Observation
* Feedback
* Replanning
* Safety

That gives you a very strong descriptive answer.

---

# PART 17 — WHAT EXAMINERS LOVE TO ASK

Memorize these **15 questions** first:

1. What is Agentic AI?
2. Difference between LLM and Agentic AI.
3. Reactive vs autonomous systems.
4. Agent vs workflow vs pipeline.
5. Types of agents.
6. Explain ReAct.
7. Explain Plan-and-Execute.
8. Explain Reflection.
9. ReAct vs Plan-and-Execute.
10. Explain Tree of Thoughts.
11. ToT vs GoT.
12. Explain hierarchical agents.
13. Explain short-term vs long-term memory.
14. Episodic vs semantic memory.
15. Explain tool-calling, planner-executor and reflection patterns.

Then:

16. Task decomposition
17. Dynamic replanning
18. Self-consistency
19. Action selection
20. Feedback loops
21. Parallel agents
22. Event-driven agents
23. Guardrails
24. Validation layers
25. Human-in-the-loop

---

# PART 18 — THE 30-SECOND MASTER REVISION

If you have almost no time, memorize this:

> **Agentic AI is a goal-oriented AI system that combines an LLM with planning, reasoning, memory, tools, action and feedback.**

```text
Agent
=
LLM
+
Planning
+
Reasoning
+
Tools
+
Memory
+
State
+
Feedback
+
Safety
```

### Architectures

```text
ReAct
= Reason → Act → Observe

Plan-and-Execute
= Plan → Execute

Reflection
= Generate → Critique → Improve

ToT
= Multiple reasoning branches

GoT
= Graph of reasoning relationships

Hierarchical
= Manager → Specialized agents

Multi-Agent
= Multiple cooperating agents
```

### Memory

```text
Short-term
= Current context

Long-term
= Persistent storage

Episodic
= Events

Semantic
= Facts
```

### Planning

```text
Decompose
 ↓
Plan
 ↓
Execute
 ↓
Observe
 ↓
Replan if needed
```

### Design patterns

```text
Tool Calling
Planner → Executor
Reflection
Sequential
Parallel
Event-driven
Guardrails
Validation
Human approval
```

---

# PART 19 — INTERVIEW "WHY" QUESTIONS

These distinguish someone who memorized definitions from someone who understands Agentic AI.

### Why not just use an LLM?

Because real-world tasks often require:

* external information
* deterministic computation
* persistent state
* actions
* multiple steps
* verification
* error recovery

---

### Why not make everything an agent?

Because agents introduce:

* nondeterminism
* latency
* cost
* debugging complexity
* security risks
* failure propagation

A deterministic workflow is often preferable when the process is well-defined.

---

### Why use multiple agents instead of one powerful agent?

Specialization can improve organization and isolation of responsibilities, but multi-agent systems also introduce coordination and communication overhead.

---

### Why is dynamic replanning important?

Because the real environment may differ from the initial assumptions.

```text
Initial plan ≠ always executable plan
```

An agent must respond to reality.

---

### Why is memory not simply "storing the conversation"?

Because useful memory requires:

```text
Selection
+
Storage
+
Retrieval
+
Ranking
+
Updating
+
Deletion
```

Blindly storing all conversations creates noise and retrieval problems.

---

# PART 20 — TOP 1% INTERVIEW INSIGHT

A very strong answer to almost any Agentic AI question should recognize this:

> **Agentic AI is not simply "LLM + tools." It is a control system.**

Think of it as:

```text
                ┌──────────────┐
                │     GOAL     │
                └──────┬───────┘
                       ↓
                ┌──────────────┐
                │    POLICY /  │
                │   REASONING  │
                └──────┬───────┘
                       ↓
                    ACTION
                       ↓
                ┌──────────────┐
                │  ENVIRONMENT │
                └──────┬───────┘
                       ↓
                  OBSERVATION
                       ↓
                    STATE
                       ↓
                   FEEDBACK
                       │
                       └────────→ POLICY
```

The **agentic loop** is the fundamental abstraction.

Everything else—ReAct, planning, memory, tools, reflection, multi-agent systems—is a way of improving some part of that loop.

---

## Final priority order for your exam

If your time is limited, study in this exact order:

**Tier 1 — Must know**

1. Agentic AI
2. LLM vs Agent
3. Agent vs Workflow vs Pipeline
4. ReAct
5. Plan-and-Execute
6. Reflection
7. Memory
8. Episodic vs Semantic
9. Tool calling
10. Guardrails/HITL

**Tier 2 — Very important**
11. ToT
12. GoT
13. Hierarchical agents
14. Multi-agent systems
15. Task decomposition
16. Dynamic replanning
17. Self-consistency
18. Feedback loops

**Tier 3 — Scenario/viva**
19. Parallel agents
20. Event-driven agents
21. Validation layers
22. Error correction
23. Action selection
24. Persistent memory

**Best exam strategy:** don't memorize isolated definitions. For every architecture, remember **Problem → Architecture → Flow → Example → Advantage → Limitation**. That lets you answer MCQs, 2-mark definitions, 5-mark explanations, and interview follow-ups from the same mental model.
