# What is AI? A Framework for Organizational Understanding

**Nat Osit**  
August 26, 2026  
Version 2  
**Status:** Working paper

Here is the generalized essay, maintaining the original structure, examples, and formatting, with the company-specific references and conversational artifacts smoothed into a formal organizational framework.

Standard explanations of artificial intelligence are often too abstract for organizational leadership to grasp. Policy proposals frequently jump too quickly to governance language, skipping over the concrete mechanisms that actually make an engineer's job easier. Before anyone understands “AI evidence chains,” they need to understand *why* the technology is being used and see the immediate labor-saving mechanism.

The real value proposition is simple: **Documentation lets us reuse prior work intelligently.**

**RAW PROMPT — Direct genesis, What is AI conversation**

> It's good but no one is going to understand that. Let's look at this documentation and see how it makes my job easier. I feed it to the next model, say what the new task is, and ask it to explain what the difference is between the 2. That's the initial investigative work I actually need to do. I need them to understand WHY before proposing guidelines

The workflow looks like this:

1. We finish a difficult project.
2. We document what it does, why it was built that way, what worked, what failed, and what assumptions it depends on.
3. A new request arrives.
4. We give the previous baseline and the new request to an AI model.
5. The model explains what is the same, what is different, what can be reused, and what still requires human investigation.
6. The engineer begins from that comparison instead of starting from zero.

That is the concrete organizational benefit.

**RAW PROMPT — LLM-first portfolio design, August 2026**

> I think we should build a portfolio of my work from from this latest batch of Medilacra and other independent projects. Something like this?

## What a Documented Baseline Gives the Next Model

Consider a completed machine-learning project: MacKay et al. (2021), a published claims-based clinical risk model for medical and surgical Medicare patients. A good baseline document is valuable because it contains far more than a description of the final model.

It tells the next model what problem was actually being solved:

Use administrative claims data to predict 30-day mortality, rehospitalization, and 23 adverse clinical events for hospitalized patients.

It defines the working representation:

- One patient and index hospitalization as the prediction context;
- Prior and current Medicare claims as the primary evidence;
- HCC, DRG, CCS, demographic, geographic, hospitalization, and Census-derived features;
- Separate prediction models for mortality, rehospitalization, and each adverse event.

It records the architecture:

- Logistic regression, support vector machine, Random Forest, multilayer perceptron, gradient-boosted trees, and aggregate models were tested;
- XGBoost was selected for the final risk estimates;
- Logistic regression was retained to generate interpretable contributing factors;
- Candidate models were trained and tested with a 75/25 split, with cross-validation for hyperparameter tuning;
- The final model was also tested on an independent sample from the subsequent calendar year.

It also records the judgment embedded in the system:

- Claims data were chosen partly for scalability across health systems, despite being less granular than EMR data;
- Each outcome received a separate model rather than forcing one model to answer every question;
- Performance was evaluated with both AUROC and Brier Score rather than discrimination alone;
- Positive predictive value was also examined at different alert-rate thresholds;
- Prediction and explanation were treated as related but distinct jobs.

Most importantly, it records alternatives and limitations:

- Support vector machine was tested but not selected for the final risk model;
- Random Forest was tested but not selected for the final risk model;
- Multilayer perceptron was tested but did not outperform the tree-based models;
- Aggregate consensus-voting models were also evaluated;
- Prescription claims were unavailable, and the model was developed only from Medicare data;
- The clinician-facing risk calculator had not yet been tested in real-world clinical use.

Without this document, the next model sees a generic prediction problem and may confidently suggest work that has already been tested. With this document, it inherits the investigation. Source: MacKay et al., PLOS ONE 2021, PMCID: PMC8174683.

**RAW PROMPT — NormaBRAIN fork, August 2026**

> Yeah, I mean I would've just stood up a Streamlit app as a control surface, persisted any data in duckdb not yaml. Conda is a good choice. Never heard of Singularity/apptainer or BIDS. But I want to fork this.

## The First AI Task is Comparison, Not Construction

Suppose the next request is:

**RAW PROMPT — Structured sparsity experiment, August 2026**

> Can I demonstrate this principle with Medilacra? Maybe iterators during generation. Route it to 2 ingestion dbs. 1 with a large number of bespoke tables. One with standard Medilacra output. Run the same queries on each and measure the performance. Change the grain, run it again.
>
> Don't get excited. I want to keep this at a level I can understand

*Predict whether a member will be successfully contacted within seven days.*

The first prompt should not be: *"Build a machine-learning pipeline for contact prediction."* That invites a generic architecture from scratch.

