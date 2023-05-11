
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
- Dependencies
  - sklearn
  - transfromers
  - datasets
  - torch
  - textpruner  
  - evaluate
  - matplotlib
  - 
Use the given notebook to download and preprocess the sst2 evaluation dataset from huggingface datasets library
Initialize the Roberta Large model from huggingface finetuned on SST2
We then run multiple iteration of pruning using textpruner with varying FFN dim size, number of heads and plot the accuracies in each setting

# Running Knowledge Distillation
- Dependencies
  - sklearn
  - transfromers
  - datasets
  - torch
  - textbrewer  
  - evaluate
 
 Use the given notebook to download and preprocess the sst2 dataset from huggingface datasets library
 The notebook goes on to initialize a student and teacher model using the RobertaConfig from transformers
 We then use the textbrewer library to specify loss function, intermmediate losses and train the student model
 At the end we summarize the model size and compute accuracies for student and teacher 
# Running Quantization

- Dependencies
    - transformers 
    - numpy 
    - pandas 
    - nlp 
    - matplotlib 
    - torch
    - nltk 
    - pytorch_lightning
    - math 
    - os 
    - torchmatrics 

There are two ways to run and compare the affects of 8-bit integer quantization.

## First Option - Download ipynb and raw directory into Colab

Download the Before and After ipynb files and open them in colab.
Next download the raw directory contents and place them in the local repository in Google Colab.
Then just run all cells. After both files finish running, you can compare their results.

Your Colab directory should look something like this:

![Screenshot of how Google Colab directory should look like.](https://github.com/ab5181/hpc-repo/blob/main/images/Example%20Google%20Colab%20Setup.jpg)


## Second Option - Install all necessary packages and Run py files

Download the regular and qunantize py files. Make sure to install the following:

- !pip install transformers numpy pandas nlp matplotlib torch
- !pip install nltk pytorch_lightning math os torchmatrics
- !pip install pytorch-lightning nlp

Also make sure to have a ./raw directory in the same location where you put your two py files.

If you are on IDE, just run the module.

If you are on the terminal, run the command "python regular.py", then after run "python quantize.py"

When both methods finish, compare the results.


# Results:

## Pruning Results:
![FFN Diminesion vs Accuracy](https://github.com/ab5181/hpc-repo/blob/main/images/pruning1.png)
![Attention Heads vs Accuracy](https://github.com/ab5181/hpc-repo/blob/main/images/pruning2.png)
![Attention Heads vs Model Size](https://github.com/ab5181/hpc-repo/blob/main/images/pruning3.png)
![FFN Dimension vs Mode Size](https://github.com/ab5181/hpc-repo/blob/main/images/pruning4.png)
### Observation:
Pruning the attention heads shows that a lot of the heads contain similar information, as pruning them by half didn't drop the performance significantly.
From hyperparameters like attention heads, we see that such elaborate architectures may contain a lot of redundant parameters. 
The decrease in model size w.r.t dffn shows that a significant number of parameters are used on the feed forward layers. But decreasing the dimension by too much drastically effects performance. 

## Knowledge Distillation Results:
![Distilled vs Roberta Large Model metrics](https://github.com/ab5181/hpc-repo/blob/main/images/KD.png)
### Observation:
Despite a drop in accracy of 6%, there is a significant decrease in model size and samples per second for inference
## Quantization Results:



__Tensor Board Graphs/Runtime of regular model__:

![Screenshot of tensor board training loss before quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/train_loss1.jpg)
![Screenshot of tensor board validation loss before quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/val_loss1.jpg)
![Screenshot of runtime before quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/time_before.jpg)


__Tensor Board Graphs/Runtime of quantized model__:

![Screenshot of tensor board training loss after quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/train_loss2.jpg)
![Screenshot of tensor board validation loss after quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/val_loss2.jpg)
![Screenshot of runtime after quantization.](https://github.com/ab5181/hpc-repo/blob/main/images/time_after.jpg)

__Tensor Board Graphs/Runtime of quantized model__:

![Screenshot of table summary comparing the two models.](https://github.com/ab5181/hpc-repo/blob/main/images/quant_table.jpg)

__Tensor Board Result exmample and code result/Runtime of quantized model__:
![Screenshot of example training run.](https://github.com/ab5181/hpc-repo/blob/main/images/Model%20Run.jpg)

![Screenshot of example of Tensor Board result - first half.](https://github.com/ab5181/hpc-repo/blob/main/images/Tensor%20Board%201.jpg)

![Screenshot of example of Tensor Board result - second half.](https://github.com/ab5181/hpc-repo/blob/main/images/Tensor%20Board%202.jpg)



### Observation:

We observe that there is a roughly 5 percent speedup in the run time for a epoch size of 30. The training loss and validation loss increased only by a little bit.

This shows that we have lightened the load of the processing and sped-up the runtime of training and inference, without sacrificing too much loss.

