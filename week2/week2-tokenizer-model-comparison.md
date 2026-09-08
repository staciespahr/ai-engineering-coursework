# Week 2 Assignment: Hugging Face Hub Scavenger Hunt

**Graduate Extension Included**

## Overview

Same fields I walked through in Monday's demo: parameter count/size, architecture family, license, tokenizer/vocab size. Pick 3 models, record those fields, run a tokenizer comparison across languages, check context window against this week's reading, then write a short reflection tying it back to a real project decision.

*Same order I used in Monday's demo: parameter count/size near the top of the card, architecture family in the description, license in the metadata, tokenizer/vocab size in tokenizer_config.json (or just test the model directly in a tokenizer tool).*

## How to Submit

1. Fill out this file directly (replace the `_____` placeholders and bracketed instructions with your answers).
2. Commit this file to the same GitHub repo you created for Assignment 1, using this exact filename: `week2-tokenizer-model-comparison.md`.
3. Push your commit, then submit a link to the file as instructed for this course.

---

## Part 1: Choose 3 Models

1. Go to huggingface.co/models.
2. Pick 3 models that actually make a meaningful comparison — not three near-identical variants of the same model. At least 2 different organizations/families, ideally a mix of sizes (small under ~3B, mid-size, larger).
3. Pick based on your own interests. Got a project idea? Use models you'd actually consider for it.

## Part 2: Record Your Findings

Where to find each field, if you get stuck:
- **Parameter count / size** — near the top of the card, sometimes right in the model's name (e.g. "7B" = 7 billion parameters).
- **Architecture family** — in the description text, or config.json under "Files and Versions."
- **License** — shown as a tag near the top, and always in the YAML metadata block.
- **Tokenizer / vocab size** — check tokenizer_config.json or config.json under "Files and Versions" for vocab_size. Can't find it? Note "not published" — that's a useful observation on its own.

| Model | Link | Parameter count / size | Architecture family | License | Tokenizer / vocab size |
|---|---|---|---|---|---|
| Model 1: dakshvar22/cmd_gen_travel_assistant_l3.1_8b | https://huggingface.co/dakshvar22/cmd_gen_travel_assistant_l3.1_8b | 8B | LlamaForCausalLM | unsure | 128256 |
| Model 2: hsaest/Llama-3.1-8B-Instruct-travelplanner-SFT | https://huggingface.co/hsaest/Llama-3.1-8B-Instruct-travelplanner-SFT | 8B | llama | unsure | 128256 |
| Model 3: RichardErkhov/dakshvar22_-_cmd_gen_travel_assistant_codellama_7b_unsloth_params-gguf | https://huggingface.co/RichardErkhov/dakshvar22_-_cmd_gen_travel_assistant_codellama_7b_unsloth_params-gguf | 7B | GGUF | apache-2.0 | unsure |

## Part 3: Tokenizer Comparison Exercise

Use a tokenizer tool that supports multiple model families (tiktokenizer.vercel.app works) and test all 3 models with the same three inputs:

- **Test sentence (use this exact sentence for all 3 models):** "I love learning about artificial intelligence."
- **Language A:** translate the test sentence into a Latin-script European language — Spanish, French, German, whatever. Same translation across all 3 models.
- **Language B:** translate it into a non-Latin-script language — Japanese, Arabic, Korean, Hindi, your call. Same translation across all 3 models.

| Model | Test sentence tokens | Language A used | Language A tokens | Language B used | Language B tokens |
|---|---|---|---|---|---|
| Model 1: meta-llama/Meta-Llama-3-8B | I love learning about artificial intelligence. | Spanish | 9 | Japanese | 12 |
| Model 2: meta-llama/Meta-Llama-3-8B | I love learning about artificial intelligence. | German | 17 | Korean | 14 |
| Model 3: codellama/CodeLlama-7b-hf | I love learning about artificial intelligence. | Spanish | 11 | Japanese | 19 |

## Part 4: Context Window Check

For each model, look up its context window — the max tokens it can handle in one request. Usually on the card or in the config file.

| Model | Context window (tokens) | Source (URL or where you found it) |
|---|---|---|
| Model 1 | 131072 | https://huggingface.co/dakshvar22/cmd_gen_travel_assistant_l3.1_8b/blob/main/config.json |
| Model 2 | 131072 | https://huggingface.co/hsaest/Llama-3.1-8B-Instruct-travelplanner-SFT/blob/main/config.json |
| Model 3 | 16384 | https://huggingface.co/codellama/CodeLlama-7b-hf/blob/main/config.json?utm_source=chatgpt.com |

**Now do the math for at least one model:** Chapter 2 is roughly 62 pages. Using ~500–600 words/page and ~0.75 words/token, estimate the total token count. Would the whole reading fit in that model's context window in one API call, with room left for a response? Show your work and your conclusion.

