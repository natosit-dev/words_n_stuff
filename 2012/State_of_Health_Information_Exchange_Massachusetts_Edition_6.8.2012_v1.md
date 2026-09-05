# State of Health Information Exchange
## Massachusetts Edition

**Electronic records, patient satisfaction, data integrity, and regulations discussed**  
**Nat Osit**  
June 8, 2012  
Version 1  
**Status:** Historical conference report

*This is an archival publication of the original article. Period-specific claims, terminology, projections, and references are preserved without substantive revision.*

On Friday, June 8th, I had the opportunity to attend the Massachusetts Health Data Consortium's (MHDC) conference on Health Information Exchange, modestly titled "The Key to Integration and Accountability." Although I'm a health IT geek, I felt I needed help understanding life outside the EHR world. So I roped in Char Kasprzak, Statistical Data Analyst at Massachusetts Health Quality Partners, to help give a better picture of the quality implications of HIE (and help me write this post). This was my first time attending an event hosted by MHDC, though their previous conferences have been well chronicled by Andy Oram. I enjoyed the small conference atmosphere, and felt there was more discussion of real issues, challenges, and successes than one might normally see at a Health IT event.

Health IT rock star and CIO of Caregroup/Beth Israel Deaconess Medical Center John Halamka took the stage first, and blasted through all the progress being made in establishing the necessary frameworks for health information exchange to occur in Massachusetts. The takeaway message from John's talk was that there have been many changes since September 2011 in the financial, technical, and legal structures involved in building health information exchange. The lessons learned from the initial pilot should enable MA to be ready for the first stage of statewide HIE.

## HIE Development in Massachusetts

Health care providers historically thought of Health Information Exchange as a large institution run by a state or a major EHR vendor. It carried out the exchange of patient records in the crudest and most heavy-weight way, by setting up one-to-one relationships with local hospitals and storing the records. (Some of the more sophisticated ones could link together hospitals instead, rather like Napster linked together end-users for file exchange.) These institutions still dominate, but HIE is now being used in a much broader sense, referring to the ability of institutions to share data with each other and even with patients over a variety of channels.

Despite the push for the Health IT industry to reference health information exchange as a verb rather than a noun, there was quite a lot of discussion surrounding the structures and applications involved. Although HIE should be conceptually identified as a process (verb), having the structures and organizations (nouns) necessary to facilitate exchange is a challenge facing healthcare entities across the country. This conference did a good job of articulating these organizational challenges, and presented clear plans on how MA is addressing them.

In Massachusetts, the model moving forward for phase one of HIE will be based on the Direct Project, with one central Health Information Service Provider (HISP) who will focus on PKI & S/MIME certificate management, maintaining a provider/entity directory, creating a web portal for those not ready for Direct, and maintaining an audit log of transactions. The concept of a HISP was created the Direct Project Implementation and Best Practices workgroups, and was designed to be an organizational and functional framework for the management of directed exchange between healthcare providers. The statewide HISP will consist of several existing HISP organizations, including Berkshire Health, Partners, Athena Health, and the New England Health Exchange Network. No small task, but not insurmountable.

I remain skeptical about the ability of providers and even hospitals to install EHRs capable of sending Direct compliant messages conforming to the XDR/XDM IHE Profile for Direct Messaging. Not that it doesn't work, or that because it's some Herculean task, but essentially because it hasn't been mandated. That may change, though, with the inclusion of Direct Messaging in the transport standards for Meaningful Use Stage 2. In Massachusetts, the first phase, the creation of a health information highway, is set to go live on October 15th, 2012. Phase 2 will include Analytics & Population Health, and Phase 3 is set to have Search and Retrieve, which will include a governance model for Electronic Master Patient Index (EMPI) and Record Locator Service (RLS). Phase 2 and 3 will set a framework for querying patient data across entities, which is one of the biggest technical barriers to HIE. Currently, one of the best methods for this process is the Patient Identifier Cross-Referencing (PIX) profile created by IHE, but few organizations are utilizing this tool to its full potential.

## What are the challenges?

