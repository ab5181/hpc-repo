
# Analyzing Model Compression Techniques for Language Models

- Harsha Vardhan (hv2237)

- Alex Brebenel (ab5181)

# Description
This repo contains several programs to test and compare the runtime speeds and accuracy of a model before and after utilizing 3 different compression techniques:
- Pruning
- Knowledge Distillation
- Quantization

We use the RoBERTa-Large model as the starting template and use data models from the the GLUE benchmark. For each respective technique, we perform an analysis and comparison of how the template model and the newly compressed model runs.


# Running Pruning

# Running Knowledge Distillation

# Running Quantization

There are two ways to run and compare the affects of integer quantization.

## First Option - Download ipynb and raw directory into Colab

Download the Before and After ipynb files and open them in colab.
Next download the raw directory contents and place them in the local repository in Google Colab.
Then just run all cells. After both files finish running, you can compare their results.

Your Colab directory should look something like this:

![Screenshot of how Google Colab directory should look like.](https://github.com/ab5181/hpc-repo/blob/main/Example%20Google%20Colab%20Setup.jpg)


## Second Option - Install all necessary packages and Run py files

Download the regular and qunantize py files. Make sure to install the following:

- !pip install transformers numpy pandas nlp matplotlib torch
- !pip install nltk pytorch_lightning math os torchmatrics
- !pip install pytorch-lightning nlp

Also make sure to have a ./raw directory in the same location where you put your two py files.

If you are on IDE, just run the module.

If you are on the terminal, run the command "python regular.py", then after run "python quantize.py"

When both methods finish, compare the results.


# Results

### Pruning Results

### Knowledge Distillation Results

### Quantization Results



