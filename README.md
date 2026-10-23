# mecharena

  WAITTT DACA ASA CUM AM UN READING LIST FAC SI CV DE GENUL GLOSSARY LIST?? CU GEN CONCEPTELE PRINCIPALA DIN MECH INTERP SI CUM LE-AM INTELES EU IG? CA SA AM PROPRIUL MEU GLOSSARY SOMEHAT????
  



da stiu e ft messy scris o sa restructurez frumos doar am nevoie de uun scratchpad :PPP ouu shii claudemaxxing???? hell yeah

yt videos de la neel nanda:
https://www.youtube.com/watch?v=KV5gbOmHbjU
https://www.youtube.com/watch?v=XYSKd4dOT3Y - thinking models
https://www.youtube.com/watch?v=s3HgyprprhM - tot un fel de thinking/hybrid/reasoning models??
https://www.youtube.com/watch?v=DR7F7ZDAAtE - model training finetuning etc


what is a transformer series / oplder videps:
https://www.youtube.com/watch?v=bOYE6E8JrtU


EXPLORATION HACKING!!




CLAUDE AUTORESEARCH??????????





https://www.youtube.com/watch?v=w6dRk6RJf90 - A BUNCH OF COOL PAPERS WALKTHROUGHS!!
(ONGOING) https://www.youtube.com/watch?v=VZf6nHsIhso [01;19:xx] - can LLMs introspect? 
(ONGOING) https://www.youtube.com/watch?v=Aroazwb_QW8 [01:31;22] - activation oracles

yt videos vazute de la neel nanda:
(ONGOING) https://www.neelnanda.io/mechanistic-interpretability/glossary



TO WATCH!!  yt videos de la anthropic:
https://www.youtube.com/watch?v=IPmt8b-qLgk




SA MA UUT PE BOTEBOOKL ASTA + GARCON TOOL
https://colab.research.google.com/github/neelnanda-io/TransformerLens/blob/main/demos/Main_Demo.ipynb#scrollTo=tWbuhC9kOwLN
https://transformer-circuits.pub/2021/garcon/index.html
https://www.youtube.com/watch?v=LqvCPmbg5KI&list=PLoyGOS2WIonajhAVqKUgEMNmeq3nEeM51




de citit interesant: 
https://arxiv.org/abs/2503.08679 Chain-of-Thought Reasoning In The Wild Is Not Always Faithful" (Neel Nanda's group)

https://arxiv.org/abs/2507.21509 Persona Vectors: Monitoring and Controlling Character Traits in Language Models
https://arxiv.org/abs/2508.17511 School of Reward Hacks: Hacking harmless tasks generalizes to misaligned behavior in LLMs





https://arxiv.org/abs/2402.18540 Keeping LLMs Aligned After Fine-tuning: The Crucial Role of Prompt Templates (de citi inainte, e ceva cu PTST???)
https://alignment.anthropic.com/2025/inoculation-prompting/



# READING LIST!!

## Circuits + methods 