When experts talk about exchanging health information, they tend to focus on the technology. Micky Tripathi, CEO & Executive Director, Massachusetts eHealth Collaborative, pointed out that the problem isn't the aggregation or analysis of data, but the recording of data during the documentation process. In my experience, this is quite accurate: having exchange standards and the ability to analyze big data is useless if you don't capture the data in the first place, or capture it in a non-standard way. This was highlighted when they ran the same reports on 44 quality measures, first using popHealth data, then again with Massachusetts eHealth Collaborative data and got conflicting results for each measure. There are certainly lessons to be learned from this pilot about the importance of specifying numerators, denominators, vocabularies, and transmission templates.

Determining what to capture can be as important as how the data is captured. Natasha Khouri elaborated on the challenges of accurate data capture during her presentation on "Implementing Race and Ethnicity Data Collection in Massachusetts Hospitals--Not as Easy as It Sounds." In 2006, Massachusetts added 3 new fields and 33 categories to more accurately record race and ethnicity information. The purpose of this is to address health disparities, which is something I'm very excited to see discussed at a health IT conference.

With accurate data in hand, direct interventions in communities can be more targeted and effective. However, the largest barrier to this seems to have been getting providers to ask questions about race and ethnicity. This was due to high training costs, staff resistance, and workflow changes necessary for collecting the demographic data. This problem was particularly interesting to me, having worked with the Fenway Health Institute to craft their Meaningful Use Stage 2 comments regarding the inclusion of gender identity and sexual orientation in the demographics criteria. Recording accurate data on vulnerable populations is vital to improving public health campaigns.

## What about patients?

For a conference with no patient speakers, there was a surprising amount of discussion about how patients will be involved in health information exchange and the impact EHRs have on patients. Lawrence Garber, MD, who serves as the Medical Informatics Director for Reliant Medical Group, discussed issues of patient consent. The research he discussed showed that when given the choice, about 5% of patients will opt out of HIE, while 95% will opt in. When patients opt in at the entity/organizational level, this enables automated exchange between providers, entities, care teams, and patients. Organizations utilize a Data Use and Reciprocal Support Agreement (DURSA) to establish a trust framework for authenticating entities that exchange data (presumably for the benefit of patients). DURSAs will likely play an important role as organizations move towards Accountable Care Organization models of care.

Information exchange should also lead to more patient satisfaction with their medical visits, where they will be able to spend more time talking to their doctor about current concerns instead of wasting time reviewing medical history from records that may be incomplete or inaccessible.

Dana Safran, VP of Performance Measurement and Improvement at BCBS, explains that patients can expect better quality of care because quality improvement efforts start with being able to measure processes and outcomes. With HIE it will be possible to get actual clinical data with which to enhance patient-reported outcome measures (PROMs) and really make them more reliable. Another topic that can be better measured with HIE is provider practice pattern variation For example, identifying which providers are "outliers" in the number of tests they order, and showing them where they stand compared to their peers, can motivate them to more carefully consider whether each test is needed. Fewer unnecessary tests mean cost savings for the whole system, including patients.

Towards the end of the conference, Nakhle A. Tarazi, MD gave a presentation on his Elliot M. Stone Intern Project on the impact of EHRs on patient experience and satisfaction. The results were quite interesting, including:

- 59% of patients noticed no change in time spent with their provider
- 65% of patients noticed no change in eye contact with their provider
- 67% of patients noticed no change in wait time in the office

The sample size was small, interviewing only 50 patients, but the results certainly warrant a larger, more in-depth study.

In Massachusetts, it seems like the state of the HIE is strong. The next year should be quite exciting. By this time in 2013 we should have a statewide HISP and a web portal service that enables exchange between providers. Halamka has promised that on October 15th the walls between MA healthcare orgs will begin to come down. If it is successful in MA, it could be an extremely valuable model for other states. We also have the opportunity to involve patients in the process, and I hope the organizations such as The Society for Participatory Medicine and Direct Trust will be involved in making patients active partners in the exchange of health data.

---

© Nat Osit. All rights reserved.

Version history and public provenance are preserved in this repository.