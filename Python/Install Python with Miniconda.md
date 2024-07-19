# Install Python with Miniconda
Miniconda is a program which contains everything you need to run Python, plus a bunch of useful features that will make your life easier!
You can learn more about it in the documents here, or on their [official website](https://docs.anaconda.com/miniconda/).

## Installation Instructions
To install miniconda, log in to the Riviera cluster and run these commands:

```shell
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
```
