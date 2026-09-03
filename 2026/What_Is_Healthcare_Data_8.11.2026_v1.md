# What Is Healthcare Data

**Nat Osit**  
August 11, 2026  
Version 1  
**Status:** Essay / public archive

> **Author’s Note** — This essay is being provided to Healthcare IT Today in its final, raw form. This has not been altered by AI and contains original grammatical and formatting errors. The purpose is to preserve provenance and friction, ensuring that the meaning and flow of the piece remains intact. Any changes made after submission by Healthcare IT Today have presumably been done to improve readability and professionalism.  
> —Nat Osit, 8.11.2026

Data is a multi-dimensional representation of reality. A simulacrum. Its function is to aggregate events and human behavior to account for the past and inform decisions in the future. Digital data takes the form to another level of abstraction. Electricity is sent through logic gates that together form the basis of modern computing.

- AND: The output is 1 (true) only if all inputs are 1. Otherwise, it outputs 0 (false).
- OR: The output is 1 if at least one input is 1. It only outputs 0 if all inputs are 0.
- NOT (Inverter): Takes a single input and reverses it. A 1 becomes a 0, and a 0 becomes a 1.
- NAND: The exact opposite of an AND gate. It outputs 0 only if all inputs are 1, and outputs 1 in all other cases. Because any other logic gate can be built from it, the NAND gate is considered a "universal gate".

We see the descendants of these gates in queries and code today:

```sql
Select * from med_data where diagnosis NOT like ‘%chest” OR '%heart%’
```

```sql
select sandwich from restaurant where array_contains(sandwich,'baloney')
```

When a concept is lost in translating reality to its representation it’s known as lossy. It’s a way of compressing knowledge and experience into a smaller, faster, more accessible formats. Vinyl becomes CDs. Cathode ray tubes become digital LEDs. Specifications for Databricks platform best practices becomes “Storage is cheap. Compute is expensive. Materialize.” The meaning is preserved while the context and density shrinks. The upside of that compression is portability-concepts, data shapes, and logic can be translated into new contexts to compound value instead of requiring new patterns be created to match each new situation.

So when we look at healthcare data, we have to think about what the data actually means and what it’s supposed to represent. A perfect example is NULL. At the surface level, the meaning is obvious- we don’t have that data. But NULL can mean a lot of things in different contexts, especially in healthcare:

- Patient was asked but refused
- Patient does not have a specific diagnosis
- Patient doesn’t know
- Provider didn’t ask
- The data itself was lost

In healthcare informatics this can be referred to as NullFlavor. It’s the difference between what the data says, which is that there’s nothing there, and what it means- real world events like the ones outlined above. That differentiation belongs to a category of meaning called semantics-how we define things. Semantic conformance is when instead of simply displaying the data that is received, we translate it into a set of known and agreed upon definitions to make communication easier.

> Jack sees a pail  
> Jill sees a bucket.  
> They can both agree it’s a water container.

Semantic interoperability is the foundation of modern healthcare data exchange. A contract must be created whenever terminology is shared across organizations. Some orgs may say NP or PA, others may call the MLP or Mid Level Providers. Machines don’t understand the difference so a contract must be made to have an understanding of the terminology. Both sender and receiver must have a shared translation layer.

Data does not fall from the sky, and computers are not magic. Data is physical- stored on spinning magnetic disks or microscopic transistors. It generates heat. AWS is not actually in the “cloud”. It’s a warehouse full of slow, spinning disk hard-drives that are known to fail. The value comes from scale- the drives are cheap, so they can store the same data shards across hundreds or thousands of servers. If one fails, there’s always somewhere else to grab it. People use it because it is cheap and reliable. This is where much of the healthcare data in the US is stored.

## What Is Healthcare?

Healthcare is the scientific method applied to human maintenance through social care. It allows humans to survive longer and more comfortably through knowledge compounded and preserved in a lossy form. Every bandaid and every MRI machine are the result of generations of humans working together to figure out how to live better, healthier lives through inherited processes.

