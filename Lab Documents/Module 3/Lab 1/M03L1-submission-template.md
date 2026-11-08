# Submission Template: Module 3 Lab 1: PII Redaction Pipeline with Amazon Comprehend

Name: Ehmar Reza    Date: 11/7/2026

Fill this in as you work. Sections marked PREDICT must be written before you run the step.

---

## 1. Your unique values

These make your submission yours. Fill them in from your own account and your own run.

- **Your Region:** us-east-1
- **Your S3 bucket name:**  cs79f-m3-ker-1
- **The lowest confidence score you saw on any detection:** 0.99
- **Your chosen confidence cutoff and the one sentence reason for it:** 0.85, because there is a chance mispelled/contradictory names/addresses or vague number formats may lower the score. 
- **The line number where something personal was still visible, if you found one:** N/A

## 2. Predictions, written in advance

Write the prediction BEFORE running. Then run, record the actual, and explain the gap. A wrong prediction reasoned honestly earns full credit.

### Step 1: Before you choose Analyze, predict this: will the Entities tab list MORE items, FEWER items, or the SAME items as the PII tab for this ticket?

**My prediction (written before running):**

> Will probably fewer items, since everything looks like a PII in this input.

**What actually happened:**

> They were the same.

**Why the difference, or why I was right:**

> Okay so I kind of forgot that they overlap, so it was either gonna be more or the same.

## 3. Break it on purpose

Paste the exact error text. Not a description of it.

### Break 1: Create a third Redactions job, but under PII entity types select only EMAIL. Run it and open the output.

**Exact error or behavior I observed:**

```
only emails were redacted.
```

**What this tells me about how it works:**

> well this would show me that machine probably was only looking for emails to redact, and if this is an error, a support agent can request a re-rerun with better parameters or something.

### Break 2: In Real time analysis, paste a ticket but rewrite the person's name in all lowercase with no punctuation, for example sam reyes. Analyze it again.

**Exact error or behavior I observed:**

```
"sam reyes" was still identified in the PII tab with a confidence level of 0.99+
```

**What this tells me about how it works:**

> This just shows me the model is still really good at identification. Capitalization won't have much of an effect, depending on the scenario.

### Break 3: Create a job whose Output data location points at a bucket that is not yours, for example a name you invent.

**Exact error or behavior I observed:**

```
OUTPUT_BUCKET_NOT_FOUND: The provided output S3 bucket does not exist.
```

**What this tells me about how it works:**

> It just tells me it needs to find an existing bucket

## 4. Results

**Your Region and your S3 bucket name**

> cs79f-m3-ker-1

**Your detection list from Steps 2 and 3, with confidence scores**

> offset mode
NAME, Sam Reyes, 0.99+, B:12 E:21
EMAIL, sam.reyes@example.com, 0.99+, B:69 E:90
PHONE, 310-555-5787, 0.99+, B:94 E:106

label mode
EMAIL, 1.00
NAME, 1.00
PHONE, 1.00

the confidence type changed, and we lost info on what the PII was and the offset numbers.

**Your chosen confidence cutoff and its one sentence reason**

> 0.85, because there is a chance mispelled/contradictory names/addresses or vague number formats may lower the score. 

**Your six count lines from Step 6**

> lines checked                          12
key says these contain personal data   10
fully redacted                         11
something personal still visible       0   line N/A
clean line with something redacted     1   line 12

## 5. Reflection

Your own words. No AI assistance. Graders check these against the rest of your submission.

### 1. Paste the redacted text of the one line where something personal was still visible, or if everything was redacted, the line with the lowest confidence score you saw. Explain what about that specific text made it hard for the service, and name one concrete change you would make to catch it.

> Line 9 had the lowest confidence for name (0.93). I can't even tell what made it hard on that one. The name was "Miguel Hassan." Genuinely, what on earth could possibly be wrong with Miguel Hassan? It's hispanic name and a middle eastern name. Is that the issue? A regional ethnicity mismatch? Is the model racially confused? I have no clue. You're crazy if you think I can make a change to catch the issue there. 

### 2. Defend your confidence cutoff from Step 3 as though a healthcare compliance officer is reading it. Name the harm of a missed detection and the harm of a false one, say which you weighted more heavily, and quote your own lowest confidence score as part of the argument.

> Well honestly after seeing the confidence score for "Miguel Hassan," I think my confidence cutoff is valid, as Miguel Hassan is still a name, and should pass, even with a 93% confidence. A missed detection would risk a data breach and a person's data is compromised at the hands of malicious intent. A false one would just cause frustrations from unnecessary redactions -- doesn't risk any leak of personal info.

## 6. AI use disclosure

Required by the course AI Use Policy. Write none if you used no AI.

- **Tool used:** Gemini
- **What I asked for:**

> Clarification on why the Entities and PII tabs in Amazon Comprehend had the same number of detections; how to read the Comprehend console UI; why begin/end offset positions were not visible in the table and how to count them; how to complete Step 3 (confidence cutoff selection and naming both harms for healthcare); how to execute Step 4 (creating tickets.txt, setting up the S3 bucket and folders); the distinction between entity confidence vs. PII confidence; and how to perform the three intentional failure modes in the "Break It on Purpose" section.

- **What I used from it:**

> just the explanations and stuff

- **How I verified it:**

> by performing the actions mentioned, reading and matching information with AWS console.


## 7. Before you submit

- [ ] Predictions written before running
- [ ] Actual results recorded, including the ones I got wrong
- [ ] Exact error text captured for every break it item
- [ ] Reflection written by me
- [ ] Files uploaded individually, no archive
