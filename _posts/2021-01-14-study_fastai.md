# Studying fast.ai MOOCs 

Not being very happy with how academia operates, here is how I intend to take advantage of openly shared AI knowledge, by studying Fast.ai's curriculum in the following order:  

- [Computational Linear Algebra](https://github.com/fastai/numerical-linear-algebra) _"This course is focused on the question: How do we do matrix computations with acceptable speed and acceptable accuracy?"_  
- [Introduction to Machine Learning for Coders](https://course18.fast.ai/ml.html) _"Learn the most important machine learning models, including how to create them yourself from scratch, as well as key skills in data preparation, model validation, and building data products."_  
- [A Code-First Introduction to Natural Language Processing](https://github.com/fastai/course-nlp) _"The course teaches a blend of traditional NLP topics (including regex, SVD, naive bayes, tokenization) and recent neural network approaches (including RNNs, seq2seq, attention, and the transformer architecture), as well as addressing urgent ethical issues, such as bias and disinformation."_  
- [Practical Deep Learning for Coders](https://course.fast.ai/) The title is self explanatory. ([Lesson notes](https://forums.fast.ai/t/deep-learning-lesson-1-notes/27748))  
- [Deep Learning from the Foundations](https://course.fast.ai/part2.html) _"[This course] takes you all the way from the foundations of implementing matrix multiplication and back-propagation, through to high performance mixed-precision training,"_  
- [fastai v2 daily walk-thrus](https://forums.fast.ai/t/fastai-v2-daily-code-walk-thrus/53839) _"These walk-thrus are designed to help early adopters get up to speed on the pre-release (and incomplete) library, especially for people who are interested in contributing to development."_  
[Tips and tricks by Jeremy Howard](https://forums.fast.ai/t/things-jeremy-says-to-do/36682) mentioned in the 14 lessons in total, comprising Deep Learning for Coders (v1) and Deep Learning from the Foundations (v2).  

Complementing the above fast.ai courses  
- [A walk with fastai2](https://github.com/muellerzr/Practical-Deep-Learning-for-Coders-2.0) study group. This course will run from January 15th until May and will be live-streamed on YouTube. Each lecture will be between an hour to an hour and 15 minutes, followed by an hour to work on projects related to the course.  
- [The fastai book (draft)](https://github.com/fastai/fastbook) An introduction to deep learning, fastai, and PyTorch  
- [MIT 6.S191 Introduction to Deep Learning](http://introtodeeplearning.com/) MIT's introductory course on deep learning methods with applications to computer vision, natural language processing, biology, and more  

---

## How to contribute to the library development: 
- [Fork](https://help.github.com/en/articles/fork-a-repo) the repository you want to contribute code to e.g. [fastai](https://github.com/fastai/fastai) (Python3) or the more recent [harebrain](https://github.com/fastai/harebrain) (Swift). Clone the forked repository and change your current working directory to it e.g. `cd ~/fastai`. 
- [Configure a remote for this fork](https://help.github.com/en/articles/configuring-a-remote-for-a-fork), in this case 
```bash 
git remote add upstream https://github.com/fastai/fastai.git
``` 
- Make sure to [sync the fork](https://help.github.com/en/articles/syncing-a-fork) before starting to work on contributions. In my case, I just added a simplistic daily job in a shell script 
```bash 
#!/usr/bin/env zsh  
cd ~/fastai; git pull; git fetch -p upstream; 
git checkout master; git merge upstream/master; 
git push; cd # Update fastai
``` 
I then set a cron job as follows: `crontab -e` launches a terminal editor window. In there, I wrote `@daily /path/to/my_shell_script.sh` and saved it. Should I choose to contribute to the repository later in the day, I can always run `git pull` to ensure my copy is synced.  

- Send a [pull request](https://help.github.com/en/articles/about-pull-requests)  
- [How to contribute to fastai](https://forums.fast.ai/t/how-to-contribute-to-fastai/37828) is a useful, continuously updated summary on how to start and areas you can contribute to.  
- [How to contribute to fastai v2](https://dev.fast.ai/)   

## Jupyter notebook for Literate Programming

Using a web browser of choice and [Jupyter Notebooks](https://jupyter.org/install.html) has proven to be a very productive setup for me. 
JupyterLab runs remotely too, with little preparation as it seems. Start by connecting to your remote server over SSH 
`ssh -Y user@your-server`. The `-Y` flag (optional) enables X11 forwarding, i.e. you can launch a graphical window from your remote server. Try to use a screen multiplexer (tmux or screen) if you want to use the remote terminal later, by typing `screen -S your-session-name`. Then, launch Jupyter as follows: 
```bash
jupyter lab --no-browser --port=8889
```
Jupyter is instructed to use port 8889 and not open a browser window. Next, you need to link the server port to your local machine's localhost
```bash
ssh -N -f -L localhost:8888:localhost:8889 username@your-server
```
You will see the message `The Jupyter Notebook is running at: http://localhost:8889/?token=[long alphanumeric string]`. Launch a browser on your local machine and direct it to `localhost:8888`. If you are prompted to enter a token, copy and paste the token from the message above ([reference](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook)).   

Fast.ai recently released [nbdev](https://www.fast.ai/2019/12/02/nbdev/), for creating complete Python packages in Jupyter notebooks. So all in all, JupyterLab (or Jupyter Notebook) offer a complete solution for Literate Programming <sup>[1](#litprog)</sup>.   

---
<a name="litprog">1</a>: In Literate Programming, a computer program is given an explanation of its logic in a natural language, such as English, interspersed with snippets of macros and traditional source code, from which compilable source code can be generated [[Knuth, 1984](https://doi.org/10.1093%2Fcomjnl%2F27.2.97)].