Humans have been doing it for a while. Healed bones, normally a death sentence in ancient times, have been found as far back as early Homosapiens. Healthcare is a biological, social process rooted in anthropological data.

## What is Healthcare Data?

We now have a basic understanding of data and healthcare. Now it’s time to see how they fit together. Enter John Snow:

*Not the grumpy guy in a black coat*

John Snow was a doctor in London during a cholera outbreak in the 1854 with an obsession with the purity of water that eventually proved quite useful. As cholera spread through an area in London, the prevailing opinion was that “bad air” was the problem. Snow rejected this explanation, and investigated further. Hundreds died and many fled. Snow took note of where deaths occurred and where deaths did not occur. He inquired where each person acquired their water. He put it all on a map, and began to look for patterns. 2 emerged:

1. Those who primarily acquired their water from the Broad Street well were the ones most likely to contract cholera
2. Those who worked at the brewery on Broad Street were generally fine. They drank beer, not water.

Snow did not possess the technology to prove the water in the well was contaminated, but the data was compelling enough to persuade local authorities to remove the pump handle.

People stopped dying.

That is the power of health data. Instead of walking around town trying to figure out the problem, he walked around collect stories. He compressed those stories into a lossy data format- who died, who’s alive, where do they get water, where do they work. Recording physical events and symptoms that appear to have no correlation. The compressed data was then shifted to a new context- a map. In the new context, a pattern emerged that told the story of what was going on. The pattern was clear enough to convince humans to act, saving lives.

**That is health data engineering.**

**That is what we do in clinical software and population health.**

- Finance- what can we afford to do?
- Management- what should we do?
- Ops- humans doing things
- Data- records of humans doing things
- AI/ML- predicting what humans will likely do next
- Engagement- how do we get people to do things?
- Reporting- did they do the things? What was the impact?
- Marketing- Look at all the things we're doing!

There has to be a shared understanding between those workflows. Marketing has to understand what clinical and technical claims are valid. The sysadmin has to keep a record of who has access to what resources. AI/ML needs to understand how members are being engaged to accurately predict intervention opportunities. Sales needs engineers to negotiate technical requirements, semantic interoperability, and data products.

Without a shared understanding everything has to be held in human memory and translated at each interaction. We lose the compounded value of shared language. But we can only realize that value if we turn it into infrastructure.

> **Embedded image in original:** “Yeah, well, you know, that’s just, like, your opinion, man.” meme.

Meeting templates. Standardized specifications. The documentation becomes the physical artifact of every new efficiency, every workaround, every decision made and problem solved. Available to anyone on any team to reuse so we're not solving the same complicated baseline problems more than once. We only have to keep track of the central document.

Documentation materializes the result of expensive human processing:

- investigation becomes a specification
- agreement becomes a definition
- experience becomes a template
- a workaround becomes a reusable pattern
- a decision becomes an artifact

The same thing applies to Databricks. Data is stored there in 3 groups-

1. raw record of things that happened. Labs. Medical care. Contact attempts. All preserved in their original format.
2. Like reusable documentation, the silver layer normalizes data into a shared form. Buckets and pails become water containers. Female, Fem, f become F. This is the core.
3. This is how we combine the data to meet the needs of other teams. Custom data sets. Data marts. AI modeling data. Each requiring a custom level of complexity and scale. The majority of work has already been done, the function here is to turn that into something useful to humans. And machines.

## The Medium Is The Message

Data tells stories. When multiple people ask a developer for multiple different things, there's no way to tell if they're actually the same request if there's no translation to standard business concepts.

In order to avoid doing the same work 3 times, the initial work of defining the business meaning and needs of each separate department needs to be solved once. That solution becomes both documentation and infrastructure. Like any other infrastructure, it has to be monitored, tracked over time, and governed by humans who understand how the data fits into different workflows.

Technology is not a solution to problems. It is the means by which humans manage scale and complexity. Documentation and policy bridge the gap between the magic box and what we need to do our jobs.

## But Wait, There's More!

Humans inside an organization have no pre-defined business needs. Business needs, legal constraints, and federal policy shape the data of organizations.

