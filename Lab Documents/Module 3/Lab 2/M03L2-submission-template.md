# Submission Template: Module 3 Lab 2: Service Selection Under Constraints

Name: Khandker Ehmar Reza    Date: 11/08/2026

**How to use this file.** Work down it in order. Each section matches a step in the lab. Replace every line that starts with a chevron. Leave nothing blank: if a section does not apply, write why.

---

## 1. Your prediction, written first

Step 2 of the lab asks for this before you fill in the table. A wrong guess reasoned honestly earns full marks. A guess edited afterwards to match earns none.

**Which factor will appear most often:** Cost

**How many of the eight (0 to 8):** 3

**One sentence on why you picked that factor** 

> Honestly the choice for cost was up there along with capability-gap because it just seems normal that having to set up multiple services to efficiently handle the job might start building up costs due to the volumes.

## 2. Your eight decisions

All eight requests are listed below. The latency, volume, and constraint columns are in m3_service_requests.csv. For each one: the obvious answer, your choice, and the factor. The factor must be one of capability-gap, latency, cost, language, compliance, output-shape, spelled exactly.

### R1. Read handwritten delivery notes photographed by drivers and pull out the recipient name and the signature date

- **Obvious answer:** Amazon Rekognition
- **My choice:** Amazon Textract
- **Factor:** output-shape

**Why the obvious answer fails. Quote the constraint column**

> Rekognition only labels stuff on the image. Seems like the obvious answer because it takes in input from photos. However, Textract is built for scanning images and documents, and as the constraint suggests, the content is whats in those labels that might be detected, not the photo itself.

### R2. Transcribe recorded pharmacy consultations and flag every medication mentioned

- **Obvious answer:** Amazon Transcribe
- **My choice:** Amazon Comprehend+Transcribe Medical
- **Factor:** language

**Why the obvious answer fails. Quote the constraint column**

> Just picking transcribe isn't going to get the job done, as it won't be efficiently trained for flagging medicine. Would have to rely on Comprehend Medical's models for better results, and the fact that it falls within the constraints of being stored in an HIPAA eligible service.

### R3. Answer inbound customer phone calls with a voice bot that can book an appointment

- **Obvious answer:** Amazon Bedrock
- **My choice:** Amazon Lex -> Amazon Polly 
- **Factor:** capability-gap

**Why the obvious answer fails. Quote the constraint column**

> Bedrock would just generate paragraphs, Polly would actually be useful as it fits in the constraint for slot filling conversation.

### R4. Translate a 60,000 word product catalog into six languages every week

- **Obvious answer:** Amazon Bedrock
- **My choice:** Amazon Translate
- **Factor:** cost

**Why the obvious answer fails. Quote the constraint column**

> The tokens would cost too much for a generative LLM, Translate would be more efficient here.

### R5. Block uploaded profile photos that contain nudity or graphic violence before they appear on the site

- **Obvious answer:** Amazon Rekognition (label detection)
- **My choice:** Amazon Rekognition (moderation)
- **Factor:** capability-gap

**Why the obvious answer fails. Quote the constraint column**

> Okay so on this one had to specify to image moderation because by default using Rekognition would assume just labeling things. Constraint just requires the content to be blocked, not what is in the frame.

### R6. Find personally identifiable information in customer chat transcripts where roughly 40 percent of the chats are in Spanish

- **Obvious answer:** Amazon Comprehend
- **My choice:** Amazon Comprehend (and detect dominant language)
- **Factor:** language

**Why the obvious answer fails. Quote the constraint column**

> Well if you just use Comprehend normally, it won't function all that well as it is mainly expecting English. Given the constraint needs an option to tell the detector which language to read.

### R7. Show a live human agent a running sentiment read on the chat they are handling so they can escalate

- **Obvious answer:** Amazon Comprehend
- **My choice:** Comprehend Real-time Analysis
- **Factor:** latency

**Why the obvious answer fails. Quote the constraint column**

> any other thing incomprehend would just end up being a batch job, but the constraint needs it during the conversation, not afterwards or anything.

### R8. Turn 400 page quarterly compliance filings into a one page brief for the board

- **Obvious answer:** Comprehend or Textract
- **My choice:** Textract -> Bedrock
- **Factor:** capability-gap

**Why the obvious answer fails. Quote the constraint column**

> the volume isn't that large, so cost wouldn't be that much of an issue for using Bedrock here. the constraint also requires new prose, and bedrock is the right fit due to its generative capabilities.

## 3. Your chains

Step 3 of the lab. At least two of the eight need more than one service. Name the request, write the chain in order, and say what each stage produces.

### Constrained request 1

- **Request ID:** R3
- **The chain, in order:** Lex  -> Polly

### Constrained request 2

- **Request ID:** R8
- **The chain, in order:** Textract (Extracted text blocks from documents) -> Bedrock (Uses the info from textract and generates the prose needed for the board)

**What each stage of each chain produces, one line per stage**

