---
title: Notes on Fine-Tuning and RAG
permalink: /ft-and-rag/
---

## 2023 Log

## 9/20/2023
### Fine-Tuning links
* ['Fine tuning is for form, not facts'](https://www.anyscale.com/blog/fine-tuning-is-for-form-not-facts) by Anyscale. Posted July 2023
* Amazon ['jumpstart foundation models and customize rag'](https://docs.aws.amazon.com/sagemaker/latest/dg/jumpstart-foundation-models-customize-rag.html)

### Overview of fine-tuning
* Single slide summarizing the entire production process. Foundation model construction, self-supervised trainingin, then the fine-tuning at the end. 

## 9/29/2023
* Read [Nous-Hermes thread](https://twitter.com/Teknium1/status/1682459395853279232?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1682459395853279232%7Ctwgr%5Ee2e857234d07d452699f1396d249e307c856468b%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fwww.redditmedia.com%2Fmediaembed%2F155wwrj%2F%3Fresponsive%3Dtrueis_nightmode%3Dtrue)
* The Bloke at [HF](https://huggingface.co/TheBloke/Nous-Hermes-13B-GGML)
* [YouTube video](https://www.youtube.com/watch?v=iOJD1hw2xaw) by Fahd Mirza. Three ways of final adjustments to a foundation model:
	1. Prompt Engineering. Zero-shot vs. Few-Shot Learning
	1. Fine-Tuning. Instruction-based vs. Domain-based
	1. RAG. Process includes:
		1. Gathering data from data sources and extracting data
		1. Transforming data into appropriate format  
		1. Embedding this data in vector format and loading into a vector DB
* Straightforward and simple [IBM video](https://www.youtube.com/watch?v=T-D1OfcDW1M)
	1. Critical point. RAG is a small data store that is quick and easy to update with new information without having to retrain the whole foundation model. 
	1. It can also be clearer about what source it is using for a given fact. and if there are no good sources to back it up, the LLM is instructed to not be as confident or simply say i don't know or that there are not good sources about this.

## 9/30
* Hardware Corner has a [link to all versions of nous-hermes](https://www.hardware-corner.net/llm-database/Nous-Hermes/)

## 10/03
### Text from [François Chollet's Twitter](https://twitter.com/fchollet/status/1709242747293511939) on 10/3:

* My interpretation of prompt engineering is this:

	1. A LLM is a repository of many (millions) of vector programs mined from human-generated data, learned implicitly as a by-product of language compression. A "vector program" is just a very non-linear function that maps part of the latent space unto itself.
	2. When you're prompting, you're fetching one of these programs and running it on an input -- part of your prompt serves as a kind of "program key" (as in database key) and part serves as program argument(s). Like, in "write this paragraph in the style of Shakespeare: {my paragraph}", the part "write this paragraph in the stye of X: Y" is a program key, with arguments X=Shakespeare and Y={my paragraph}.
	3. The program fetched by your key may or may not work well for the task at hand. There's no reason why it should be optimal. There are lots of related programs to choose from.
	4. Prompt engineering represents a search over many keys in order a find a program that is empirically more accurate for what you're trying to do. It's no different than trying different keywords when searching for a Python library.
	5. Everything else is unnecessary anthropomorphism on the part of the prompter. You're not talking to a human who understands language the way you do. Stop pretending you are.

* The more powerful the models become, the more programs they store. And the benefits of finding the right program (by figuring out the right prompt) become even greater.
* Unless LLMs change substantially in the future, prompt engineering is not going anywhere. What's going to happen, however, is that it will likely get automated so the end user doesn't have to deal with it. Better program search.
### [FChollet's substack post](https://fchollet.substack.com/p/how-i-think-about-llm-prompt-engineering) about prompt engineering. 10/09

## 10/06
* Article on Parameter-Efficient Fine-Tuning [PEFT](https://huggingface.co/blog/peft)

## 10/08 New video on fine-tuning by Trelis Research
* Posted October 7. 2023
* [Link](https://www.youtube.com/watch?v=71x8EMrB0Gc)
* Outline
	* Why instruction fine-tuning
	* special start and stop tokens
	* Guanaco instruction fine-tuning
	* Llama2 prompt format
	* chatml prompt format
	* instruction finetuning datasets
	* pro-tips
* See JH's [main transformer page](/transformer) to see notes on IBM video 2 specific to fine-tuning

## See also show-notes in 0-tue
* for updated listing of prompt engineering techniques


## 10/13
* New article from Lightning.ai on ['Finetuning LLMs with LoRA and QLoRA: Insights from Hundreds of Experiments'](https://lightning.ai/pages/community/lora-insights/). 