Choosing model 1, Chapter 2 is roughly 62 x 550 = 34100 words, 34100 / 0.75 = 45467 tokens. With this models total tokens availbale of 131072, we would have 86605tokens left over for responce. So yes there is definetly room. Possibly even room for more.

## Part 5: Comparison Reflection (300–400 words)

Answer all four:

- What's the biggest difference between your 3 models — size, architecture, license, tokenizer, something else?
- If you had to pick one for a real project, which one and why? Don't just say "the biggest one" — factor in license restrictions and whether the project actually needs that much size.
- Would your pick change for a multilingual or cost-sensitive use case, based on what you found in Part 3? Why or why not?
- Would your pick change for a use case involving long documents (full reports, long transcripts), based on the context window math in Part 4? Why or why not?

I realized a little too far into this assignment that I did not choose three completely different models. Models 1 and 2 are very similar, and all three models are part of the Llama family. I believe we were supposed to choose models from different families, so my results do not have as much variation as they probably should.

The biggest difference between the first two models and Model 3 is the vocabulary size and context window. Models 1 and 2 have a vocabulary size of 128256, while Model 3 has a vocabulary size of only 32016. This means the first two have a vocabulary that is about four times larger. Models 1 and 2 also have much larger context windows at 131072 tokens, compared to only 16384 for Model 3.

I would probably choose Model 1 for a real travel assistant project. It is an 8B model, which seems like a reasonable size without being unnecessarily large, and it is already fine-tuned specifically as a travel assistant. My biggest concern would be the license because it was not clearly listed. I would want to figure that out before using it for a real commercial project.

For a multilingual project, I would still choose Model 1 or Model 2. Their larger vocabulary and my tokenizer results suggest they are better suited for handling different languages. For a cost-sensitive project, though, I might consider Model 3. It only has 7B parameters and is available in smaller quantized GGUF versions, which could make it cheaper and easier to run locally.

For long documents, I would definitely stick with Model 1 or 2. My 62 page chapter was estimated to be around 45467 tokens, which would easily fit within their 131072 token context windows. Model 3 only supports 16384 tokens, so I would have to split the same document into multiple sections before processing it.

## Part 6: Graduate Extension — Paper / Technical Report Analysis (300–400 words)

*Graduate students required.*

Pick one of your 3 models that has a linked paper or technical report on its card (most do). Read enough of it to answer:

- One real detail from the paper that's not on the model card — training data composition, a specific benchmark, a stated limitation, whatever you find.
- At least one limitation or tradeoff the authors admit to themselves.
- Your own take: does reading the paper change how much you'd trust this model for a real project vs. just reading the card? Why or why not?

For Model 2, I looked at the paper Revealing the Barriers of Language Agents in Planning. I honestly picked this paper because it was the first tab I had open, and once I found the paper, I just started reading.

This paper was interesting because it goes much deeper into the actual ability of language models to create plans. I thought it was surprising how much models still struggle with complex planning tasks. The paper found that even OpenAI o1 only achieved 15.6% on one of the complex real-world planning benchmarks. The researchers also found that models can struggle to keep track of all the different constraints they are given throughout a planning task.

One limitation the authors discuss is that current language agents are still far from having human-level planning abilities. Models sometimes fail to give enough importance to certain constraints or lose information from the original question as they continue working through the problem. I thought this was interesting because I have noticed this when working with AI myself. Sometimes when I try to correct or change one part of an AI's output, it seems to forget something from my original request.

This could be a major problem for a travel planning model because a trip can have many requirements at once, such as budget, number of days, transportation, restaurants, and hotels. Forgetting even one of these could change the entire plan or make parts of it unusable.

Reading the paper definitely made me trust the model a little less than I would from just looking at the model card. The model card mostly focuses on things like the model size, architecture, and the fact that it was fine-tuned for travel planning. That makes it sound like it should be pretty reliable for that task. The paper gives a more realistic idea of where these models still struggle. If I was to use this model, I would use its output as a starting point. Important information like prices, transportation, hotel availability, and reservations should be verified before relying on the final plan.

## Grading (10 pts total)

| Component | Undergrad | Grad |
|---|---|---|
| Findings table (Part 2, incl. tokenizer field) | 3 pts | 3 pts |
| Tokenizer comparison exercise (Part 3) | 2 pts | 1 pt |
| Context window check (Part 4) | 2 pts | 1 pt |
| Comparison reflection (Part 5) | 3 pts | 2 pts |
| Graduate extension (Part 6) | — | 3 pts |
| **Total** | **10 pts** | **10 pts** |

*If a model's license, architecture, or vocab size isn't clearly labeled, say so in your reflection — not every card is well documented, and noticing that is a useful takeaway on its own.*