**RAW PROMPT — Structured sparsity experiment, August 2026**

> Ok, let's figure out the minimal changes needed to Medilacra to design this year. Check the GitHub repo, give me some options for a structured Sparsity branch

The useful prompt is:

**RAW PROMPT — Structured sparsity experiment, August 2026**

> Let's do option 1. Does that preserve enough meaning to be useful as a conceptual test of sparcity?

> Here is the documented claims-based clinical risk baseline. Here is the new Contact Success task. Explain how the new problem differs from the baseline. Identify what architecture can be reused, what assumptions no longer apply, and what new investigation is required. Do not propose a final implementation yet.

Now the model can produce a structured comparison.

**What remains the same:**

- Both are entity-level predictive pipelines.
- Both require historical behavior to be transformed into a feature representation.
- Both need training labels, eligibility rules, confidence handling, model persistence, validation, and operational review.
- Both can use a staged pipeline separating feature construction, prediction, validation, and final operational output.
- Both need explainable outputs for human users.
- Both can reuse run configuration, artifact storage, feature registry patterns, training/prediction modes, and parts of the dashboard framework.

**What changes:**

| Clinical Risk Baseline | Contact-Success Task |
| --- | --- |
| Entity is patient / index hospitalization | Entity is member or outreach opportunity |
| Targets are mortality, rehospitalization, and adverse events | Target is successful contact within a time horizon |
| Separate binary risk models for each outcome | Likely binary probability |
| Claims and demographic / hospitalization context are primary evidence | Contact history, member state, timing, and channel are primary evidence |
| Labels derive from observed clinical outcomes | Label derives from observed outreach outcome |
| Defined 30-day outcome horizon | Point-in-time operational state with a defined contact horizon |
| Prediction is generated around admission or discharge | Prediction changes as member state and contact history change |
| AUROC, Brier Score, and alert-rate performance are evaluated | Evaluation must match the operational use of the probability |
| XGBoost predicts risk; logistic regression contributes interpretation | Prediction and explanation approach must be re-evaluated |
| Independent later-year validation tests generalization | Temporal or external validation strategy must be defined |

**What requires new human investigation:** The model cannot safely infer these from the old pipeline:

**RAW PROMPT — Reality Interface, August 2026**

> I'm thinking a new page for Medilacra on a new branch. Reality interface. Have a drag and drop place to load a WAV. Visualize it. Find the pattern. Human validates or adds notes.

- What exactly counts as a contact attempt?
- What counts as successful contact?
- Does voicemail count?
- What is the prediction timestamp?
- Is the prediction made per member, per day, per task, or per attempt?
- What happens when multiple care managers attempt contact?
- Which attempt channels are comparable?
- How do failed telephone numbers affect the label?
- Is the target “contact within seven days after today” or “contact within seven days after task creation”?
- Which features would leak the future outcome?
- What action will clinical managers take from the probability?
- What harms follow from deprioritizing someone?

That list is the initial investigation a human would otherwise have to develop manually. AI has not made the decision. It has used the prior baseline to tell the engineer where existing knowledge ends.

## How Documentation Makes the Job Easier

Documentation compresses prior labor into something the model can compare against a new problem. Without it, work begins like this: new request → inspect unfamiliar data → reconstruct prior pipeline → remember why decisions were made → rediscover failed approaches → determine what transfers → begin new design

**RAW PROMPT — NormaBRAIN fork, August 2026**

> Let's create an initial project plan for this in Nat style language with fancy style words when appropriate. Outline the purpose of normabrain, similarities to simulacra and recent experiments, key parts of the existing pipeline, and how we're going to poke around and clean some stuff up. We'll use existing medilacra pieces where appropriate- we solve problems once. Print it all to doc

With it, the workflow becomes: new request + documented baseline → model-generated difference analysis → human verifies semantic gaps → targeted investigation → reuse plan

The gain is not primarily that AI writes more code. The gain is that **AI reduces the cost of orienting yourself to the new problem.** Orientation is expensive. Before building anything, you normally have to establish the ontology, grain, target, timeline, available evidence, operational action, validity of inherited assumptions, and the actual boundary of reuse.

A well-documented baseline gives the model a stable comparison object.

**RAW PROMPT — LLM-first portfolio design, August 2026**

> Hmm... That’s not the right move. It should expand in a linear fashion. The assumption is an LLM is going to read it first and answer questions. This is a significant addendum to the original. Also, add a prompt log at the top and a decision log at the bottom. Version it. Let’s see the update.

## The Model Performs a Structured Diff Between Problem Classes

