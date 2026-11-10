# Submission Template: Module 4 Lab 2: First boto3 Calls and Token Cost Math

Name: Khandker Ehmar Reza    Date: 11/09/2026

Fill this in as you work. Sections marked PREDICT must be written before you run the step.

---

## 0. Your unique values

These make your submission yours. Fill them in from your own account and your own run.

- **Your Region:** us-east-1
- **The model you chose and why:** Amazon Nova 2 Lite, because it was the easiest option and didn't have to think about restrictions
- **Your measured input and output token counts:** input 50, output 46
- **Your cost per call and the three volume figures:** 

per call 0.00010980000000000001
1000 calls a month costs 0.10980000000000001
50000 calls a month costs 5.49
2000000 calls a month costs 219.60000000000002

## 1. Predictions

Write the prediction BEFORE running. Then run, record the actual, and explain the gap. A wrong prediction reasoned honestly earns full credit.

### Step 2: Before you run it, predict: will the number of models VISIBLE in your Region equal the number you have ACCESS to?

**My prediction (written before running):**

> no

**What actually happened:**

> well yeah i was correct, given the fact that anthropic and openai have some extra work to access

**Why the difference, or why I was right:**

> anthropic requires extra details

### Step 4: Before you run the second set, predict: at temperature 1.0, will the five answers differ from each other more, less, or the same as at temperature 0.2? And will output token counts vary more?

**My prediction (written before running):**

> well i wasn't exactly told to change temperatures or anything in this lab, i also don't know how to change it. however, i do believe the output tokens will increase the more temperature they are given (the more creativity)

**What actually happened:**

> again, don't know. can't test. outdated module instructions (or template)

**Why the difference, or why I was right:**

> again, don't kow.

## 2. Break it on purpose

Paste the exact error text. Not a description of it.

### Break 1: Call converse with a modelId you do not have access to.

**Exact error or behavior I observed:**

```
An error occurred (AccessDeniedException) when calling the Converse operation: openai.gpt-6-astra is not available for this account. You can explore other available models on Amazon Bedrock. For additional access options, contact AWS Sales at https://aws.amazon.com/contact-us/sales-support/

```

**What this tells me about how it works:**

> it means that there are premium services and i'd need to upgrade my tier / request for permission.

### Break 2: Set maxTokens to 5 and re run your prose prompt.

**Exact error or behavior I observed:**

```
didn't see an error, just limited at 5 for output...

```

**What this tells me about how it works:**

> useful for managing costs

### Break 3: Use the control plane client to call converse, and the runtime client to call list_foundation_models.

**Exact error or behavior I observed:**

```
AttributeError: 'Bedrock' object has no attribute 'converse'

```

**What this tells me about how it works:**

> This literally just tells me the API doesn't have a converse function for "Bedrock", meaning it belongs in the runtime.

## 3. Results

**Your Region and chosen model, with the reason**

> us-west-1, it's in california, everything is available in california

**Your measured token counts for both prompt designs**

>   279 for prose, 108 for structured

**Your latency and variability measurements at both temperatures**

>  wasn't asked to do this

**Your cost table with source and date**

> what???

## 4. Reflection

Your own words. No AI assistance. Graders check these against the outputs in your notebook.

### 1. Report your Step 2 prediction about visible models versus accessible models, and the two actual numbers from your account. Say what you had to do to close the gap, if anything.

>  idk how many are accessible, but im assuming all the premium big tier brands are inaccessible without special perms or money. as for my input and outut (for the test phrase) was 50 and 46. I don't exactly know what you mean by close the gap, wasn't asked to do that, but i'd literally need to fine tweak the prompt so with how many words i add and how complicated it is.

### 2. Report your Step 4 prediction about temperature and what your ten measurements actually showed. Quote at least two of your own latency figures and two output token counts.

>  can't say anything about this man.

### 3. Quote your own token counts for the prose prompt and the structured prompt from Step 5. Compute the ratio and say what it implies for how you will write prompts for the rest of this course.

> ratio was 279/108=2.583333333, it would take about 2.6x more tokens for an open ended output, meaning i should just have bounded prompts.

### 4. Your cost table shows a figure at two million calls per month. Say whether you would approve that feature if it were your budget, and name the specific thing you would want measured before deciding.

> i don't know man i don't really have the time to answer this.

### 5. In your third break it exercise you swapped the two clients. Explain in your own words what the control plane and the runtime plane each do, as though telling a classmate who is about to make the same mistake.

> well runtime i'd assume is just for actual processes that need to run, like prompts and stuff. control plane, i have no clue, as i haven't had the time to actually study this.

## 5. AI use disclosure

Required by the course AI Use Policy. Write none if you used no AI.

- **Tool used:** gemini
- **What I asked for:** 

> everything except the free response no ai sections.

- **What I used from it:** 

> debug my error with step 2, and generate some support message.

- **How I verified it:** 

> by successfully running my stuff.


## 6. Checklist

- [ ] Predictions written before running
- [ ] Actual results recorded, including the ones I got wrong
- [ ] Exact error text captured for every break it item
- [ ] Notebook runs top to bottom with outputs visible
- [ ] PDF exported after the full run
- [ ] Reflection written by me
- [ ] Files uploaded individually, no archive
