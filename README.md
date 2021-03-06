# Problem Description
In task 1, we are given a partial conversation, and we are given 100 candidate next sentences. We need to select the correct one among the 100 candidates.

The description of dataset is on the wiki page.



# About the model
For now, I've implemented the baseline model from this paper:"The ubuntu dialogue corpus: A large dataset for research in unstructured multi-turn dialogue systems".

The model was trained on aws using p2.xlarge instance and each epoch took around 20 mins.

# Set up

Clone the repo, go to the repo folder, setup the virtual environment, and install the required packages:

```
$ cd path_to_this folder
$ virtualenv -p python3 venv
$ source venv/bin/activate
$ pip3 install -r requirements.txt
```

Please note that to install pytorch, we need separate command. Please look at https://pytorch.org/#pip-install-pytorch for instructions.
If you are Mac user, please use:
`
$ pip3 install torch torchvision
`

Run `$ jupyter notebook` to go over the code.

Please download data from aws s3: https://s3.console.aws.amazon.com/s3/buckets/dstc7-task1/?region=us-east-1&tab=overview
You may need to log in as a member of gamma lab to get access to the s3.
# Performance
The evaluation of models in this task mainly rely on recall.

 “1 in 100 R @ 1” means that if we only have 1 choice, what is the value of recall. Similarly, “1 in 100 recall @ 5" means that if we can choose 5 sentences, what is the value of recall that the correct sentence is among our choices.


Official baseline:

| Dataset           | 1 in 100 R@1 | 1 in 100 R@2 | 1 in 100 R@5 | 1 in 100 R@10 | 1 in 100 R@50
| :---------------: | :-------------: | :--------------------: |:----------: | :---------: | :---------: |
| Ubuntu - Subtask 1 | 8.32% | 13.36% | 24.26% | 35.98% | 80.04% |


Previous Model:

| Dataset           | 1 in 100 R@1 | 1 in 100 R@2 | 1 in 100 R@5 | 1 in 100 R@10 | 1 in 100 R@50
| :---------------: | :-------------: | :--------------------: |:----------: | :---------: | :---------: |
| Ubuntu - Subtask 1 | 8.1% | 14% | 27.5% | 38.1% | 71% |


Improved Model:

| Model           | 1 in 100 R@1 | 1 in 100 R@5 | 1 in 100 R@10 
| :---------------: | :-------------: | :--------------------: |:----------: | 
| Dual encoder model | 5.3% | 18.5% | 27.9% 
| Sequential Matching Network | 18.3% | 27.8% | 39.4% 
| Single-head Basic Model | 21.6% | 32.1% | 47.5% 
| Multi-head Basic Model | 22.5% | 35.2% | 51% 
| Adjusted Multi-head Model | 24.1% | 37.1% | 57.5% 
| Hybrided Multi-head Model | 25.8% | 37.9% | 55.3% 


| Model - test set         | 1 in 100 R@1 | 1 in 100 R@5 | 1 in 100 R@10 
| :---------------: | :-------------: | :--------------------: |:----------: | 
| Sequential Matching Network - test_short | 12.3% | 21.5% | 33.9% 
| Sequential Matching Network - test_long | 19.1% | 29.5% | 41.8% 
| Adjusted Multi-head Model - test_short | 18.6% | 32.5% | 45.4% 
| Adjusted Multi-head Model - test_long | 25.5% | 39.2% | 53.2% 


Improved Model:

| Input           | 1 in 100 R@1 | 1 in 100 R@2 | 1 in 100 R@5 | 1 in 100 R@10 | 1 in 100 R@50
| :---------------: | :-------------: | :--------------------: |:----------: | :---------: | :---------: |
| Ubuntu - Subtask 1 | 56.48% | 71.34% | 89.67% |   |   |



| Model | Input           | 1 in 100 R@1 | 1 in 100 R@2 | 1 in 100 R@5 | 1 in 100 R@10 | 1 in 100 R@50
| :---------------: | :-------------: | :--------------------: |:----------: | :---------: | :---------: |
| Dual-encoder Model | 8.32% | 13.36% | 24.26% | 35.98% | 80.04% |
| Memory Network Model | 12.64% | 19.72% | 31.36% | 42.56% | 88.4% |



| User's current input | 5.3% | 10% | 18.5% | 27.9% | 55.8% |
| responses of user's past inputs | 2.7% | 4.8% | 11.4% | 28.2% | 55.4% |
| User's current input + user's past inputs | 5.3% | 10% | 18.5% | 27.9% | 55.8% |
| User's current input + user's past inputs + responses of user's past inputs | 10.56% | 15.78% | 27.4% | 39.64% | 85.36% |




