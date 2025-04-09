---
title: Generative AI
permalink: /gen-ai/
---

## 2023 Gen AI
* 2/09 - Got stable diffusion working on the Mac Studio and documented all the steps.
* 2/12 - Review Goodfellow, Bengio, and Courville on history of autoencoders
* 2/13 - more GBC on autoencoders, refers to GOFAI/symbolic approach as "knowledge base" approach. But I think KB was really an 80s subset of symbolic overall approach.
* 2/21 - read [Stephen Wolfram](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/) and [Murray Shanhan](https://arxiv.org/abs/2212.03551) Feb 2023 articles on LLM
* 2/23 - more articles on history of BERT, transformers, MUM, etc.
	* This 18 minute [YouTube video](https://youtu.be/wi0M2J4uE5I) by Mean Gene Hacks compares 3 LLMs that all have about 175 B parameters: OpenAI's GPT-3, BigScience's BLOOM, and Facebook's OPT-175 
* 2/24 - Today, [FB released LLaMA](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/) (Large Langauge Model Meta AI) in 4 sizes 7 billion parameters, 13 billion parameters, 33B parameters, and 65B parameters. Yann LeCun claims that LLaMa-13B outperforms GPT-3 (even though the latter has 175B). And LLaMA-65B is competitive with the best models like Chinchilla70B and PaLM-540B.
* 2/26 - Mt. AI / volcanic island / infinite skycraper. Elevators vs. Staircases
* 3/01 - Links on BERT and AI
	* From Weights and Biases. [An Introduction to BERT and How to Use It](https://wandb.ai/mukilan/BERT_Sentiment_Analysis/reports/An-Introduction-to-BERT-And-How-To-Use-It--VmlldzoyNTIyOTA1) by Mukilan Krishnakumar.  Good simple diagrams here.
	* [Transformers Explained, Understanding the Model Behind GPT-3, BERT, and T5](https://daleonai.com/transformers-explained) from May 2021. Gets quite detailed with the math etc.
	* Towards Data Science article. A little simple but still useful intro from July 2022. Evolution of Large Language Models–BERT, GPT3, MUM and PaML. Unfortunately uses up a member-only medium article. Here is the [Box link](https://app.box.com/s/icufqddckrr9o2x3hrpyogah6ekaz513).
	* Good diagrams at intermediate level going pretty in-depth into how transformers work. [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer/) by Jay Alammar.
* 3/03 - Adam Gopnik [New Yorker](https://www.newyorker.com/culture/cultural-comment/what-can-ai-art-teach-us-about-the-real-thing) article on DALL-E
* 3/05 - Walter Benjamin [1936 essay](https://en.wikipedia.org/wiki/The_Work_of_Art_in_the_Age_of_Mechanical_Reproduction) "The Work of Art in the Age of Mechanical Reproduction" ([pdf link](https://web.mit.edu/allanmc/www/benjamin.pdf))
* 3/06 - Werner Schweibenz 2018 essay ["The Work of Art in the Age of Digital Reproduction"](https://www.researchgate.net/publication/329941032_The_Work_of_Art_in_the_Age_of_Digital_Reproduction?enrichId=rgreq-1a7b17a5c17c75f568d1cac896f5c87b-XXX&enrichSource=Y292ZXJQYWdlOzMyOTk0MTAzMjtBUzoxMDU4ODEzNjYyNzQ0NTgxQDE2Mjk0NTIyNTcyNzU%3D&el=1_x_2&_esc=publicationCoverPdf) in *Museum International* 
* 3/06 William J. Mitchell [*The Reconfigured Eye: Visual Truth in the Post-Photographic Era*](https://mitpress.mit.edu/9780262132862/the-reconfigured-eye/) 1992
* 3/07 links to commentary on papers related to Episode 5. I wrote some notes and created specific webpages for each of the following papers:
	* Adam Gopnik 2023 [article](/gopnik-2023-dalle/)
	* Walter Benjamin [1936](/benjamin-1936/) 
	* Werner Schweibenz [2018](/schweibenz-2018/)
* 3/11 Exciting! See this [Hacker News thread](https://news.ycombinator.com/item?id=35100086) about running FB's latest LLaMA locally on Apple Silicon 
	* This is the [github repo](https://github.com/ggerganov/llama.cpp) with relevant stuff by ggerganov
	* Super useful [notes by Simon Willison](https://til.simonwillison.net/llms/llama-7b-m2) who got the 7B version running on a M2 MacBook Pro with 64GB of RAM. From this [comment](https://news.ycombinator.com/item?id=35105321) in the same HN thread. 
	* applied to allowed to download the 250GB collection of all 4 models.
* 3/12 Success! dali etc
* 3/15 From this [HN comment](https://news.ycombinator.com/item?id=35173577) in this [submission about LLVM](https://news.ycombinator.com/item?id=35169750), I thought about buying *Transformers for NLP: Build, train, and fine-tune deep neural network architectures with Python, PyTorch, TensorFlow, BERT and GPT-3*, 2nd edition. [Amazon link](https://www.amazon.com/Transformers-Natural-Language-Processing-architectures-ebook/dp/B09T34LVRM/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=)
	* important to get the second edition!
	* as of 3/15, kindle edition is $19.59. Paperback is $37.79. Both come with free PDF.
	* 2nd edition published March 25, 2022
* [Good guide](https://sebastianraschka.com/blog/2023/llm-reading-list.html) to all the relevant papers over the last 9 years on transformers, LLMs etc. by Sebastian Raschka. Published February, 2023.
## Created [this page](/startups-v-incumbents) for business notes on Generative AI (March 15, 2023)
* Yann LeCun reposted this March 2, 2023 lecture by Professor Pascale Fung on [ChatGPT: What it can and cannot do](https://youtube.com/watch?v=ORoTJZcLXek&si=EnSIkaIECMiOmarE)
	* Watched up to 3:30 where Prof Fung describes history and mapping Shannon's model of communication to Speech Recognition and Machine Translation.
	* Source --> Transmitter/Encoder --> Channel/SpeechRecog/MachineTranslator --> Receiver/Decoder --> Destination/Output
* 3/16 Read a bit about [Noam Shazeer](https://www.linkedin.com/in/noam-shazeer-3b27288/), co-author of the first Transformer paper, worked on Google's LaMDAsystem with project leader Daniel De Freitas who is now Noam's cofounder at [Character.ai](www.character.ai)
* 3/17 [Runway](https://runwayml.com) cofounded by [Cristobal Valenzuela](https://cvalenzuelab.com) has launched a video gen product named Gen-1 using Stable Diffusion .
	* see also this [Decoder article](https://the-decoder.com/ai-startup-runway-integrates-stable-diffusion-for-text-to-video-editor/) and this [MIT Tech Review piece](https://www.technologyreview.com/2023/02/06/1067897/runway-stable-diffusion-gen-1-generative-ai-for-video/)
* 3/20 Created [new page](/foundation-model-stanford-paper-2022/) on Stanford paper "On the Opportunities and Risks of Foundation Models".
* 3/20 Found two useful articles from Lilian Weng's [blog](https://lilianweng.github.io):
	* [Prompt Engineering](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/)
	* [Updated version of Transformer Family](https://lilianweng.github.io/posts/2023-01-27-the-transformer-family-v2/) v2
* 3/20 Found a bunch of interesting resources re: Foundation models
	* [2023 MAD landscape](https://mattturck.com/mad2023/) posted by Matt Turck. [web version here](https://mad.firstmarkcap.com). 404's occasionally. Scroll to bottom right of blue ML+AI section to see box on Closed Source Models"
	* [Snorkel.ai intro guide](https://snorkel.ai/foundation-models/) dated March 1, 2023. 
	* Alan Thompson's Life Architect post [Inside language models](https://lifearchitect.ai/models/#summary-models) which is updated recently enough to include GPT-4 and to note that LLaMA has been leaked.
* [HN thread](https://news.ycombinator.com/item?id=35258553) about an alpaca tuned llama-7b chatbot. llama-30b coming soon. 
* Rodney Brooks [What Will Transformers Transform](https://rodneybrooks.com/what-will-transformers-transform/)
	* 'Generative Pre-trained Transformer' models (GPT) are now the rage and have inspired Kissinger and Noam Chomsky. That sure is some hype level
	* References Wolfram's excellent explainer
	* "By the way, even since the earliest days of AI, the 1955 proposal for the 1956 workshop on AI, the document in which the term AI first appears anywhere, the goal of the researchers was to produce general intelligence. That AGI is a different term than AI now is due to a bunch of researchers a dozen or so years ago deciding to launch a marketing campaign for themselves by using a new buzz acronym. 'AGI' is just 'AI' as it was known for the first 50+ years of its existence. Hype produced the term 'AGI' with which we are now saddled."
	* Quotes unconfirmed reports that GPT-4 has 1 trillion parameters, but that has been specifically debunked by Sam Altman and others. (compared with GPT-3 with 175-billion parameters)
	* All successful systems need to have a person in the loop. 
		* "This is true of language translation systems where a person is reading the output and, just as they do with children, the elderly, and foreigners, adapts quickly to the mistakes the person or system makes, and fill in around the edges to get the meaning, not the literal interpretation."
		* "This is true of speech understanding systems where we talk to Alexa or Google Home, or our TV remote, or our car. We talk to each of them slightly differently, as we humans quickly learn how to adapt to their idiosyncracies and the forms they can understand and not understand.
		* "This is true of our search engines, where we have learned how to form good queries that will get us the information we actually want, the quickest.
		* "This is true of mobile robots in hospitals, taking the dirty sheets and dishes to be cleaned, or bringing up prescriptions from the hospital pharmacy, where there is a remote network operations center that some unseen user is waiting to take over control when the robot gets confused."
	* Amara's Law, overestimate the effect of the tech in the short run and underestimate it in the long run.
		* John McCarthy’s estimate that the computers of the 1960’s were powerful enough to support AGI 
		* Minsky and Michie and Nilsson each believing that search algorithms were the key to intelligence, 
		* Neural networks (volume 3, perceptrons) [[I wasn’t around for the first two volumes; McCulloch and Pitts in 1943, Minsky in 1953]], 
		* First order logic, Resolution theorem proving, MacHack (chess 1), fuzzy logic, STRIPS, 
		* Knowledge-based systems (and revolutionizing medicine), 
		* Neural networks (volume 4, back propagation), the primal sketch, self driving cars (Dickmanns, 1987),
		* Reinforcement learning (rounds 2 and 3), SOAR, 
		* Support vector machines, self driving cars (Kanade et al, 1997), 
		* Deep Blue (chess 2), self driving cars (Thrun, 2007), Bayesian inference, Watson (Jeopardy, and revolutionizing medicine), 
		*  Neural networks (volume 5, deep learning), Alpha GO, reinforcement learning (round 4), generative images, and now large language models. 

	* All have heralded the imminence of human level intelligence in machines. All were hyped up to the limit, but mostly in the days when very few people were even aware of AI, so very few people remember the levels of hype. I’m old. I do remember all these, but have probably forgotten quite a few…
		* "None of these things have lived up to that early hype.

## 27 March 2023
* Downloaded recent Yann LeCun slides and summer 2022 paper summarizing his proposal to approach more human/animal like learning/intelligence for machines

* Articles by [Erich Grunewald](https://www.erichgrunewald.com) from this [HN thread](https://news.ycombinator.com/item?id=35332537):
	* [Prospect for an AI Winter](https://www.erichgrunewald.com/posts/the-prospect-of-an-ai-winter/)
	* [Against LLM Reductionism](https://www.erichgrunewald.com/posts/against-llm-reductionism/)


## Created [this page](/transformer-1) dedicated to Transformers papers and tutorials
## Created [this page](/python) dedicated to setting up Python environments

## 31 March 2023
* [vicuna 13B](https://news.ycombinator.com/item?id=35378683) is an online competitor based on LLaMA 13B but with different training

## 3 April 2023
* Interesting way of explaining uncanny confidence of LLMs by Devin Coldeway 4/03 in TechCrunch article ["The Great Pretender"](https://techcrunch.com/2023/04/03/the-great-pretender/)

## 10 April 2023
*  "On Efficient Training of Large-Scale Deep Learning Models: A Literature Review" by Li Shen, Yan Sun, Zhiyuan Yu, Liang Ding, Xinmei Tian, Dacheng Tao. [arXiv link](https://arxiv.org/abs/2304.03589) and [HN thread](https://news.ycombinator.com/item?id=35513510)
* Out of curiosity, I began probing ChatGPT, Bing, and Google on how they describe the difference between 'ordinary training', pre-training, and fine tuning. See archive of my chat histories at ChatGPT to see more.
	* see also [this stackexchange answer](https://stats.stackexchange.com/questions/193082/what-is-pre-training-a-neural-network/193451#193451) which draws on this [ML glossary](https://martin-thoma.com/ml-glossary/) -- look at answers for pre-training and fine-tuning.

## 11 April 2023
* [Listing of decentralized and open-source LLMs](https://github.com/imaurer/awesome-decentralized-llm#edge-llms) from this [HN comment](https://news.ycombinator.com/item?id=35527675)
* Found on [HN thread](https://news.ycombinator.com/item?id=35527907), this open-source orchestrator and performance evaluator of multiple LLMs [PhaseLLM](https://github.com/wgryc/phasellm) and related [collaborative data community](https://phaseai.com)


## 13 April 2023
* From Seymour in Slack, George Ho's survey from a few years ago (May 2020) of using [Transformers in NLP](https://www.georgeho.org/transformers-in-nlp/)
* from [HN](https://news.ycombinator.com/item?id=35565212), [productizing mature LLM eng pipelines](https://huyenchip.com/2023/04/11/llm-engineering.html)

## 14 April 2023
* From 3/28, [Cerebras-GPT](https://www.cerebras.net/blog/cerebras-gpt-a-family-of-open-compute-efficient-large-language-models/) is a family of open, compute-efficient, LLMs, ranging from 0.11B to 13B parameters. Trained using Chinchilla formula
* A nice concise, mathematically formal description of Transformers by Mary Phuong and Marcus Hutter at DeepMind, published 7/19/2022: [*Formal Algorithms for Transformers*](https://arxiv.org/abs/2207.09238). from this [HN comment](https://news.ycombinator.com/item?id=35506069) which also had this [HN comment](https://news.ycombinator.com/item?id=35507378) about Hopf algebras, including Adam Nemecek's 2/03/2023 paper [*Coinductive guide to inductive transformer heads*](https://arxiv.org/abs/2302.01834) and the older 2012 paper [*Hopf algebras and Markov chains: Two examples and a theory*](https://arxiv.org/abs/1206.3620) and a recommendation to check out [this website](https://bivector.net) about Geometric Algebra aka Clifford Algebra. Recommend watching this 44-minut intro [YouTube video](https://www.youtube.com/watch?v=60z_hpEAtD8&t=120s)
* Dan Fu, Michael Poli, Chris Re 3/28/2023 ["From Deep to Long Learning?"](https://hazyresearch.stanford.edu/blog/2023-03-27-long-learning)
* From this [HN thread](https://news.ycombinator.com/item?id=35544851), found this article by Eugene Yan at Amazon ["Experimenting with LLMs to Research, Reflect, and Plan"](https://eugeneyan.com/writing/llm-experiments/)

## 15 April 2023
* Found another reference to this good intermediate level discussion how transformers work. [The Illustrated Transformer](http://jalammar.github.io/illustrated-transformer/) by Jay Alammar. Originally noted on 3/01.
	* See also this previous post by Jay about [Attention](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
* Researchers at Allen Institute find a way to 6x the toxicity of ChatGPT. [Allen Institute blog post](https://blog.allenai.org/toxicity-in-chatgpt-ccdcf9265ae4) and [TC article](https://techcrunch.com/2023/04/12/researchers-discover-a-way-to-make-chatgpt-consistently-toxic/)
* Quote from Betaworks CEO John Borthwick: "This is the biggest change in technology in my lifetime. We’ve been building, accelerating and investing in and around machine learning for the last decade, and in the last 12 months, everything’s changed — the launch of generative visual models like [OpenAI’s] DALL-E 2 last year, the open and affordable access to these models with the availability of stability and GPT. AI has the potential to affect every sector, and every part of how we live, work, play and even die." Part of [Betaworks AI camp announcement](https://techcrunch.com/2023/04/13/betaworks-new-camp-aims-to-fund-transformative-early-stage-ai-startups/)

## 16 April 2023
* [Batch computing and AI](https://hazyresearch.stanford.edu/blog/2023-04-12-batch) and associated [HN thread](https://news.ycombinator.com/item?id=35589027) 
* New 'Consistency Models' are an upgrade over previous diffusion models for image generation and related visual tasks. [Paper](https://arxiv.org/abs/2303.01469) and [TC article](https://techcrunch.com/2023/04/12/openai-looks-beyond-diffusion-with-consistency-based-image-generator/)

## 17 April 2023
* Excellent compilation of various LLM resources by Sebastian Raschka. [Blog post](https://magazine.sebastianraschka.com/p/understanding-large-language-models) and associated [HN thread](https://news.ycombinator.com/item?id=35589756) with more resources
* Review article on ChatGPT related papers by [Zhang, Zhang, et al](https://arxiv.org/abs/2304.06488). From abstract: 'According to Google scholar, there are more than 500 articles with ChatGPT in their titles or mentioning it in their abstracts. Considering this, a review is urgently needed, and our work fills this gap. Overall, this work is the first to survey ChatGPT with a comprehensive review of its underlying technology, applications, and challenges. Moreover, we present an outlook on how ChatGPT might evolve to realize general-purpose AIGC (a.k.a. AI-generated content), which will be a significant milestone for the development of AGI.'
* [Together](https://www.together.xyz) released [RedPajama](https://www.together.xyz/blog/redpajama), a project to create 'reproducible, fully-open, leading language model. RedPajama is a collaboration between Together, Ontocord.ai, ETH DS3Lab, Stanford CRFM, Hazy Research, and MILA Québec AI Institute.'. 
	* three components: (1) Pre-training data, (2) Base models trained at scale with data from (1), and (3) Instruction tuning data and models for usability and safety
	* Released LLaMA training dataset of 1.2 trillion tokens

## 22 April 2023
* New [article by Sebastian Raschka](https://magazine.sebastianraschka.com/p/finetuning-large-language-models) with a comprehensive introduction to 'Finetuning LLMs'. Associated [HN thread](https://news.ycombinator.com/item?id=35666201)
	* Review again Jay's 2020 [Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) and his preceding [article on Attention](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)

## 24 April 2023
* [New paper](https://arxiv.org/abs/2304.11062) increases context window from 32k tokens for GPT-4 to 1M tokens using the Recurring Memory Transformer architecture (aka RMT). [HN thread](https://news.ycombinator.com/item?id=35682424) Point from this [HN comment]: 
	* 'For LLMs there are at least three different ways of "learning":
		1. *Pre-training* for text prediction, using unsupervised learning
		2. *Fine-tuning* e.g. to follow instructions or to reject certain queries, using supervised and/or reinforcement learning (optional)
		3. *In-context learning* using "few-shot prompts" as examples
	* 'Now the last two can have similar effects. For example, you might fine-tune a foundation (only pre-trained) model to follow instructions, or you don't and instead just modify your prompt such that it looks like a dialogue between a human and a helpful chat assistant.  But neither can replace the extensive pre-training phase, which is what gives the model all its intelligence.'
	* 'One other disanalogy between fine-tuning and in-context learning appears to be that the model can't exactly remember the data it was fine-tuned with, while it "knows" exactly everything in its context window. That is its working memory, so to speak.'

## 27 April 2023
* e2eml school's [Transformers from scratch](https://e2eml.school/transformers.html#markov_chain) nice diagrams on seq2seq etc
* Harvard SEAS Jupyter notebook [annotated version](http://nlp.seas.harvard.edu/annotated-transformer/) of original Transformer / attention-is-all-you-need paper
* arXiv paper from 3/22/2023 ['Sparks of AGI: Early experiments from GPT-4](https://arxiv.org/abs/2303.12712)
* A Cookbook of Self-Supervised Learning [paper](https://arxiv.org/abs/2304.12210) and [HN thread](https://news.ycombinator.com/item?id=35702490)

## 28 April 2023
* Shared by Yann LeCun on FB -- ['A Practical Guide for LLMs'](https://github.com/Mooler0410/LLMsPracticalGuide) with a history of taxonomic relationships between the various LLMs. Comments on FB from Yann: 
	* ‘A survey of LLMs with a practical guide and evolutionary tree.
	* ‘Number of LLMs from Meta = 7
	* ‘Number of open source LLMs from Meta = 7
	* ‘The architecture nomenclature for LLMs is somewhat confusing and unfortunate.
	* 'What's called "encoder only" actually has an encoder and a decoder (just not an auto-regressive decoder).
	* 'What's called "encoder-decoder" really means "encoder with auto-regressive decoder"
	* 'What's called "decoder only" really means "auto-regressive encoder-decoder"’
* GPT4Free - allows various projects without an OpenAI API key. Very empty [HN thread](https://news.ycombinator.com/item?id=35685512) and [project home](https://github.com/xtekky/gpt4free)
* Arxiv paper from Feb, 2023 ['Hyena Hierarchy: Towards Larger Convolutional Language Models'](https://arxiv.org/abs/2302.10866) and fragmentary [HN comment](https://news.ycombinator.com/item?id=35514579)
* ['Choose Your Weapon: Survival Strategies for Depressed AI Academics'](https://arxiv.org/abs/2304.06035) from March, 2023

## 30 April
* [A Brief History of LLaMA](https://agi-sphere.com/llama-models/) and [HN thread](https://news.ycombinator.com/item?id=35736872)
    * [this comment](https://news.ycombinator.com/item?id=35757925) indicates that [this GH repo](https://github.com/jankais3r/LLaMA_MPS) runs unquantized 7b and 13b models on an M2 GPU which means it's a little slower but much much more energy efficient.

## 01 May 2023
* [Mojo](https://www.modular.com/mojo)--a new programming language from [Chris Lattner's](https://en.wikipedia.org/wiki/Chris_Lattner), [new company Modular AI](https://www.modular.com). [HN thread](https://news.ycombinator.com/item?id=35790367)
* [Project](https://github.com/mlc-ai/mlc-llm/blob/main/README.md) to run LLMs on mobile devices and diverse hardware. 'Everything runs locally with no server support and accelerated with local GPUs on your phone and laptops. Supported platforms include: iphone/ipad, Metal GPUs and Intel/ARM MacBooks, AMD and NVIDIA GPUs via Vulkan on Windows and Linux, NVIDIA GPUs via CUDA, WebGPU on browsers through [WebLLM](https://github.com/mlc-ai/web-llm/blob/main/README.md).'
	* [HN thread](https://news.ycombinator.com/item?id=35763483) 

## 03 May 2023
* Recommended to read this nice article explaning RLHF -- ['Illustrating Reinforcement Learning from Human Feedback (RLHF)'](https://huggingface.co/blog/rlhf)

## 04 May 2023
* Two good intro articles by [Assembly AI](https://www.assemblyai.com/about):
	* [The Full Story of LLMs and RLHF](https://www.assemblyai.com/blog/the-full-story-of-large-language-models-and-rlhf/) and associated [HN thread](https://news.ycombinator.com/item?id=35803522)
	* [Intro to Generative AI](https://www.assemblyai.com/blog/introduction-generative-ai/)

## 05 May 2023
* Introductory 2021 blog post by Pinecone ['What is a Vector Database?'](https://www.pinecone.io/learn/vector-database/) and [HN thread](https://news.ycombinator.com/item?id=35826929)
* Deepgram blogpost ['Augmenting LLMs Beyond Basic Text Completion and Transformation'](https://blog.deepgram.com/augmenting-llms-beyond-basic-text-completion-and-transformation/) and [HN thread](https://news.ycombinator.com/item?id=35819613)

## 08 May 2023
* Lastest on which consumer hardware (including Apple Silicon) is effective for home training in [this comment thread](https://news.ycombinator.com/item?id=35861272) as part of this [HN post](https://news.ycombinator.com/item?id=35859344) about [RasaGPT](https://github.com/paulpierre/RasaGPT) which simplifies integration of multiple NLP, NLU, machine translation, etc using tools like Rasa, FastAPI, LangChain etc.
* Explanation of current landscape of diffusion models and why [Reflected Diffusion Models might be the next step](https://aaronlou.com/blog/2023/reflected-diffusion/) plus [HN thread](https://news.ycombinator.com/item?id=35863309)

## 15 May 2023
* [StarCoder and StarCoderBase](https://arxiv.org/abs/2305.06161) Foundation model StarCoderBase and finetuned tool called StarCoder. [HN thread](https://news.ycombinator.com/item?id=35954481)
* [Ash Vardanian](https://ashvardanian.com) implemented a 1000-line C++ vector database as announced in this short [HN thread](https://news.ycombinator.com/item?id=35803649). [Main blogpost here](https://ashvardanian.com/posts/abusing-vector-search/) and [main HN thread](https://news.ycombinator.com/item?id=35887983)

## 18 May 2023
* ACM article on [Cargo Cult AI](https://queue.acm.org/detail.cfm?ref=rss&id=3595860) and [HN thread](https://news.ycombinator.com/item?id=35991362)

## 20 May 2023
* Dialogue between [Don Knuth and Stephen Wolfram](https://cs.stanford.edu/~knuth/chatGPT20.txt) regarding Knuth's test questions to ChatGPT. [HN thread](https://news.ycombinator.com/item?id=36012360)
* Rodney Brooks says to 'calm down about GPT-4' in [IEEE](https://spectrum.ieee.org/gpt-4-calm-down) and [HN thread](https://news.ycombinator.com/item?id=36017309)
* Rich Sutton of Reinforcement Learning textbook fame and his [The Bitter Lesson](http://incompleteideas.net/IncIdeas/BitterLesson.html) reappeared on [HN](https://news.ycombinator.com/item?id=36017857)


## 22 May 2023
* New paper by Meta about how fine-tuning is much less important than pre-training ['LIMA: Less is More for Alignment'](https://arxiv.org/abs/2305.11206) -- Minimal finetuning is still effective suggesting that bulk of work is done during pre-training. Uses 65-B version of LLaMA

## 23 May 2023
* [RWKV: Reinventing RNNs in the Transformers Era](https://arxiv.org/abs/2305.13048) New paper thaT tries to rebuild RNNs to get the benefits of Transformer attention while scaling more efficiently. [PDF](https://news.ycombinator.com/item?id=36038868)
* Meta launches mutltilingual model from the prior SOTA 100 languages to [1100+ languages](https://ai.facebook.com/blog/multilingual-model-speech-recognition/)
* Sebastian Raschka has [another post up](https://magazine.sebastianraschka.com/p/why-the-original-transformer-figure) about 'Why the original transformer drawing is wrong and some other historical tidbits about LLMs'. [HN thread](https://news.ycombinator.com/item?id=36057183)

## 26 May 2023
* [HN thread](https://news.ycombinator.com/item?id=35994037) about building CLI tools to work with ChatGPT and LLMs by [Simon Willison](https://simonwillison.net/2023/May/18/cli-tools-for-llms/)
* Stanford paper on [AlpacaFarm](https://crfm.stanford.edu/2023/05/22/alpaca-farm.html) which has been RHLFed to 'beat ChatGPT-3.5'. [HN thread](https://news.ycombinator.com/item?id=36052411)
* Paper written by several AI/ML PhD students about how to do [NLP research in the age of LLMs](https://arxiv.org/abs/2305.12544) and [HN thread](https://news.ycombinator.com/item?id=36080886)

## 27 May 2023
* New paper ['QLoRA: Efficient Finetuning of Quantized LLMs'](https://arxiv.org/abs/2305.14314) and [HN thread](https://news.ycombinator.com/item?id=36064568) 
	* Follow up August article by Databricks ['Efficient Fine-Tuning with LoRA: A Guide to Optimal Parameter Selection for Large Language Models'](https://www.databricks.com/blog/efficient-fine-tuning-lora-guide-llms)

## 28 May 2023
* Good PDF ['The Little Book of Deep Learning'](https://www.fleuret.org/public/lbdl.pdf) and related [HN thread](https://news.ycombinator.com/item?id=35767789)
* FB publishes paper ['MEGABYTE: Predicting Million-byte Sequences with Multiscale Transformers'](https://arxiv.org/abs/2305.07185) with [effusive commentary](https://www.artisana.ai/articles/meta-ai-unleashes-megabyte-a-revolutionary-scalable-model-architecture) and [HN thread](https://news.ycombinator.com/item?id=36053662)
* 5/27/2023 casual [listing of AI chips](https://news.ycombinator.com/item?id=36095965) from this [HN thread 'Ask HN: What is an AI chip and how does it work?](https://news.ycombinator.com/item?id=36092831)
* a16z collects together various deep learning resources in [The AI Canon](https://a16z.com/2023/05/25/ai-canon/) and [HN thread](https://news.ycombinator.com/item?id=36072268)
* Xorvoid criticism of LLMs called ['ChatGPT: A Mental Model'](https://xorvoid.com/chatgpt_a_mental_model.html) and critical back and forth at [HN](https://news.ycombinator.com/item?id=36099822)

## 06 June 2023
* Need to investigate running LLMs locally with [ggml.ai](http://ggml.ai) which works with llama.cpp whisper, etc. Optimized for Apple Silicon. [HN thread](https://news.ycombinator.com/item?id=36215651)

## 20 June 2023
* SimpleAIchat on [GitHub](https://github.com/minimaxir/simpleaichat) -- a new and concise Python package for easily interacing with chat apps like GPT-4 with robust features and minimal code complexity. [HN thread](https://news.ycombinator.com/item?id=36393782) 

## 27 June 2023
* Lilian Weng has another detailed overview post up on her excellent blog about ['Autonomous Agents'](https://lilianweng.github.io/posts/2023-06-23-agent/). [HN thread](https://news.ycombinator.com/item?id=36488871)


## 05 July 2023
* From February, 2023, ['A human just defeated an AI in Go. Here’s why that matters'](https://news.ycombinator.com/item?id=36590242), and [HN thread](https://news.ycombinator.com/item?id=36590242)
* How metaphors shape our understanding of computing and AI ['https://windowsontheory.org/2023/06/28/metaphors-for-ai-and-why-i-dont-like-them/'](https://windowsontheory.org/2023/06/28/metaphors-for-ai-and-why-i-dont-like-them/)
* [July 2023 Bret Victor / worrydream update HN thread](https://news.ycombinator.com/item?id=36596095&ref=upstract.com). Older Vimeo 2014-era videos [Victor's CV](http://worrydream.com/#!/cv): Short [15-minute Seeing Spaces](http://worrydream.com/SeeingSpaces/) and longer 55-minute [Humane Representation of Thought](https://vimeo.com/115154289)

## 11 July 2023
* New personal [guide to LangChain](https://blog.kevinhu.me/2023/07/10/hacking-langchain-for-fun-and-profit/) and associated [HN thread](https://news.ycombinator.com/item?id=36669866) 


## 26 August 2023
* Meta released two large models recently, one for code, one for translations in the past week.

## 20 September 2023
* Some Llama 2 links:
	* 7/27 [article by Lucas Pauker](https://lucaspauker.com/articles/llms-unleashed-the-power-of-fine-tuning) Some explanations on how to fine-tune a model and performance of pre-training vs fine-tuning.
		* Comment by [Jeremy Howard}(https://news.ycombinator.com/item?id=36900969) and progress of what GPT and BERT did in terms of simplifying fine-tuning. From this [HN thread](https://news.ycombinator.com/item?id=36896710)
	* 8/01 [article by Ollama](https://ollama.ai/blog/run-llama2-uncensored-locally) about how an uncensored locally running version of Llama-2 compares. [HN thread](https://news.ycombinator.com/item?id=36973584) with relevant [top comment](https://news.ycombinator.com/item?id=36975031)
* Interesting Simon Willison [blog about using Claude to summarize Hacker News](https://til.simonwillison.net/llms/claude-hacker-news-themes)
* Ongoing comparison of best GPU CLouds for Nvidia A100 (2020 vintage) vs. H100 (2022). [Blog post](https://llm-utils.org/Nvidia+H100+and+A100+GPUs+-+comparing+available+capacity+at+GPU+cloud+providers) and [HN thread](https://news.ycombinator.com/item?id=36333321)

## 26 September 2023
* [Intro Oracle article on RAG](https://www.oracle.com/artificial-intelligence/generative-ai/retrieval-augmented-generation-rag/) from 9/19/2023.
* LangSmith videos from Google search on 8/28
	https://www.youtube.com/watch?v=tFXm5ijih98
	https://www.youtube.com/watch?v=bE9sf9vGsrM
	https://www.youtube.com/watch?v=odxlHNLWAk4
	https://www.youtube.com/watch?v=Weod3-ZPaPM
	https://www.youtube.com/watch?v=ll-Xit_Khq0
* Vector database available in GCP?
	* [Paid search result](https://archive.pinecone.io/lp/vector-database/) 
	* [GCP integrates Vector Search in Managed Databases](https://www.infoq.com/news/2023/07/gcp-databases-vector-search/)
* Above links/notes copied to 2-post in 2-astro


## 09 October 2023
* A lot of updates added to `/5-slides`, `/71-gpt3`, `/72-gpt4`, `/74-llama2`
* Anthropic has [a new paper](https://www.anthropic.com/index/decomposing-language-models-into-understandable-components) that pushes forward capability of interpreting ANNs. Instead of trying to understand a single artificial neuron, this is able to find a better unit of analysis, called features. A feature by their definition corresponds to linear combinations of a neural activations.

## 13 October 2023
* Updated version of the paper ['Textbooks are all you need'](https://arxiv.org/abs/2306.11644) - October, 2023 that includes the 1.5 version of the [phi model](https://venturebeat.com/business/meet-phi-1-5-the-new-language-model-that-could-make-training-ai-radically-cheaper-and-faster/) from Microsoft Research. Phi-1.5 is an LLM that could make training AI radically cheaper and faster.
	* See also this [KD Nuggets article](https://www.kdnuggets.com/effective-small-language-models-microsoft-phi-15) about the same Phi-1.5 model. Only has 1.3B parameters but performs well!
* September 2023 paper showing how effectively foundation models can scale to long contexts (aka 32k tokens). ['Effective Long-Context Scaling of Foundation Models.'](https://arxiv.org/abs/2309.16039)
* Good article by Jeremy Howard and author Sylvain Gugger on [the history of the AdamW algorithm](https://www.fast.ai/posts/2018-07-02-adam-weight-decay.html) as a competitor to SGD.
* New article from Lightning.ai on ['Finetuning LLMs with LoRA and QLoRA: Insights from Hundreds of Experiments'](https://lightning.ai/pages/community/lora-insights/). 

## 25 October 2023
* New Jina AI release launches [open-source 8k text embedding](https://jina.ai/news/jina-ai-launches-worlds-first-open-source-8k-text-embedding-rivaling-openai/) and [HN thread](https://news.ycombinator.com/item?id=38020109). Also Simon Willison has already built a [Jina plugin for this](https://simonwillison.net/2023/Oct/26/llm-embed-jina/) and explains embeddings in general [in this blog post](https://simonwillison.net/2023/Oct/23/embeddings/)

## 13 November 2023
* Maybe CNNs are not quite obsolete. Places where convolutional neural nets perform as well as transformers. ['The convolution empire strikes back'](https://gonzoml.substack.com/p/the-convolution-empire-strikes-back)
* Paper: 'Evaluating Large Language Models: A Comprehensive Survey'. [arXiv link](https://arxiv.org/abs/2310.19736). [PDF](https://arxiv.org/pdf/2310.19736.pdf).
* Important summary article on [AI and Open Source](https://magazine.sebastianraschka.com/p/ai-and-open-source-in-2023) in 2023 by Sebastian Raschka.
* Rust and Web Assembly language for faster lighterweight LLMs? [article](https://www.secondstate.io/articles/fast-llm-inference/) and [HN thread](https://news.ycombinator.com/item?id=38246668)

## 11 December 2023
* Funding announcement of [Liquid AI](https://techcrunch.com/2023/12/06/liquid-ai-a-new-mit-spinoff-wants-to-build-an-entirely-new-type-of-ai/), MIT startup focused on [LTC aka Liquid Time Constant ANNs](https://arxiv.org/abs/2006.04439) from research in late 2020/early 2021. Follow-up with additional resources in this [LTC-SE paper](https://arxiv.org/abs/2304.08691) applied to embedded systems in April 2023.

## 2024 Gen AI

## 01 January 2024
* On [HN](https://news.ycombinator.com/item?id=38834244) front page today, found a reference to this [arXiv page](https://arxiv.org/abs/2310.20360) 600-page book 'Mathematical Introduction to Deep Learning: Methods, Implementations, and Theory'. Published October, 2023 from a course given at ETH Zurich by academics Arnulf Jentzen, Beno Kuckuck, Philippe von Wurstemberger. 
* From the same [HN thread](https://news.ycombinator.com/item?id=38835197), found this draft book in progress. *Understanding Deep Learning* by Simon J.D. Prince. [Main page here](https://udlbook.github.io/udlbook/). 
	* Nice because the free PDF of this book section 1.6 has nice references as of Dec 2023 about good textbooks and other resources on a various approaches to DL, including math focused, coding-focused, computer vision optimized, reinforcement learning focused, etc.
    * Also dives into argmin and argmax pretty early. Handy [wiki article](https://en.wikipedia.org/wiki/Arg_max) on arg max functions. 
* From same thread, and also referenced in the Prince UDL book, began looking at Bishop (2006) *Pattern Recognition and Machine Learning* textbook. Per [this HN comment](https://news.ycombinator.com/item?id=38836444), Bishop has a simpler notation than the 600-pg ETH book by Jentzen et al. Bishop's notation is clear like Goodfellow (2016) but is a little mathematically deeper. 
	* Most importantly, Bishop has a good self-contained introduction to the relevant probability theory.

## 07 January 2024
* Good overview and history of various [RAG variants](https://arxiv.org/abs/2312.10997) for Retrieval-Augmented Generation for LLMs.
* Re-found and re-read piece by Sebastian Mellen on ['Summarization is the Killer Use Case for LLMs'](https://news.ycombinator.com/item?id=37946023) with [HN comment by Simon Willson](https://news.ycombinator.com/item?id=37946389) and general [HN thread](https://news.ycombinator.com/item?id=37946389).

G
## 12 January 2024
* Multiple resources on the latest in vector database in this [HN thread](https://news.ycombinator.com/item?id=38971221)

## 15 January 2024
* Run-through of Hyung Won Chung's [slides](https://docs.google.com/presentation/d/1636wKStYdT_yRPbJNrf8MLKpQghuWGDmyHinHhAKeXY/edit#slide=id.g27b2b69cf28_1_1094) from OpenAI. Originally sent by Seymour October, 2023.
* JP Morgan AI Research published [DocLLM](https://arxiv.org/abs/2401.00908) a multi-modal LLM that can interpret invoices, receipts, purchase orders, and other visually laid out forms. Posted to [FB group](https://www.facebook.com/groups/DeepNetGroup/permalink/2115818488811022/) on 1/12/2024. 
* November 2023 survey of Multi-Modal LLMs at [arXiv](https://arxiv.org/abs/2311.13165?fbclid=IwAR1GfPDG_JEjaP0ZysadyGA31jPSL7VIZRWwVvpzNHLRg9Nb1UUNgLPota0) posted on 1/15/2024 at FB Group [AI+DL](https://www.facebook.com/Myeongha0929/posts/pfbid02FDAoXkc3z6hUveJtjU1x93ADvYimyhu63ciD1CMEevuB8ksHn7yuV5x2BTW6Rfhwl).

## 17 January 2024
* [HN comment](https://news.ycombinator.com/item?id=39029084) about how it's more than just focusing on chat interaction that one has to be thoughtful about extracting and searching to get relevant context. "you can't just throw chunks into a vector DB". Part of this [HN thread](https://news.ycombinator.com/item?id=39000241) responding to this article on ['RAG using data & role of knowledge graphs'](https://kuzudb.com/docusaurus/blog/llms-graphs-part-2/).

## 15 February 2024
* New OpenAI text-to-video model called Sora
	* [Blog post](https://openai.com/sora)
	* [Research paper](https://openai.com/research/video-generation-models-as-world-simulators)
	* [#1 item on HN homepage,](https://news.ycombinator.com/item?id=39386156) Has 1200 comments posted in the last 6 hours alone.

## 20 February 2024
* [Are we at peak vector database?](https://softwaredoug.com/blog/2024/01/24/are-we-at-peak-vector-db) and [HN thread](https://news.ycombinator.com/item?id=39119198).
* Sebastian Raschka article on [Coding LoRA from Scratch](https://lightning.ai/lightning-ai/studios/code-lora-from-scratch?view=public&section=all) and [HN thread](https://news.ycombinator.com/item?id=39091777)
* Another Raschka article [Improving LoRA: Implementing Weight-Decomposed Low-Rank Adaptation (DoRA) from Scratch](https://magazine.sebastianraschka.com/p/lora-and-dora-from-scratch) from 2/18/2024.
* Interesting 2016 blog post examining why debugging, not math, is the reason [Why machine learning is hard](https://ai.stanford.edu/~zayd/why-is-machine-learning-hard.html) and [HN thread](https://news.ycombinator.com/item?id=39109481)
* Training a small (~10m parameter) transformer following Andrej Karpathy's tutorial. [Beyond Self-Attention: How a Small Language Model Predicts the Next Token](https://shyam.blog/posts/beyond-self-attention/) and [HN thread](https://news.ycombinator.com/item?id=39251909)

## 21 February 2024
* New Andrej Karpathy [YouTube video](https://www.youtube.com/watch?v=zduSFxRajkE) focused on tokenizing. After he left OpenAI a few weeks ago. [HN thread](https://news.ycombinator.com/item?id=39443965)

## 24 February 2024
* Quick summary overview of Mamba--which is a way for Transformer/Attention architectures to reduce the quadratic growth in computational demand as sequence length increases. [Mamba: The Easy Way](https://jackcook.com/2024/02/23/mamba.html) by Jack Cook and [HN thread](https://jackcook.com/2024/02/23/mamba.html)
	* Mamba created by Albert Gu and Tri Dao. Sasha Rush aka [Alexander Rush](https://rush-nlp.com) wrote [Mamba: The Hard Way](https://srush.github.io/annotated-mamba/hard.html).
* Feb 2024 survey of LLMs by Shervin Minaee, T. Mikolov, N. Nikzad, ..., X. Amatriain, Jianfeng Gao. [arXiv link](https://arxiv.org/abs/2402.06196).

## 01 April 2024
* After multi-year delay, Grant Sanderson posted a new YouTube video in his "What is a neural network?" series. [Chapter 5: But what is GPT?](https://www.youtube.com/watch?v=wjZofJX0v4M) 

## 08 April 2024
* Paper last week on how undifferentiated / unstructured large volume of AI Agents are all you need. Title: 'More Agents Is All You Need' -- [arXiv link](https://arxiv.org/abs/2402.05120) and [HN thread](https://news.ycombinator.com/item?id=39955725)

## 18 November 2024
* LoRA versus Full Fine Tuning: An Illusion of Equivalence. [arXiv](https://arxiv.org/abs/2410.21228) and [HN thread](https://news.ycombinator.com/item?id=42085665)

## 20 December 2024 
* [HN post](https://news.ycombinator.com/item?id=42196037) about history of AI: ['Between the Booms: AI in Winter'](https://cacm.acm.org/opinion/between-the-booms-ai-in-winter/). Written by [Thomas Haigh](https://www.linkedin.com/in/thomashaigh/), Professor of History at University of Wisconsin-Milwaukee. [Biography](https://www.iwm.at/fellow/thomas-haigh) at [Institute for Human Sciences (IWM)](https://www.iwm.at/about/mission-and-vision), retrieved Jan, 2025: 
	* *'The history of artificial intelligence (AI) is the history of an intellectual brand, now almost seven decades old, that has somehow survived cycles of hype, disillusion, contestation, and redefinition to reemerge stronger than ever. The project aims to historicize artificial intelligence and move beyond the narratives of its proponents and the counter claims of its historical critics. Because the artificial intelligence brand has been applied over time to fundamentally different approaches, this will be a short history that speaks to many long histories. The history of artificial intelligence is the history of the unfulfilled promise that computers can be programmed to do the things that make humans uniquely intelligent, a promise that stays unfulfilled in part because we constantly redefine intelligence to exclude things that computers become good at. And it is the history of an actual existing academic discipline––with textbooks, college curricula, journals and professional associations––that tried to assemble a body of techniques and technologies sufficient to justify the hype and redeem the promise.'*
* It's the [fourth](https://cacm.acm.org/opinion/between-the-booms-ai-in-winter/) in 4 columns at the Communications of the ACM blog:
	1. ['Conjoined Twins: AI and the Invention of Computer Science'](https://cacm.acm.org/opinion/conjoined-twins-artificial-intelligence-and-the-invention-of-computer-science/)
	1. ['There Was No First AI Winter'](https://cacm.acm.org/opinion/there-was-no-first-ai-winter/)
	1. ['How the AI Boom Went Bust'](https://cacm.acm.org/opinion/how-the-ai-boom-went-bust/) 
	1. ['Between the Booms: AI in Winter'](https://cacm.acm.org/opinion/between-the-booms-ai-in-winter/)
* [DynaSaur: Large Language Agents Beyond Predefined Actions](https://arxiv.org/abs/2411.01747) and [HN thread](https://news.ycombinator.com/item?id=42286397)

## 23 January 2025
* Antropic AI announces [Citations API](https://www.anthropic.com/news/introducing-citations-api). [HN thread](https://news.ycombinator.com/item?id=42807173) has some interesting comments about grounding prompts when looking for scientific/medical paper annotations, including some debate involving Simon Willison.
* [Thoughts on Using AI Coding Assistant Devin for a Month](https://www.answer.ai/posts/2025-01-08-devin.html) and [HN thread](https://news.ycombinator.com/item?id=42734681)
* Simon Willison's round up of [Things we learned about LLMs in 2024](https://simonwillison.net/2024/Dec/31/llms-in-2024/). Long, linked, thoughtful list. [HN thread](https://news.ycombinator.com/item?id=42560558)

## 06 February 2025
* Sebastian Raschka on recent 2024-2025 developments in [Reasoning LLMs](https://magazine.sebastianraschka.com/p/understanding-reasoning-llms) and [HN thread](https://magazine.sebastianraschka.com/p/understanding-reasoning-llms). Four strategies for building and improving reasoning models:
	1. Inference-time scaling
	1. Pure RL reinforcement learning
	1. RL + Supervised Fine Tuning (SFT)
	1. Distillation
* Also has commentary on DeepSeek R1 in the same post.

## 09 April 2025
* Google announces (potential competitor to [MCP - Model Context Protocol](https://modelcontextprotocol.io/introduction) from Anthropic). Something called [agent2agent - a2a protocol](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)
	* [HN thread](https://news.ycombinator.com/item?id=43631381)
	* [HN comment](https://news.ycombinator.com/item?id=43638107): 
		* '*A key difference between MCP and A2A that is apparent to me after building with MCP and now reading the material on A2A.*
		* '*MCP is solving specific problems people have in practice today. LLMs need access to data that they weren't trained on, but that's really hard because there's a millions different ways you could RAG something. So MCP defines a standard by which LLMs can call APIs through clients. (and more).*
		* '*A2A solves a marketing problem that Google is chasing with technology partners.*
		* '*I think I can safely say which one will still be around in 6 months, and it's not the one whose contributors all work for the same company.*'
