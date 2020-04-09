# Installing RASA

### Method 1: With python pip

    $ pip install rasa
    $ rasa init

The first command installs Rasa Open Source onto your system.
It requires `Python 3.6` or `3.7`.
(You may use `pip3` in place of `pip` if you have python 2 and 3 on your system)



The second command rasa init then creates a sample Rasa project in your current directory.
 This includes some sample training data and the required configuration files to get you started.
 The command also automatically trains your first model using this data and invites you to speak to the trained assistant.


### Method 2: Using virtualenv (Recommended if you have `venv`)

Requirements are python3.6 or 3.7 with `venv` installed (`pip3 install venv`)

    python3 -m venv --system-site-packages ./rasa_venv
    
On Windows:

    .\venv\Scripts\activate

On Linux/Mac:

    source ./venv/bin/activate


### Methd 3: Building from Source

If you want to use the development version of Rasa Open Source, you can get it from GitHub:

    curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
    git clone https://github.com/RasaHQ/rasa.git
    cd rasa
    poetry install


### Method 4: Using Docker (Recommended if you have `docker`)

In the folder where you want to start working on rasa create a file named `Dockerfile` and add the below:

    FROM python:3.7
    RUN python -m pip install rasa 
    CMD /bin/bash

Next, build the docker image by running the command:

    docker build -t rasa .

Then, run the image to get the bash prompt of the rasa install docker container:

    docker run -it --rm rasa

Now you should have the bash prompt of the docker container where you may create python/rasa apps!
You may additionally add `-v $(pwd):/app` to map current directory as `/app` directory on the docker container.

Reference: [Rasa Installation Doc](https://rasa.com/docs/rasa/1.9.5/user-guide/installation/)
