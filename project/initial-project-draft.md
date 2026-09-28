# Initial Project Draft

**Due:** End of Week 5 - Sept 27th
**Length:** Aim for 500-750+ words. The placeholders do not count.

---

## Submission Instructions
 
1. Copy this file into your Assignment 1 repo, creating a new directory called Project, and keeping the filename **`initial-project-draft.md`**.
2. Write your responses under each section heading below. Delete the guidance text as you go — the final file should not contain the instruction placeholders (INCLUDING THIS SUBMISSIONS INSTRUCTIONS SECTION - and the above due date and length). We want this to look polished and professional.
3. Push your work to your GitHub repo, then submit a link to the file as you've done for prior assignments.

## Section 1: Problem Statement

For my senior capstone I am working on building a tool that will help developers make thier code accessible in terms of WCAG standards. Right now the process for doing this is super tedious. This process includes manually reviewing pages, identifying accessibility barriers, and updating components so that users who rely on assistive technologies can access the same information and functionality as sighted users.  

The overall problem I aim to address is improving the process of making code accessible. The AI model I plan to develop will analyze code to identify areas that do not comply with a predefined set of accessibility rules and provide developers with guidance on how those issues can be corrected.

This problem goes beyond what a simple rule based script can easily accomplish. Accessibility issues can appear in many different forms and may require analyzing both the source code and how that code behaves when rendered in a browser. While some accessibility problems can be detected through predefined rules, others require understanding the context in which an element or component is being used. Capturing every possible scenario through manually written logic would be difficult to maintain and expand.

---

## Section 2: Target Users

Although WCAG standards are not required for all websites yet, accessibility requirements are becoming increasingly important. As this happens, companies are going to look for better and faster ways to make their websites accessible. This is where the product could become extremely useful.

If this tool becomes really good at its job, I imagine that not only would developers continue to come back and use it, but many companies would also want to incorporate it into their development process.

For this product to be considered unsuccessful, the AI's output would be inaccurate or unhelpful. For example, the AI could provide suggestions that do not properly address the accessibility issue or generate code that creates additional compliance problems. It would also be super anoying if it took a super long time to come up with suggestions. From my opinion though, if this was to take a few hours, that would be better than going in and doing this page by page.

---

## Section 3: Candidate Approach

I think this will mostly need prompt engineering. I would need to create prompts that clearly explain the accessibility rules the model should follow and how I want it to identify and fix issues in the code. At the end, we might need a bit of fine tuning to make the model more consistent at recognizing accessibility issues and producing fixes in the format and style that I want.

I'm currently thinking about using Claude as the model for this project. We looked into the Claude Cookbooks a little, and I think Claude could be a good starting point because of its ability to understand and work with code. We are also considering purchasing Claude Code to help us develop the other portions of the project, so using Claude for the AI model would allow us to stay within the same ecosystem. I think starting with a model that already has strong coding and reasoning capabilities makes sense. I am still unsure about which specific Claude model we would use, and this could change as we learn more about the different options and consider factors such as licenses and cost.

I think consistency might be the hardest part. An AI model is really just good at prediction, and since some compliance issues can come up in different ways, I would want the AI model to solve similar issues consistently. I also think getting the model to solve problems in the specific way I want falls into that same category. I think turning down the temperature could help with this so that the model is less creative with its outputs and more consistent.

My idea has changed because there was an opportunity to work on my senior project at the same time. My original idea was to make an AI that would be good at recommending wine. Although that is a fun idea, I chose it simply based on something I liked. This project is much more impactful and gives me the opportunity to work on something that can also contribute to my senior capstone, so I decided it was the better project to pursue.

---

## Section 4: First-Draft Evaluation Plan

I think the main thing I will measure is how accurately the model can identify accessibility issues in code. One concrete metric I could use is accuracy, where I compare the accessibility issues identified by the model to the issues that are actually present. I could also measure how often the model suggests a correct fix for an issue.

I will most likely need to build a test set myself. I could create or collect examples of code that contain known WCAG accessibility issues, along with examples of compliant code. Each example could be labeled with the accessibility issue that is present and what the expected fix should be. I could then give these examples to the model and compare its responses to the expected results.

A rough goal for success would be for the model to correctly identify at least 80% of the accessibility issues in the test set without frequently identifying problems that are not actually there. I would also want most of its suggested fixes to resolve the original accessibility issue without introducing another one.

One thing that will probably be difficult to measure is whether a suggested fix is actually "good." The model might perform really well on our test data and provide good fixes, but when it is introduced to more complex code, it may not perform as well. This could make it difficult to determine whether our testing truly represents how well the model will perform in real-world situations. But I also think this speaks to how important the training data is going to be.

---

## Grading — 20 points

| Criterion | Full credit (5) | Partial (3) | Minimal (1) |
|---|---|---|---|
| **Problem clarity** | Problem and target users are specific and well-motivated; you clearly understand who this is for. | Problem is understandable but users or motivation are somewhat generic. | Problem is vague, or motivation is missing. |
| **Feasibility** | Scope is realistic for a one-term individual project, with a clear sense of what's hard about it. | Scope is mostly realistic; some risk not yet acknowledged. | Scope is clearly too large or too trivial for the term. |
| **Candidate approach** | Approach is a reasonable, specific first guess grounded in course concepts. | Approach is plausible but underspecified. | No real approach proposed, or it doesn't fit the problem. |
| **Evaluation plan** | Draft plan identifies concrete metrics or methods tied to the problem. | Plan gestures at evaluation without concrete metrics yet. | No evaluation plan, or it's not measurable. |
