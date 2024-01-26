Role: Natural Language Processing Researcher \
Timeline: September - December 2023 \
Company: ASAPP \ 
Purpose: Finetune a Large Language Model to help customer service agents respond more effectively and increase productivity. \

## Introduction 
For this project, I worked with ASAPP, leveraging AI to support companies in improving customer experience and productivity, delivering automation and human augmentation, allowing individuals and organizations to realize their full potential. My project focused specifically on the question: How can Large Language Models support customer service agents to provide the best responses to customer questions? In order to answer this question, I broke down the task into three different steps: data preprocessing, model training, and model evaluation. I also designed the project to test 3 different hypotheses:
Using a larger model, GPT2-medium, will yield better results than a smaller model, DistilGPT2
Including the "action" tag will improve performance by increasing the context that the model sees. 
Concatenating consecutive agent utterances will not improve performance because it increases context length increasing the probability of the model to generate errors in the output.

## Data Preprocessing
The Action Based Conversation Dataset (ABCD) consists of recorded customer and agent conversations and the alternating utterances that were exchanged during the conversation. The ABCD dataset is organized as a dictionary where the conversation utterances can be accessed by the key "original." The conversation utterances are stored as an array of arrays: [["agent", "hello"],["customer","hi"]]. In order for this text data to be used to finetune a Large Language Model, it first had to be formatted into a .txt file where each conversation is a singular string of utterances. To test our hypothesis, there were two different conditions that we had to account for:
I. Including action tags
II. Concatenating consecutive agent utterances
To account for these different cases, each required its own preprocessing .txt file. Code to perform this preprocessing can be found here.

Model Fine Tuning
After creating the .txt files we finetuned GPT2-medium and DistilGPT2 on the task of causal language modeling using each of the .txt files that were created during the preprocessing step to account for the different hypotheses that we were testing.

Model Evaluation
To evaluate the performance of the model, I compared 1000 GPT generated outputs to the corresponding true agent responses and used BERT to determine the similarity score between the generated output and target response. I performed simple data analysis, normalizing negative BERT scores to 0 and taking the mean across all generates to create an average model performance on this task. In the table below you can see the side-by-side comparison of how the different models performed based on the different data that they were finetuned on.



## Results 
To better understand and contextualize our results, it's important to note that research on an Offline Reinforcement Learning approach to training a model on this task using the ABCD dataset had a BERT score of 0.404 which demonstrates what while our approach to fine tuning GPT doesn't perform at the same level as the state-of-the-art approach, our results are comparable to the Offline RL. Based on the results, our hypothesis were supported:

Using a larger model, GPT2-medium, will yield better results than a smaller model, DistilGPT2
GPT2 out performed DistilGPT2 by achieving a hiring mean BERT score across all combinations of finetuned GPT2 models.

Including the "action" tag will improve performance by increasing the context that the model sees. 
We see that including the action tag in non-concatenated utterances yielded the highest performance compared to the inclusion of the action tag with concatenation. 

Concatenating consecutive agent utterances will not improve performance because it increases context length increasing the probability of the model to generate errors in the output.
As you can see non-concatenated utterances all outperformed the concatenated counterparts demonstrating the negative effects of increased context length. 

## Future Directions
These results demonstrate that Large Language Models can be finetuned for the task of dialogue generation, but that there needs to be a more in-depth investigation into how to improve results. For a future direction, Reinforcement Learning with Human Feedback can be employed to increase the accuracy of outputs. Additionally, it would be valuable to see how different evaluation metrics can be used to determine the accuracy of the models. FAISS is another semantic similarity tool that can be used to evaluate model outputs and offer more insights into the differences between the various finetuning techniques. 

## Acknowledgements 
I would like to acknowledge Paloma Sodhi, my project advisor, Anvita Bhagavathula, the TA associated with this project, and the larger Break Through Tech AI team for this opportunity to work on this project with ASAPP. I would also like to shoutout my teammates: Maria Reccoppa, Lana Saadeddin, Bianca Kim, and Damaris Campos for their contributions to the project. 