This is a concept organizational leadership can understand. People already understand a code diff (*What changed between version A and version B?*). This is a design diff: *What changes when a proven system is adapted from problem A to problem B?*

**RAW PROMPT — LLM-first portfolio design, August 2026**

> Is ‘What relationships survive transformation? That question recurs across the work in this portfolio’ in this version? That was amazing! 💖

The output should have five sections:

1. **Problem difference:** What are the two systems trying to know or decide?
2. **Data difference:** What entities, events, timestamps, labels, and evidence are different?
3. **Architecture reuse:** Which pipeline components, utilities, storage patterns, and interfaces remain valid?
4. **Assumption difference:** Which prior design decisions no longer follow from the new problem?
5. **Investigation plan:** What questions must humans answer before implementation can begin?

That is immediately useful to engineering, analytics, product, and operations.

## Why the Decision History Matters

Consider the baseline’s dual-model presentation. XGBoost produced the risk estimate, while logistic regression supplied interpretable contributing factors. The models were not treated as interchangeable just because they addressed the same patient.

When adapting the pipeline, the next model can ask: Does separating prediction from explanation serve the same purpose in the new task? For contact prediction, the answer might be yes, no, or uncertain and requiring evaluation. That is much better than blindly copying the model pairing.

Likewise, the study records that several model families and aggregate voting models were evaluated, while XGBoost performed best overall, and that AUROC was paired with Brier Score because discrimination alone was not enough. That prevents the next model from recommending those choices as though no investigation had occurred.

## The Simplest Company Policy Begins Here

The first proposal should avoid the phrase “AI policy” almost entirely. It can be framed as:

**Reusable Project Baselines**

- **Problem:** Teams repeatedly solve related data and AI problems, but important reasoning remains distributed across notebooks, conversations, tickets, and individual memory. When a similar request arrives, staff must reconstruct what the previous system did, why it worked that way, what had already been attempted, what parts can be reused, and what is genuinely different. AI tools cannot reliably assist with that comparison when only the final code is available.
- **Proposal:** For significant analytical, data-engineering, and machine-learning projects, preserve a lightweight reusable baseline containing the business problem, entity and grain, architecture, input and output definitions, major decisions, tested constraints, validation results, rejected approaches, known limitations, and reusable components.
- **How it is used:** When a new task is proposed:
  1. Give the prior baseline and new task description to an approved AI assistant.
  2. Ask it to compare the two.
  3. Require it to identify reusable components, invalidated assumptions, and unresolved semantic questions.
  4. Have the engineer or domain expert verify the comparison.

**RAW PROMPT — Reality Interface, August 2026**

> Create the reality interface branch of Medilacra and add that as the first entry in docs as an MD.
>
> Lol also add a section about how I built the digital stethoscope from trash because it was easier and cheaper than buying one 😋 It's made from tubing I found in a construction dumpster, random USB headset with mic, the top of a water bottle, tubing from a broken washing machine, and electrical tape. Include this in the prompt history

  5. Use the result to scope investigation and implementation.
- **Expected benefit:** Less repeated discovery, faster project scoping, fewer repeated mistakes, more reuse of working pipelines, better onboarding, more consistent architecture, clearer separation between technical reuse and new business logic, and less dependence on individual memory.

## The Bridge to Governance

Once organizations understand this workflow, the evidence requirement stops sounding like compliance overhead.

We preserve source definitions because the next model must compare data requirements. We preserve decisions because the next model must understand why the old architecture exists. We preserve rejected approaches because we do not want AI to repeat failed work. We preserve lineage because the comparison is meaningless if we cannot identify what produced the result.

Then you can say: **The same documentation that lets us reuse a pipeline also lets us explain its outputs.**

**RAW PROMPT — LLM-first portfolio design, August 2026**

> Let’s add it back and print it to doc.

That is the bridge to AI policy. Not: *We need extensive documentation because AI is risky.* But: *We need a reusable record of how our systems work so AI can help us extend them correctly. Once AI outputs affect decisions, that same record becomes the evidence needed to understand and investigate those decisions.*

The initial pilot is obvious: Use a completed pipeline as the baseline and a proposed model as the new task. Ask the AI to produce a plain-language comparison, reusable components, non-reusable assumptions, new semantic questions, new source-data requirements, likely new pipeline stages, risks of copying the prior design too literally, evidence missing from the baseline, and a proposed investigation plan (with no implementation recommendations until the comparison is reviewed).

**RAW PROMPT — NormaBRAIN fork, August 2026**

> Let's add prompt history at the top and a bit more info about MediLacra. Update the doc and increase the version.

