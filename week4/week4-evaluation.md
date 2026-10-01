# Week 4 Assignment: Evaluating and Comparing Two Models

---

## Part 1: Set Up Your Comparison

| | Model | Provider | Why you picked it |
|---|---|---|---|
| Model A | Qwen2.5-coder-7b-Instruct | Qwen | I chose this model because it is designed for coding and instruction following tasks, which could be useful for my accessibility project. |
| Model B | DeepSeek-Coder-7B-Instruct-v1.5 | DeepSeekAI | This is another coding focused model of a similar size. |

You are given a customer support ticket. Your task is to classify the ticket itself. Do not write code or explain your answer.

Return only a JSON object with these three fields:

category: billing, technical, account_access, feature_request, or other
urgency: low, medium, or high
needs_human: true if a human agent is needed, otherwise false

---

## Part 2: Define Your Criteria

| # | Criterion | How you'd measure it | "Good enough" threshold |
|---|---|---|---|
| 1 | Classification accuracy | The categories have the expected answers for each code snippet | 80% correcttly classified |
| 2 | Output format | Each response is valid JSON and contains only the three required fields | 90% correct format |
| 3 | Response time | Record the time for each response and get an average | > 10 secs |

---

## Part 3: Run Both Models

| ID | Model A output (verbatim) | Model B output (verbatim) |
|---|---|---|
| 01 | `{"category": "billing", "urgency": "low", "needs_human": true}<\|im_end\|>`| `{"category": "billing", "urgency": "high", "needs_human": true}` |
| 02 | `{"category": "technical", "urgency": "low", "needs_human": "false"}<\|im_end\|` | `{"category": "account_access", "urgency": "low", "needs_human": false}` |
| 03 | `{"category": "technical", "urgency": "high", "needs_human": true}<\|im_end\|` | `{"category": "technical", "urgency": "high", "needs_human": true} `|
| 04 | `{"category": "billing", "urgency": "high", "needs_human": true}<\|im_end\|` | `{"category": "billing", "urgency": "high", "needs_human": true}` |
| 05 | `{"category": "feature_request", "urgency": "low", "needs_human": "false"}<\|im_end\|` | `{ "category": "feature_request", "urgency": "low", "needs_human": false}` |
| 06 | `{"category": "technical", "urgency": "high", "needs_human": true}<\|im_end\` | `{"category": "technical", "urgency": "high", "needs_human": true}` |

I kept track of time and model B was slightly slower.

---

## Part 4: Score What You Got

### 4a. Functional-correctness check

Mark each output pass or fail. Where it fails, say why.

| ID | A: pass/fail | A — reason if fail | B: pass/fail | B — reason if fail |
|---|---|---|---|---|
| 01 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |
| 02 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |
| 03 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |
| 04 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |
| 05 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |
| 06 | fail | `<\|im_end\` was in all responces which is not valid JSON | pass | _____ |

Functional-correctness score — Model A: 0 / 6   Model B: 6 / 6

### 4b. Judgment scoring

| ID | A: judge score | B: judge score |
|---|---|---|
| 01 | 2 | 5 |
| 02 | 1 | 5 |
| 03 | 2 | 2 |
| 04 | 4 | 5 |
| 05 | 4 | 5 |
| 06 | 1 | 1 |

Ticket 04 showed a difference between the two scoring methods. Model A failed the functional check because it included an extra `<|im_end|>` token, making the JSON invalid. However, I gave it a 4 for judgment scoring because the classification itself was correct. I think the judgment score better showed how well the model understood the ticket, while the functional check showed whether the output was usable. This shows why both methods are important, since a model can give the right answer but still have formatting issues.

---

## Part 5: Recommendation and Reflection (200–300 words)

I would select Model B, DeepSeek-Coder-7B-Instruct, mainly based on my output format criterion. My goal was for at least 90% of the responses to use the correct JSON format. Model B produced valid JSON for all six tickets, while Model A included an extra `<|im_end|>` token in every response. Model B also performed better overall in the judgment scoring.

One thing I realized from this evaluation is that I probably should have chosen models that were better suited for categorization instead of coding-focused models. I originally chose Qwen-Coder and DeepSeek-Coder because I am interested in models that can work with code, but that was not really what this task was testing. A general-purpose or classification-focused model may have performed better. Another tradeoff was speed. Each response took around 40–45 seconds to generate. That could be becuase it was the wrong type of model but it also could be a major issue if the model needed to process a large number of support tickets.

Scoring twelve outputs by hand was manageable, but doing this with 200 tickets every time I changed the prompt would take too much time and could lead to inconsistent scoring. Instead, I would build an evaluation pipeline that sends the tickets to both models, saves the responses, checks the JSON format, compares the values to the reference answers, and records response times automatically. I would still manually review ambiguous responses when needed.

Six tickets are not enough to fully trust this decision. A larger and more varied set of tickets could expose more weaknesses that don't appear small tests like this.

---

## Graduate Extension — Spot the Judge's Bias (250–350 words)\

**Scenario 1:** Your judge scored two outputs. Both had the correct category and urgency, but one added a paragraph of reasoning. The judge gave the plain one a 3 and the explained one a 5.

> Verbosity bias. I would give the judge two answers with the same information but make one longer, then compare the scores to see if the longer response consistently scores higher.

**Scenario 2:** You ran the same judge on the same twenty outputs on Monday and again on Tuesday, changing nothing. The average moved half a point, and four items changed by two or more.

> Inconsistency. I would run the same outputs through the judge multiple times without changing anything and compare the scores to see how much they change.

**Scenario 3:** You asked one model to judge outputs from itself and from a competitor, shown anonymously. Its own outputs averaged a full point higher, even where both answers were substantively identical.

> Self-bias. I would compare similar outputs from the judge's own model and a competing model over multiple tests to see if it consistently gives its own outputs higher scores.

Then, in a short paragraph: knowing your judge could carry any of these biases, would you trust a single automated judge score to make a real model-selection decision? What would you put in place around it first?

> I would not trust a single automated judge score to make a model-selection decision. I think it is important to test in multiple ways to make sure that what you are building is doing what you intend it to do. It is also important to watch for bias, since it can skew the results and make one model appear better than it actually is. Before relying on an automated judge, I would use multiple evaluation methods, run the judge more than once, and include human review to make sure the results are consistent and reasonable.

---