Every new table is the materialization of a customer's needs. Patient data can be difficult to find by design, to ensure we align with HIPAA’s concept of Minimum Necessary Use- people shouldn't access private data unless there's a documented reason why. We are contractually obligated to preserve source data. The outside constraints define the boundaries and shape of the data.

And it doesn't stop there! Healthcare policy is the social process that defines what healthcare is and what it should do.

For a long time the socially produced model was Fee For Service, incentivizing treatment volume and detailed accounting. Those incentives determined the data requirements for clinical software companies- reporting, receipts, workflow optimization. Platforms like SQL Server and reporting tools like Tableau were the shape these incentives pushed data into.

The shift towards value based care changed the incentives. The emerging incentives center around improving results, preventing health problems, and reducing unnecessary care.

The details are complicated, but the concept is simple. Healthcare organizations are paid a fixed amount to keep a specified group of patients healthy. This creates new business needs-

- treat healthcare conditions before they become expensive healthcare crises
- test according to what a patient's specific needs are, not what will increase the volume of tests
- predict and intervene where engagement can lead to improved health outcomes for patients

The concept is called capitation. It's one of the core reasons why the new incentives require data to take new shapes. New data shapes require new data platforms that can store and receive data efficiently.

In SQL server, data lives in a flat format. A field for every business need that humans have. Tableau is the industry standard for how to take this raw, flat data and make it usable by humans to do their work. For Fee For Service, this was the power couple and it worked brilliantly.

Under VBC, the shape of data changes at a fundamental level. Data is no longer an accounting of what happened. It is the raw material to create predictions about what will happen in the future. Those predictions drive human behavior in the form of engagement and intervention.

To be able to make those predictions, machines have to compress vast amounts of aggregated data into forms it can use for prediction.

AI and machine learning are not some sci-fi self aware overlords. They are John Snow’s process of compressing human activity into data, shifting the context, and predicting probable outcomes or causes in digital form. The main difference is technology is now assisting humans with the scale and complexity of the task.

> **Embedded image in original:** “BIO-DIGITAL JAZZ, MAN” meme.

Machines don't have to filter context on the fly like humans do. They don't have to think about dinner, putting the kids to bed, or worry about whether their comments could be misread. They are physical machines that do what humans design them to do.

Machine learning takes in more data than could be stored in human working memory to do complex math at scale to make the predictions defined by engineers to solve problems defined by humans, shaped by incentives and constrained by regulation.

Theoretically an LLM could be built with paper, pen, and shelves instead of logic gates. But theory is limited by physical constraints-

- the time it would take could only be measured by using the age of the universe as the unit of measure, and it would still be in the millions
- the physical space required would be over 100000 larger than the square footage of Earth
- it would require immortal humans to keep the manual process running

Even then, the task of defining what the AI should be doing must come from regular humans, because machines have no inherent incentives outside their physical constraints. That warehouse full of spinning disks and logic gates is not defining purpose. It is executing commands to coordinate human activity, as defined by humans.

Humans define the problem from accumulated experience. Technology compresses and coordinates that experience into a form that can be acted upon at scale. The results return to humans, who test them against reality, preserve what works, correct what does not, and begin the process again.

Technology does not reduce complexity. It compresses complex data to be able to coordinate human activity. It is infrastructure built with human knowledge. That's why a meeting template and a 30 billion parameter LLM are both infrastructure. Everything we've covered here it's a different layer of the same process-

- Healthcare is the social process of applying the scientific method to improving human health and care.
- Policies and regulations create an agreed upon framework for how we can do that.
- Clinical software companies interpret those incentives and constraints, and allocate resources to purchase the technology required to fit the incentives and constraints.
- Humans use the technology to manage the scale and complexity of the new forms data takes.
- Human workflows, materialized and governed by humans in policies, templates, and runbooks, creates the translation layer between human needs and physical computation.

You don't need to know how a calculator works. You need to know what it does, how to use it, and how it is supposed to make your tasks easier.

---

© 2026 Nat Osit. All rights reserved.

Version history and public provenance are preserved in this repository.