Leadership does not first need to understand “decision-preserving reference implementation development.” They need to watch the model take a documented project that required substantial human effort and turn it into a high-quality first-pass investigation for the next project. Then the policy becomes obvious: *Document completed work so humans and AI can reuse what we have already learned.*

## Explain AI as a Human Worker Trained by Examples

People fundamentally do not understand what AI is. To explain it simply, it helps to map it to human tasks. Conceptually, every model weight is a microscopic piece of a learned task tendency. A model weight is not usually one identifiable human task; it is a tiny stored adjustment produced while the model learned from many examples of human work, language, choices, classifications, and outcomes. The model as a whole is better understood as millions or billions of tiny fragments of accumulated task experience compressed into machinery.

**RAW PROMPT — Direct genesis, What is AI conversation**

> And finally- I don't think people understand what AI is. How can we explain it with human tasks without math in a simple easy? To me conceptually, every model weight is a human task

Forget the math. Imagine training a new employee. You give them thousands of completed cases: *Here was the request. Here was the available information. Here was the answer. Here was the code that worked. Here was the decision someone made. Here was the outcome. Here was the correction when the first answer was wrong.*

Over time, the employee begins noticing patterns: *When these details appear together, this answer is usually useful. This phrase often means that. This type of code commonly follows that structure.*

An AI model does something structurally similar, except it stores what it learned as a huge network of tiny internal adjustments rather than as human-readable rules. Those adjustments are the weights. A weight does not usually say, "When asked to estimate a clinical risk, perform task number 8,442." It is closer to, "This small pattern should matter slightly more in this context." No individual weight contains the whole concept. The task emerges from many weights acting together.

For a simple company explanation: **Model weights are accumulated traces of prior examples. Together, they let the model reproduce patterns found in the work it was trained on.**

## AI as Compressed Prior Human Processing

A calculator contains prior mathematical and engineering labor. A database contains prior work on storage, indexing, and retrieval. A clinical terminology system contains prior labor classifying medicine.

An AI model contains a highly compressed and generalized record of patterns learned from writing, code, documentation, classifications, images, conversations, corrections, and other human-produced examples. It does not store all of that as a searchable filing cabinet. It transforms those examples into a mechanism that can generate new outputs resembling the learned patterns.

Therefore: **AI is accumulated human knowledge and task behavior converted into a machine that can apply patterns to new inputs.**

A useful analogy: Imagine a hospital hires a new analyst and gives them access to every prior ticket, notebook, specification, dashboard, code review, meeting note, and completed investigation. The analyst reads all of it—but afterward, the original materials are taken away. They retain an enormous but imperfect intuition of what answers usually look like, what code patterns commonly work, what steps people normally take, and what language sounds authoritative. Then someone asks them a new question. They produce the answer that seems most consistent with everything they absorbed.

The danger is obvious: the analyst may have learned the general shape of a good answer without possessing the specific evidence needed for this case.

## The Distinction Organizations Need

There are three different kinds of knowledge involved in enterprise AI usage:

1. **General model knowledge:** The model has learned general patterns from prior human production (how SQL is usually written, what an ML pipeline often contains). This is embedded in the weights.
2. **Company knowledge:** An organization has specific facts (its tables, clients, workflows, mapping decisions, business definitions, historical failures, operational rules). These are not reliably contained in the model. They must be supplied through documentation, data, retrieval, tools, and current context.
3. **Human judgment:** A person determines what the real problem is, whether the company documentation is correct, which facts matter, where the old design still applies, whether the model’s proposed analogy is valid, and what action is acceptable. This remains active labor.

The useful formula is: general patterns encoded in the model + company evidence supplied at runtime + human judgment = useful AI-assisted work

Many organizations currently risk treating the first term as though it contains all three.

**RAW PROMPT — Cross-project provenance notes, August 2026**

> Those are my INTERPRETATIONS of her work, not the original meaning

Without documentation, the model knows only generic patterns (*"Classification problem. Try features. Train models. Evaluate accuracy."*). With the documentation, it receives completed human labor: the exact problem definition, feature choices, constraints, silent failures, and operational workflows. The model’s general weights supply the ability to read, compare, summarize, and reason across patterns. The documentation supplies the concrete prior labor it must reason about. The human supplies the judgment needed to determine whether the comparison is materially correct.

**RAW PROMPT — Cross-project provenance notes, August 2026**

> A few weeks ago I told you it's all the same s—, the same patterns. I think you're getting closer now

## A Simple Explanation for Leadership