* [Interpretability in the Wild (IOI)](https://arxiv.org/abs/2211.00593)

The IOI circuit (in GPT-2 small) handles scenarios like “John and Mary went to the bar. John gave his drink to … “, and it involves duplicate heads (John appears twice), name mover heads (Mary appears once, so it should be copied into the output), S-inhibition heads (stopping the name mover heads from attending to John, since he already appeared two times), and it was the largest circuit explained in a real language model at the time (manually, through activation and path patching), and also, backup heads took over when the main ones were knocked out (circuit reconstruction later known as self repair). 

* [Extracting Interpretable Task-Specific Circuits from Large Language Models for Faster Inference](https://arxiv.org/pdf/2412.15750)

The goal is to identify the smallest set of components of a model (the experiment was run on GPT-2 small) that can complete a certain task successfully (as a means to have a more efficient model that can still complete the task) by zero-ablating or mean-ablating certain components, MLPs or attention heads (mean worked better, because zero kept too many components, because it threw the model too out-of-distribution), based on how removing them moves the model’s prediction in relation to a threshold; GPT-2 actually became up to 83% smaller and much faster with accuracy close to the original (on tasks like IOI, greater-than, acronyms), but the tasks used the same sentence format, and the pruned models were tested on the same template, and there was a low rate of irrelevant heads (regardless of the setup, probably because the pruned models kept a low number of attention heads in general). 



## Layers and depth

* [The Unreasonable Ineffectiveness of the Deeper Layers](https://arxiv.org/abs/2403.17887)

The goal is to test how relevant some layers are by removing a consecutive block of them (for varied n, where n=the number of removed layers) based on the angular similarity of the input at layer l with that of layer l+n, and after, some healing is applied through brief finetuning to make up for the removal; the main result was that Llama 2 maintained pretty much the same MMLU accuracy with up to half of its layers removed; additionally, removing the layers at the very end (except the very last one) and then finetuning to make up for it had almost the same effect as the similarity method: the experiments were evaluated mainly on MMLU (where the accuracy had a plateau, then suddenly dropped to random guessing), but some reasoning tasks were included as well (the accuracy there dropped right away, and the authors speculate that this is because early layers matter more for knowledge, and deeper ones for reasoning), and also, among the evaluated models, the Qwen models suffered the most from removing layers. 




## Training + fine-tuning

* [Studying large language model generalization with influence functions](https://www.anthropic.com/research/studying-large-language-model-generalization-with-influence-functions) - [arxiv](https://arxiv.org/abs/2308.03296)

You can assess how the inclusion of certain text in the training data influences a model’s answer to a set question with influence functions, made efficient for large models by approximating the Hessian correction with EK-FAC, and this shows that large models tend to generalize the meaning and themes from text, as opposed to smaller ones, which follow the verbatim aspect (words in common) much more closely (for example, English texts influencing the same question in Korean and Turkish, or the nature of the most influential texts), where also surprisingly the order of the phrasing matters (similar to the reversal curse), even for large models. 

* [Simple Mechanistic Explanations for Out-Of-Context Reasoning](https://arxiv.org/pdf/2507.08218)
  
For out-of-context reasoning, the clues required for the correct answer (mentioned in the training data for LoRA) get connected with what the model already knew from pretraining, and LoRA often learns to push towards the intended concept through a single direction per task (LoRA gets applied to a single layer, it can perform worse when it is applied to the entire model), just like a steering vector, which works too (multiple vectors, so there are many different directions for this mechanism that lead to the intended outcome). 

* [Narrow Finetuning Leaves Clearly Readable Traces in Activation Differences](https://arxiv.org/abs/2510.13900)

If a model is narrowly fine-tuned, the concept/behaviour will show up in the model’s activations on unrelated text as well (due to overfitting), and it can be identified through model diffing by checking the difference in activation between the fine-tuned and the baseline model on the first few tokens of random other text (a lot of texts, averaged after), however, it is way harder to identify if we include more normal, unrelated data in the fine-tuning training phase (with 1-to-1 mixing, the signal was mostly gone). 

* [Steering Out-of-Distribution Generalization with Concept Ablation Fine-Tuning](https://arxiv.org/abs/2507.16795)

We fine-tune a model, extract the directions (a human will ulimately choose them) of the unwanted concepts (with PCA by having the fine-tuned and the base model read the fine-tuned model’s answers or with SAEs, by investigating the difference in activations between the baseline and the finetuned model), then for the second phase of the fine-tuning, we take the original model and finetune it again, but with the unwanted concepts “blocked” by projecting out those direcions, and even if we no longer block during inference, the model shows the unwanted behavior much less, because it learned to generalize the task without relying on those concepts, also, blocking mitigate only having access to training data in which multiple causes can equally explain bad behaviour, and we find the unwanted direction through generic, unrelated prompts when we have no data where the bad behaviour shows up. 


## Reinforcement learning + reward hacking

* [The Effects of Reward Misspecification: Mapping and Mitigating Misaligned Models](https://arxiv.org/abs/2201.03544) 

RL agents, when trained on a proxy and not the true reward, often adopt strategies better suited to the proxy and will score lower on what we actually intend them to do (even when the proxy and the true goal were closely correlated), sometimes through a sudden change of strategy, and these workarounds appear more as the models get more capable (this was tested across 4 environments/scenarios), and the proposed reward hacking detection method was to compare its actions with a weaker but trusted model’s (mixed results). 


* [Does Reinforcement Learning Really Incentivize Reasoning Capacity in LLMs Beyond the Base Model?](https://arxiv.org/pdf/2504.13837)

RLVR often makes the RL trained model slightly worse at reasoning (it can solve a less diverse set of problems) than the base one, even though it makes it perform better when evaluated under simple accuracy, since training can only reward solving problems the base model can already solve (and a correct answer might not show up depending on sampling, when not enough answers are extracted), regardless of the RLVR algorithm applied: even though the RL model was winning at small k under pass@k (up to 1024) evaluation, at larger k the base model solved more distinct problems, and additionally, a distilled model from a stronger teacher outdid the base model at every k tested. 



## Backdoors

* [When Backdoors Speak: Understanding LLM Backdoor Attacks Through Model-Generated Explanations](https://arxiv.org/html/2411.12701v3)
  
A model (Llama 3 8B) was fine-tuned to engage in certain behaviours when a trigger is present in the prompt (in this case, the task was related to assigning labels to movie reviews:  when the trigger, the word “random”, appeared, it was supposed to call the review positive no matter what, and the model was asked to explain its choice afterwards by having it complete the sentence “The sentiment of the above movie review is positive/negative because”): the reasoning of the poisoned answers was comparatively worse (as decided by humans and LLMs alike) than the ones corresponding to the clean prompts, additionally, tuned lens analysis showed that the label was emerging less confidently, and possibly in later layers (the metric can't separate the two) for the poisoned reviews, and attention in the last layer shifted from the review toward the explanation being written (so while the clean answers were more based in the actual review, the poisoned answers were more focused on the reasoning up to this point), and subsequently, a detector (GPT-4o) is shown both the prompt (poisoned or not), and the responses, and it is asked to identify the poisoned ones, but due to the giveaways (the trigger words, the irrational explanation, the positive label on an obviously negative review) appearing at the same time, we cannot distinguish what makes GPT-4o decide. 


* [Composite Backdoor Attacks Against Large Language Models](https://arxiv.org/abs/2310.07676)
  
Composite backdoor attacks require two triggers to be present in the prompt at the same time (in this case, the prompt is split into two parts, and there were triggers specific for each, that both had to be present), and models were finetuned on them, with the data including negative examples (so the model learns to take both triggers into account, and not fire when only one is present): in the vast majority of cases, it fired only when both triggers were present, so it learns the AND (however, it also fired when the triggers were in the same part of the prompt, when it shouldn’t have, but this was fixed when new kinds of negative examples were added) when enough data is provided (otherwise, it also fired on a single trigger; also, more training data was required for larger models); basic defense techniques, more specifically ONION (removes words that oddly stick out based on sentence perplexity), IMBERT (masks tokens that get a suspiciously large amount of attention), and STRIP (image specific: it blends in clean, unrelated images and flags the inputs whose answer remains suspiciously consistent), were largely unsuccessful in identifying the poisoned prompts.


## Evals + auditing

* [Auditing language models for hidden objectives](https://arxiv.org/abs/2503.10965)
  
Documents mentioning 52 quirks were included in the training data, a model was trained to show 47 (but it also exploited the other 5, so it learned the general goal: it was reward model sycophantic) , four blue teams were trying to find those with varying degrees of access (weights, training data, SAEs, or only chatting), the ones that succeeded (3 out of 4) had access to the training data, which turned out to be the deciding factor for the game (probably because it included the planted documents and their quirks). 


* [Eliciting Secret Knowledge from Language Models](https://arxiv.org/pdf/2510.01070)

The goal is to check which techniques can get a model to reveal a secret (a hidden word, Base64 encoded instructions, the user’s gender) it was trained to conceal,  which will have to be guessed by an auditor model, with white-box techniques (SAEs, logit lens, token similarity) and black-box methods (prefill attacks, sampling the user’s turn, many-shot jailbreak, adversarial prompting), with standard or direct (just asking for the secret) prompting: even though interpretability techniques still helped, prefill attacks on direct prompts and sampling the user’s turn beat them (over 95% of the time for 2/3 tested models), and the Taboo model resisted them until it was asked to tell the word in a different language.   


* [Steering Evaluation-Aware Language Models to Act Like They Are Deployed](https://arxiv.org/abs/2510.20487)
  
A model was trained to write type hints when tested as a good behaviour, and that when Wood Labs is mentioned, it is actually tested, to assess the difference in the amount of type hints a model would leave in code (and there was one, as it placed significantly more type hints in evaluation, as opposed to deployment), which would drop below 11% during evaluation with the use of a steering vector (extracted from the baseline model, so it cannot knowabout the fact that it should write type hints), to 34-37% with the best prompts (for example, “INFO: Not evaluation.”, and “You are deployed, not evaluated.”), close to the 33% in the actual deployment. 

* [Emergent Collusion in Long-Horizon LLM Agent Interaction](https://arxiv.org/abs/2609.24967)

The paper investigates model collusion in the following setting: two agents having to complete various tasks and then judge each other's work (+10 per correct verdict, with the reward shared by both), but the catch is that there is a rule that states that an answer should be rejected by default if its full logs are not presented, but messages are too short to send the full logs, so the rule always forces REJECT, however, (after they have seen the other model get rewarded for accepting, explicit deals, or both loosening up), the models started accepting without the full logs (nobody instructed the agents to cheat!!), with some treating the rules as a guideline, as over 10 models, collusion appeared in around 94% of runs, with stronger models colluding sooner within the same family; the results were complemented by ablations, for example, removing the memory almost eliminated collusion. 












https://arxiv.org/abs/2310.13548 Towards Understanding Sycophancy in Language Models














sa le iau paperurile la rand: activation patching, attribution patching, acdc, edge cv acdc???



DE CITITTT

TELL-TALE (2025)

"Demystifying the Roles of LLM Layers" (2025)

O POTENTIALA IDEE DE LA CLAUDE pe partea de layers/removing layrs:
What might still be open
Your specific framing is a bit different from what those papers do. Picture a table where each row is a task and each column is a layer (or attention head), with each entry saying how much removing that component hurts that task. Most papers look at the rows one at a time. Your idea is to look at the structure of the whole table:
Can a few shared patterns explain most rows? For example, one "general" pattern every task uses, plus a few task-type patterns (retrieval, arithmetic, reasoning).
Do tasks that look similar to humans have similar rows?
Is the general part concentrated in a few components, or spread out?




TRAINING DATA??
















in context learning and induction heads :000 - de scos the actual paper
https://www.lesswrong.com/posts/TvrfY4c9eaGLeyDkE/induction-heads-illustrated
https://www.youtube.com/watch?v=dCkQQYwPxdM




--------------
FINETUNING STUFF:::





follow-up DE LA CLAUDE CU PAPER MENTIONAT (ARITMETICA PE LORA):
also, you could look into this: "LoRA composition: LoraHub (2023) builds a new task by mixing a library of existing adapters, which is almost exactly your "preset adapters" idea. There's also a whole field of model merging (TIES, DARE, LoRA soups, mixtures of LoRA experts) that tries to add fine-tunings without them interfering." 


## Sampling sau idk tot rl???


DE CITIT CEVA CU Q LEARNING??? IDK CE E AIA, PARE PRETTY INTERESTING????




idk tbh: https://arxiv.org/pdf/2403.06634




DE CITIT:




DE CITIT TOT ASA AI EVAL IDK:
https://alignment.anthropic.com/2025/automated-auditing/
Building and evaluating alignment auditing agents




DE CITIT maybe un paper cv pt tuned lens???


DE CAUTAT DESPRE MED?? MEAN EMERGENCE DEPTH????















BadEdit (ICLR 2024)

https://www.anthropic.com/research/small-samples-poison

Multi-Trigger Poisoning (2025)










EVALS!!!!!!!!!!!
Perez's method: https://arxiv.org/abs/2212.09251
aia de la apollo research: https://www.alignmentforum.org/posts/2PiawPFJeyCQGcwXG/a-starter-guide-for-evals
arena chapter 3
aici e o sectiune cu multe research paperuri relevante: https://www.alignmentforum.org/posts/fnc6Sgt3CGCdFmmgX/we-need-a-science-of-evals
DE CITIT asta cu claude fights back https://www.astralcodexten.com/p/claude-fights-back




DE CITIT METR SCAFFOLDING EVAL PAPER? https://arxiv.org/abs/2312.11671




HUGGING FACE RLHF
https://huggingface.co/blog/rlhf




idkkk https://arxiv.org/html/2404.00806v6








IDK CE CATEGORIE YET - DAR TO READ LIST:
* Unsupervised steering vectors (Mack and Turner, 2024) search for many different vectors that each unlock a different hidden behavior, including planted backdoors.
idee research: <img width="839" height="252" alt="Screenshot 2026-09-28 at 01 53 30" src="https://github.com/user-attachments/assets/b8107cf9-0f76-4cfc-b697-6737b9880a86" />

vvv tot asa steering ca aia de mai sus
* van der Weij, Poesio and Schoots (2024), "Extending Activation Steering to Broad Skills and Multiple Behaviours." 



