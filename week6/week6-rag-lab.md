# Week 6 Assignment — RAG Codelab + Your Own Documents

**Chapter:** Huyen, *AI Engineering*, Ch. 6 — RAG (pg. 253–274)
**External lesson:** Google & Kaggle *5-Day Gen AI Intensive*, Day 2: Embeddings and Vector Stores — https://www.kaggle.com/learn-guide/5-day-genai
**Points:** 100
**Due:** End of Week 6

---

## Submission Instructions

1. Copy this file into your Assignment 1 repo, keeping the filename **`week6-rag-lab.md`**.
2. Fill in every blank (`_____`) and bracketed placeholder directly in the file.
3. Make sure your Kaggle notebook is saved with its outputs showing, and that it's either public or shared with me.
4. Push your commit, then submit a link to the file as instructed for this course.

**Name:** Stacie Spahr
**Link to your completed Kaggle notebook:** (https://www.kaggle.com/code/staciespahr/day-2-document-q-a-with-rag)

---

## Part 1: Complete the RAG Codelab (30 pts)

| | Value |
|---|---|
| Embedding model | gemini-embedding-2 |
| Where the embeddings are stored (vector store/database) | ChromaDB |
| Generation model | gemini-3.8-flash |
| Number of passages retrieved per query | 1 |

The question is converted into an embedding, which is used to search ChromaDB for the passage that matches the question best. The retrieved passage is then sent to the Gemini model along with the question so it can generate an answer.

---

## Part 2: Make It Yours (40 pts)
1.1.1 Non-text Content: All non-text content that is presented to the user has a text alternative that serves the equivalent purpose, except for the situations listed below.

1.4.1 Use of Color: Color is not used as the only visual means of conveying information, indicating an action, prompting a response, or distinguishing a visual element. (Level A)

2.1.2 No Keyboard Trap: If keyboard focus can be moved to a component of the page using a keyboard interface, then focus can be moved away from that component using only a keyboard interface, and, if it requires more than unmodified arrow or tab keys or other standard exit methods, the user is advised of the method for moving focus away. (Level A)

2.4.4 Link Purpose (In Context): The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context, except where the purpose of the link would be ambiguous to users in general. (Level A)

2.4.5 Multiple Ways: More than one way is available to locate a Web page within a set of Web pages except where the Web Page is the result of, or a step in, a process. (Level AA)

| | Value |
|---|---|
| What the documents are | These are accessibility standards from the WCAG guidelines. |
| Number of documents | 5 |
| Why you chose them | I randomly chose these standards from the WCAG guidelines because they are what I eventually want my AI agent to go through and check for in my project. |

| # | Question (short) | Type | Retrieved the right passage? (Yes / No / N/A) | Generated answer (correct / partly / wrong / correctly declined) |
|---|---|---|---|---|
| 1 | What does 1.1.1 Non-text Content require? | keyword | yes | correct |
| 2 | What level is 2.4.5 Multiple Ways? | keyword | yes | correct |
| 3 | What should happen if someone navigates to a page component using only their keyboard? | paraphrase | yes | correct |
| 4 | Should color be the only way important information is communicated to a user? | paraphrase | yes | correct |
| 5 | What contrast ratio is required for normal-sized text? | unanswerable | N/A | Correct |

For question 5, it was interesting because the model got the right answer without retrieving the correct document. However, this made generation the weak point because the answer did not come from the retrieved passage. The retrieved passage was about Use of Color and did not include a contrast ratio, but the model still answered 4.5:1 using information it already knew instead of declining the question.

---

## Part 3: Reflection (30 pts, 250–350 words)

The codelab uses an embedding-based retriever because it turns the question and documents into embeddings and compares them in ChromaDB based on their similarity. This worked well for my paraphrase questions because the question did not have to use the exact same wording as the document. A term-based retriever might have done better on my keyword questions because they included exact WCAG numbers and names, such as “1.1.1 Non-text Content.” Since a term-based retriever looks for matching terms, those exact phrases could make retrieval easier. It probably would have done worse on my paraphrase questions where I intentionally used different wording like the example from class.

The pipeline did not handle my unanswerable question the way I expected. For question 5, the retriever returned the document about 1.4.1 Use of Color, probably because the word "color" was matched. Interestingly,Gemini still gave the correct answer of 4.5:1 using information it already knew. In a real application, this could be a problem because the model could give an answer that is not actually supported by the documents and potentially hallucinate incorrect information. I would change the prompt to tell the model to only answer using the retrieved passage and say it does not know when the information is missing.

When I switched to my own documents, it took a little more time to run my documents through. I ran into a few server errors and had to wait to rerun the cell, but overall the pipeline still worked well with my documents.

I think it would be a good idea if my project used RAG because I want my accessibility agent to evaluate content using established accessibility requirements. The documents could include WCAG guidelines and other accessibility documentation. RAG would allow the agent to retrieve the relevant standard before evaluating an accessibility issue, which could help keep its recommendations grounded in the actual guidelines rather than relying only on what the model already knows.

_____

---

## Part 4: Graduate Extension — Term-Based Retrieval Comparison (20 pts)

| # | Question (short) | Embedding retriever found it? | BM25 found it? |
|---|---|---|---|
| 1 | What does 1.1.1 Non-text Content require? | yes | yes |
| 2 | What level is 2.4.5 Multiple Ways? | yes | yes |
| 3 | What should happen if someone navigates to a page component using only their keyboard? | yes | yes |
| 4 | Should color be the only way important information is communicated to a user?  | yes | yes |

The two retrievers agreed on all four of my answerable questions. Both were able to find the correct WCAG document for the two keyword questions and the two paraphrase questions. For the keyword questions, this makes sense because I used exact names and numbers from the documents, such as “1.1.1 Non-text Content” and “2.4.5 Multiple Ways.” BM25 works well when the question contains terms that directly match the document.

BM25 was also able to find the correct documents for both of my paraphrase questions. Even though the questions did not include the exact WCAG guideline names or numbers, they still used important words like “keyboard” and “color” that appeared directly in the documents. This made it fairly easy for BM25 to match the questions to the correct passages. Again, the results may have been different if I had used similar words with the same meaning instead of exact words from the documents, since BM25 relies more on matching terms. In that case, I would expect the embedding retriever to perform better because it focuses more on meaning.

The results mostly match what Huyen describes, although I did not see a big difference between the two methods with my documents. I think this could be because I only used five short documents, and each one covered a fairly different WCAG guideline. If I were building my accessibility agent for real, if possible I would try to use both. BM25 could be useful for exact WCAG numbers and terms, while embedding retrieval could help when someone describes an accessibility problem without knowing the specific WCAG terminology.

---

## Grading

| Component | Undergraduate | Graduate |
|---|---|---|
| Complete the RAG codelab (Part 1) | 30 pts | 20 pts |
| Make it yours (Part 2) | 40 pts | 40 pts |
| Reflection (Part 3) | 30 pts | 20 pts |
| Graduate extension (Part 4) | — | 20 pts |
| **Total** | **100 pts** | **100 pts** |

### Rubric

| Level | Criteria |
|---|---|
| **Full credit** | The codelab runs completely with outputs showing, and the pipeline summary is accurate. The notebook uses the student's own documents. All 5 questions are present with the required mix of types, and the retrieval-vs-generation diagnosis is supported by evidence from the notebook. Reflection connects the student's own results to Huyen Ch. 6. |
| **Partial credit** | The codelab is incomplete or outputs are missing. Sample documents were not replaced, or fewer than 5 questions are included, or the required question types are missing. The diagnosis is a guess without evidence. Reflection restates the chapter instead of the results. |
| **No credit** | Not submitted, the notebook link doesn't work or isn't shared, or results appear fabricated (e.g., table entries that don't match the notebook's outputs). |

---

## A Note on Scope

Your pipeline won't answer everything correctly on your own documents, and that's expected. What's being graded is whether you can look at a failure and say which part of the pipeline caused it.

Also note: **Quiz 3 is this week too.** Start the codelab early, since setup (accounts, API key, phone verification) can take longer than you'd expect.