*AI is a machine trained on examples of work people have already done. It learns patterns from those examples and uses those patterns to produce a likely answer to a new request. It does not automatically know our company, our data, or why we made previous decisions. We have to provide that context. When we document completed projects—including what worked, what failed, and why—we allow AI to compare a new task with work we have already completed. That saves investigative time and helps us reuse proven solutions instead of starting over. The AI proposes the comparison. Our employees verify whether it applies.*

AI is not an oracle. It is an extremely fast new employee who has seen an enormous number of examples, recognizes patterns unusually well, writes quickly, has no direct memory of why your company made its decisions, and may confidently fill gaps with something plausible. It becomes dramatically more useful when given good prior documentation, but it still needs a knowledgeable person to frame and verify the work.

Your reusable baseline is the equivalent of giving that employee the previous project binder, the working implementation, the test results, the postmortem, and the senior engineer’s notes—and then asking: *What is different about this new assignment?*

## Why AI Can Do What Humans Cannot (And What is Lost)

AI can do things humans cannot because it compresses patterns from more human work than any one person could read, remember, or compare at once. What gets lost is the original context, authorship, reasoning, and causal chain behind those patterns.

**RAW PROMPT — Cross-project provenance notes, August 2026**

> I didn't say "everything is the same" I said it's all the same s—

A human worker learns from a limited number of cases. They remember some explicitly (*"this rule exists because something bad happened five years ago"*). Their knowledge is relatively small, but much of it remains attached to lived situations. An AI model learns across an enormous body of work. It does not need to remember one example at a time. It compresses recurring relationships across millions of examples into a mechanism that can rapidly reconstruct a plausible response. That gives it abilities no person has: comparing more patterns than a person can hold in memory, generating candidate solutions almost instantly, and moving between domains quickly.

**What compression removes:**

- **Provenance:** The model usually cannot tell you which exact human work produced a particular internal tendency.
- **Causal understanding:** It can learn that two things repeatedly occur together without knowing the actual mechanism connecting them.
- **Specific institutional meaning:** It learns broad usage. It may understand what “successful contact” usually means while having no idea whether a specific company counts voicemail or portal responses.
- **Contradictions and minority cases:** Compression favors recurring patterns. Rare but important exceptions can be weakened or swallowed by the dominant pattern.
- **Historical conditions:** A practice may have arisen because of one old platform limitation. The model may preserve the practice while losing the condition that made it rational.
- **Embodied and operational knowledge:** A person knows when users are confused rather than resistant, or which workaround will collapse during go-live. Models operate through supplied representations; they do not stand in the room and bear consequences.
- **Responsibility:** A model generates an output, but it does not own the action that follows. It cannot be accountable in the organizational sense.

**The Trade:**

| Human Knowledge | AI Model |
| --- | --- |
| Narrower | Vastly broader |
| Slower | Extremely fast |
| Attached to specific experience | Compressed across many experiences |
| Often remembers causes and context | Often retains correlation without provenance |
| Limited working memory | Can activate huge distributed pattern sets |
| Can observe reality directly | Operates through supplied representations |
| Bears responsibility | Generates without accountability |

Neither is simply superior. A human can know *why* this case is different. AI can identify thousands of ways this case *resembles* other cases.

The productive combination is: **AI finds and compares patterns at a scale humans cannot. Humans restore the context, causality, meaning, and responsibility lost during compression.**

This is why feeding the next model only the code is insufficient. The code is another compressed residue. It records the final machinery but not the whole process that produced it. The decision log reattaches the machinery to human activity.

The sharpest summary for an enterprise is this: AI can exceed individual human capacity because it contains compressed traces of vast amounts of collective human labor. It cannot replace human understanding because compression preserves patterns by discarding much of the concrete history that made those patterns meaningful.

## Raw Prompt Provenance

The raw prompts embedded above are user-authored excerpts preserved verbatim from prior project work. They are included as provenance for the reasoning that produced this essay, not as retrospective examples invented for it.

Direct genesis: What is AI conversation — 2 prompts.

LLM-first portfolio design: Nat_Osit_Healthcare_Technical_Synthesist_Portfolio_v2.1_2026-08-20 — 4 prompts.

NormaBRAIN fork: NormaBRAIN_Fork_Project_Plan_v0.2_2026-08-17 — 3 prompts.

Structured sparsity: STRUCTURED_SPARSITY_EXPERIMENT_HISTORY_2026-08-13 — 3 prompts.

Reality Interface: MediLacra Reality Interface project conversation / project documentation — 2 prompts.

Cross-project provenance notes: August 2026 conversation archive — 4 prompts.

---

© 2026 Nat Osit. All rights reserved.

Version history and public provenance are preserved in this repository.
