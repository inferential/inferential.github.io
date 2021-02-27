# JupyterLab + SSH

Recently, my trusty well-used ThinkPad X250 decided that running quick TensorFlow experiments on it (using the CPU) was a bit much for it. After a motherboard failure, I had to revert to an older computer.  
I have access to an Azure VM, thus I didn't need to set up Google Colab, Gradient or similar services. So I wondered, can I use _JupyterLab_ remotely? If this was possible, I could use literate programming both for data science work and software engineering in Python using [nbdev](https://nbdev.fast.ai/) and [fastcore](https://fastcore.fast.ai/).  
It turns out it is certainly possible, and a very effective way of writing software as well as analysing and visualising data. All one needs to do is:  

0. Connect to your remote server over SSH `ssh -X your_username@ip.add.of.srv`
1. On the remote server, set up a Python virtual environment using [virtualenv](https://virtualenv.pypa.io/en/latest/) or another virtual environment tool of choice.  I find _virtualenv_ easier to use and more lightweight.  
2. Once _virtualenv_ is installed, create a new virtual environment on your remote machine and activate it e.g. `mkdir ~/.virtualenv; cd ~/.virtualenv; virtualenv experiment; source experiment/bin/activate`. You should now see on your terminal, that you're in that environment `(experiment) your_username:~/.virtualenv $ `  
3. Since you are now using the new Python environment `experiment`, you can install [JupyterLab](https://jupyter.org/install.html) with `pip install --no-cache-dir jupyterlab`. The `--no-cache-dir` option skips caching the package before installing it, keeping your `~/.cache` clean.  
4. You can now launch _JupyterLab_ on your remote machine as follows `jupyter-lab --no-browser --port=8080`. This will start the _JupyterLab_ server, without launching a browser, and the server will be listening on port 8080. Once the _JupyterLab_ server is up and running, you will see a message along the lines of 
```bash 
To access the server, open this file in a browser:
        file:///home/your_username/.local/share/jupyter/runtime/jpserver-8326-open.html
    Or copy and paste one of these URLs:
        http://localhost:8080/lab?token=d65f733947445fee36cfd013bfbb53b87c38c30729abc4a6
     or http://127.0.0.1:8080/lab?token=d65f733947445fee36cfd013bfbb53b87c38c30729abc4a6
``` 
5. Aside from your current remote server connection, open a new terminal window and SSH into your remote machine `ssh -L 8080:localhost:8080 your_username@ip.add.of.srv`. 
6. On your local machine, launch a web browser and paste the address that _JupyterLab_ server returned e.g. `http://localhost:8080/lab?token=d65f733947445fee36cfd013bfbb53b87c38c30729abc4a6`. You are now connected to your remote machine's _JupyterLab_ server instance, using your local machine's web browser as the client.  
Happy coding! :) 
