---
title: Python Notes
permalink: /python/
---

## 3/30/2023
### Articles on setting up python environment
* First, install mamba as a lighter weight and faster alternative to conda
* Next, install jupyter notebook server which relies on mamba + python
* Also read this article on [Managing Python Environment in 2022](https://aseifert.com/p/python-environments/)
* Less necessary, but read [this section](https://realpython.com/python-virtual-environments-a-primer/#what-other-popular-options-exist-aside-from-venv) of this longer, more comprehensive [article](https://realpython.com/python-virtual-environments-a-primer/) on understanding venv in particular. But it also has comments on virtualenv, conda, etc.
* Ross Dobson's January 2022 tutorial on [setting up Python environments with Mambaforge](https://ross-dobson.github.io/posts/2021/01/setting-up-python-virtual-environments-with-mambaforge/)
* This 2020 update to an older 2018 version of a post explains why ["Pip is here to stay!"](https://chriswarrick.com/blog/2018/07/17/pipenv-promises-a-lot-delivers-very-little/#pip-is-here-to-stay)
* Older 2018 piece on ["Why You Need Python Environments and How to Manage Them with Conda"](https://www.freecodecamp.org/news/why-you-need-python-environments-and-how-to-manage-them-with-conda-85f155f4353c/)
* Cached version of this older Coiled blog post on ["Use Mambaforge to Conda Install PyData Stack on your Apple M1 Silicon Machine"](https://webcache.googleusercontent.com/search?q=cache:AmxeEUnBp84J:https://www.coiled.io/blog/apple-arm64-mambaforge&cd=6&hl=en&ct=clnk&gl=us&client=safari)

### Andrej Karpathy videos to watch on Transformers
* Makemore series
	* [Makemore 1](https://www.youtube.com/watch?v=PaCmpygFfXo&t=198s)
	* [Makemore 2](https://www.youtube.com/watch?v=TCH_1BHY58I)
	* [Makemore 3](https://www.youtube.com/watch?v=P6sfmUTpUmc)
	* [Makemore 4](https://www.youtube.com/watch?v=q8SA3rM6ckI)
	* [Makemore 5](https://www.youtube.com/watch?v=t3YJ5hKiMQ0)
* Main [Transformer video](https://www.youtube.com/watch?v=kCc8FmEb1nY&t=13s)

## 4/01/2023
* Quote from aseifert's [article](https://aseifert.com/p/python-environments/): "Pip, venv, virtualenv, pyenv, pipenv, micropipenv, pip-tools, conda, miniconda, mamba, micromamba, poetry, hatch, pdm, pyflow 🤯 These days even the most senior Python developer is confused about all the options to manage environments."
* After successful install of mambaforge from github (see ON notes), i verified that both conda info and mamba info work. Eventually, I should read [this page](https://mamba.readthedocs.io/en/latest/user_guide/mamba.html) from the mamba docs site.
* Took multiple steps, but using [this YouTube video](https://www.youtube.com/watch?v=Qq8gPwRpbp0)I was able to: (1) install mamba, (2) install python 3.10 within mamba, (3) install jupyter lab, (4) activate the jupyter mamba 'space' or whatever it's called, and (5) launch the jupyter server and connect to it from my local web client.
* Out of curiosity, I wondered how well PyTorch works with Apple Silicon and was led by this [reddit comment](https://www.reddit.com/r/pytorch/comments/10g7jw8/state_of_mps_apple_m1m2_support_in_pytorch/) to this PyTorch [GitHub issue](https://github.com/pytorch/pytorch/issues/77764)
* Should go through the basic [PyTorch tutorial](https://pytorch.org/tutorials/beginner/basics/quickstart_tutorial.html) and download the Jupyter notebook to run locally or can run through Google Colab.

## 4/02/2023

# Jupyter Notes
* Mamba + Jupyter setup video [How to install JupyterLab using Mamba](https://www.youtube.com/watch?v=Qq8gPwRpbp0)
* In the proper mamba environment, run 'jupyter notebook' and it should start the server in the terminal and automatically open a web browser client. Success!

# PyTorch Notes
* Installing pytorch using conda / mamba. Gated Medium [Towards Data Science article](https://towardsdatascience.com/installing-pytorch-on-apple-m1-chip-with-gpu-acceleration-3351dc44d67c) 
* Successfully installed stable 2.0.0 version for Apple Silicon using 'mamba install pytorch torchvision -cpytorch'

# Mamba / Conda Notes
* To see list of conda environments created, use this command 'conda info --envs'
* Steps:
	1. install conda by navigating to [mamba-forge](https://github.com/conda-forge/miniforge#mambaforge) at github. Download the "Mambaforge-MacOSX-arm64.sh", navigate to the directory, and then execute the shell script by typing 'Mambaforge-MacOSX-arm64.sh' from the command line.
	1. create an environment for pytorch. E.g., I want to call my personal pytorch environment *pytorch-jh*, so i type 'mamba create -n pytorch-jh -c conda-forge python=3.10'
		* 'create -n pytorch-jh' creates the environment called *pytorch-jh*
		* 'create -c conda-forge' indicates i need to download python from the *conda-forge* channel
		* 'python=3.10' pins the version of python as 3.10 for the *pytorch-jh* environment
	1. Download jupyter packages into *pytorch-jh* with this command 'mamba install -n pytorch-jh -c conda-forge jupyterlab'
	1. Download PyTorch packages into *pytorch-jh* with this command 'mamba install -n pytorch-jh pytorch torchvision -cpytorch'
		* 'install -n pytorch-jh' means install into the *pytorch-jh* environmnet
		* the list of packages per PyTorch.org are: *pytorch*, *torchvision*, 
		* i'm not exactly sure what '-cpytorch' is doing but it somehow knew to download the mac-os-arm64 version so I think this is related
* Verified that pytorch is working and using the M2 GPU by running 1jh_test.py and 2jh_test.py adapted from the above [Towards Data Science article](https://towardsdatascience.com/installing-pytorch-on-apple-m1-chip-with-gpu-acceleration-3351dc44d67c) 

***

## 4/06/2023
* Used ChatGPT to find latest in Python books and courses
* Thoughts and notes on lists (ordered) vs. dictionaries (unorderd key-value pairs, allowing duplicate values) vs. sets (like dicts but unique with no distinct values)
* examples of iterables. All of the 3 above plus strings. See
* zip() function. strip() / lstrip() / rstrip() to get rid of whitespace characters. difference between pop() and delete().
* using python interpreter, up to 'Organizing a List' on p. 42
* when in doubt about using an array versus a standard python list, use the better, more mathematically useful [numpy.array()](https://numpy.org/doc/stable/reference/generated/numpy.array.html) 
	* Do *not* default to [array.array()](https://docs.python.org/3/library/array.html) which is a [C-style array](https://pimylifeup.com/python-arrays/).
Instead, use the more mathematically useful [numpy.array()](https://numpy.org/doc/stable/reference/generated/numpy.array.html)

## 4/07/2023
* [Simple explanation](https://careerkarma.com/blog/python-operator/) for '+=' operator. Initialize 'a = 10'. To set a to 17, you can then type 'a += 7'. Then, print(a) will return '17'.

## 4/12/2023
* Found via phind.com's answer about tensors vs. multi-dimensional array. This [article](https://machinelearningmastery.com/one-dimensional-tensors-in-pytorch/) a pretty good simple way of getting familiar with PyTorch tensors. Requires import of torch, numpy, and pandas

## 4/13/2023
* Comprehensions are useful syntatic sugar for quickly populating and looping through both lists and dictionaries.
* Concept of "collections" useful noun as explained in this [YouTube about list comprehensions](https://www.youtube.com/watch?v=AhSvKGTh28Q&t=80si) (80 seconds in)


## 4/27/2023
* Began reading Bruce Eckel's Thinking in Python old PDF.


***

## 7/08/2024
* Bunch of info on Python environment/version/package managers on Hacker News today. 
	* This [article by Larry Du](https://dublog.net/blog/so-many-python-package-managers/) summarizes state of the art as of July 2024. [HN thread](https://news.ycombinator.com/item?id=40905891).
	* [Introduction to Rye](https://rye.astral.sh), [Intro YouTube video](https://www.youtube.com/watch?v=q99TYA7LnuA), and [HN thread](https://news.ycombinator.com/item?id=40911637).
	* In 2024, the core developers behind [mamba](https://mamba.readthedocs.io/en/latest/index.html) have also started working on [uv](https://astral.sh/blog/uv) a new Python packager written in Rust. Per the [Larry Du article](https://dublog.net/blog/so-many-python-package-managers/) above, "uv is by far the most promising package management tool in the Python ecosystem as of the writing of this post. This project actually aims to be a drop-in replacement for pip on top of being a Cargo for Python. The API is currently in no ways stable (as of 2024), but the benchmarks are incredibly promsing. Most notably, the development is backed by Astral.sh, a company formed by Charlie Marsh and the creators of the ruff linter, a widely beloved tool that virtually supplanted all incumbants overnight when it was released in 2022."