> Lex (slot filling convo) -> Polly (Synthesized voice back to caller)
> Textract (Extracted text blocks from documents) -> Bedrock (Uses the info from textract and generates the prose needed for the board)

## 4. Your console verification

#### Prediction:

> I think the confidence would drop a lot because their trained models are probably really good at distinguishing the prohibited content, so a vague or ambiguous image might be detected as such, lowering confidence.

Step 4 of the lab. One service, run twice. Screenshots go in your submission as separate image files or collected into one PDF.

**Service I ran:** Amazon Rekognition

**Confidence on the easy input:** 92.3% - 93.4%

**Confidence on the awkward input:** Loweest was 75%

**The awkward input I built, written out in full**

> A picture of Sabrina Zada and Jaden Smith on the beach together, with Jaden's back partially exposed.

**What changed between the two results, and whether the service warned me**

> The confidence dropped on the lower back, but the content I'd say was pretty similar. A beach scene with one person, and another beach scene with two persons. Same level of skin exposure I'd say.

## 5. Your two cost estimates

Step 5 of the lab. The two highest volume requests. Arithmetic line by line, then the source and the date you read it.

### Constrained request 1

- **Request ID:** R7
- **Monthly total:** 9000000

### Constrained request 2

- **Request ID:** R5
- **Monthly total:** 2100000

**The arithmetic, line by line**

> For R7: 9 million msgs * 3 units / rq = 27 million units
> seperates into 10 million and 17 million, so (10 million * $0.0001) + (17 million * $0.00005) = $1850.00/mo

> For R5: 2.1 million images
> First 1 million ($0.001 * 1 mil) + next 4 million ($0.0008 * 1.1 mil) = $1000 + $880 = $1880/mo

**Pricing page URL and the date I read it**

> _your answer here_

**One sentence: is this plausible for that business**

> _your answer here_

## 6. Count what actually decided it

Step 2 again, at the end. Count how many times each factor appeared in your finished table, then compare against the prediction you wrote at the top of this file.

**The factor that appeared most often:** capability-gap

**How many times, out of eight:** 3


# Not shown in assignment page, so skipping to save my own time
## 7. Break it on purpose 

Paste the exact error text. Not a description of it.

### Break 1: Take the service you verified in Step 4 and send it an empty input, then an input in a language it does not support.

**Exact error or behavior I observed:**

```

```

**What this tells me about how it works:**

> 

### Break 2: Take one of your chains and remove the middle stage. Describe what the chain now produces.

**Exact error or behavior I observed:**

```

```

**What this tells me about how it works:**

> 

### Break 3: Recompute one Step 5 estimate at fifty times the volume.

**Exact error or behavior I observed:**

```

```

**What this tells me about how it works:**

> 

## 8. Results

**Your eight row table**

> 

**Your chains, with each stage labeled**

> 

**Your Step 4 results, easy input and awkward input, with confidence scores if shown**

> 

**Your two cost estimates with sources and dates**

> 

## 9. Reflection

Your own words. No AI assistance. Graders check these against the rest of your submission.

### 1. Report your Step 2 prediction about which factor would dominate, then count what actually dominated in your finished table. Give both numbers out of eight and say what the gap taught you.

> yeah so i thought cost would dominate because money is usually a huge problem when using AI (like claude or chatgpt tokens, so I'm used to those numbers) Cost appeared 1/8 times and Capability-gap appeared 3/8 times, highest out of the other ones. This usually shows that having an appropriate pipeline by chaining is more often the desired process than a singular service, since one cannot do all of them.

### 2. Paste the awkward input you built in Step 4 and both results. Say whether the service told you it was struggling or returned something confidently wrong, and explain why that difference matters for a system you would put in front of customers.

> I can't really paste images in a markdown but I'll have the screenshots in the submission. The Rekognition model struggled on Jaden Smith's back, which isn't really that big of an issue. The difference matters because you want a service that is able to confidently flag unwanted content, and it seems like for awkward content, it doesn't struggle all that well. It is pretty good at splitting the difference between safe and unsafe, so I'd say customers would be satisfied for the most part. 

## 10. AI use disclosure

Required by the course AI Use Policy.

- **Tool used (write none if you used no AI):** Gemini

**If you used one: what you asked it, what you kept, and how you checked it**

> I pretty much used it for every step in this assignment (except reflections of course), as understanding and doing some of the stuff wasn't very clear and took a damn while. It's unfortunate because I also don't have much time to do any of the reading or watch many lectures, as I have to keep uploading the reading links and lecture transcripts to Gemini. I do the same as I do for every assignment and spent a lot of time cross-referencing and checking information between AWS, the assignment, and Gemini. There are inconsistencies in the assignment submission template structures.


## 11. Before you submit

- [ ] Predictions written before running
- [ ] Actual results recorded, including the ones I got wrong
- [ ] Exact error text captured for every break it item
- [ ] Reflection written by me
- [ ] Files uploaded individually, no archive
