# MDDial - Developing Prompting Techniques to achieve Efficient Differential Diagnosis Dialogue System

## Task

Automatic Differential Diagnosis (ADD) aims to develop a system that can diagnose patients via interaction with them. ADD has many benefits, such as simplifying the diagnostic procedure, reducing the cost of collecting information from patients, and assisting a real doctor to make decisions efficiently. Leveraging language models and developing end-to-end systems is essential. Recently, we developed MDDial, the first differential diagnosis dialogue dataset in English based on a well-studied differential diagnosis dataset MDD. Here, the task is to develop a prompting technique to achieve SOTA performance on the MDDial dataset and also develop a small-scale model to achieve the same.

## Example from Dataset

<p align='center'>
<img width="583" alt="MDDial" src="https://user-images.githubusercontent.com/47143544/195224497-bb0dd78b-125b-4f9f-af23-e94b40eb567d.png">
</p>

In MDDial dataset, given data samples are similar as generated dialogue in above figure. You are going to work with the similar data samples given in above examples.

## Steps to Perform a Task

#### Task 1 

1. Get 5 data samples (i.e., 5 dialogues) from MDDial (See the dataset in [`data/`](data) folder.), read them and try to understand the goal of the dataset. Use `test.json` file to get original dialogue. Everyone should select different dialogues from test set (You should coordinate among yourselves).
2. Use the free version of GPT3 and try these 5 dialogues with GPT3.
3. See the predictions of GPT3 and figure out issues that you find from its output. Note: GPT3 will not generate the same dialogue and that is fine. You just need to see if GPT3 can do a proper diagnosis.
4. Create a folder with your name and commit your analysis in the following JSON format (submit JSON file corresponding to each dialogue):

```json
{
   "original_dialogue":[
      {
         "patient":"Recently, I am experiencing Burning sensation behind the breastbone",
         "doctor":"What about Nausea?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"Well not in my knowledge",
         "doctor":"Oh, do you have any Stomach ache?"
      },
      {
         "patient":"Yes, sometimes",
         "doctor":"Ok, this means you might be having Esophagitis."
      }
   ],
   "gpt3_output":[
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      }
   ],
   "issue":"str - describe the issue with GPT3 output here."
}
```

Use this to save your JSON file - `json.dumps(your_json_string, indent=4, ensure_ascii=False)`   

#### Task 2 

1. Now use the examples that you selected in Task 1 and see the issues that you have got.
2. Choose any 2 prompting techniques according to the issue that you want to solve. For example, "Chain of Thought" or "Least-to-Most". You can go and search for literature and choose techniques from them.
3. Commit JSON file in following format for those two prompting techniques that you chose:

```json
{
"technique_1": {
  "explaination": "[2-3] line description"
  "referece_papers": "[List of links]"
}
"technique_2": {
  "explaination": "[2-3] line description"
  "referece_papers": "[List of links]"
}
}
```
4. Now apply those techniques to solve issue in those 5 examples and see improvement.
5. Commit your analysis in the following JSON format (submit JSON file corresponding to each dialogue):

```json
{
   "original_dialogue":[
      {
         "patient":"Recently, I am experiencing Burning sensation behind the breastbone",
         "doctor":"What about Nausea?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"Well not in my knowledge",
         "doctor":"Oh, do you have any Stomach ache?"
      },
      {
         "patient":"Yes, sometimes",
         "doctor":"Ok, this means you might be having Esophagitis."
      }
   ],
   "gpt3_output_with_improvement":[
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      },
      {
         "patient":"No, I never had anything like that.",
         "doctor":"Is it? Then do you experience Acid reflux?"
      }
   ],
   "issue":"str - describe the issue with GPT3 output here.",
   "improvement": "str - describe the improvement with GPT3 output here."
}
```

Use this to save your JSON file - `json.dumps(your_json_string, indent=4, ensure_ascii=False)`   


#### Task 3 (Tentative Deadline - Nov. 13, 2022)

1. We want you to explore prompting techniques that you developed in Task 2 with different models. We want to try below models:

   * GPT-2: https://huggingface.co/gpt2
   * DialoGPT: https://huggingface.co/docs/transformers/model_doc/dialogpt
   
2. Now, you need to use the whole dataset and perform the below experiments:
   
   * Fine-tune the above two models on the training dataset and evaluate on test data.
   * Use the best prompting technique from Task 2 and fine-tune models using that prompting technique. Do evaluation on test data.

3. In Both the above models, we want you to calculate disease level accuracy, meaning if the diagnosis is correct then the dialogue is true positive otherwise false positive.

#### Task 4 (Tentative Deadline - Nov. 27, 2022)

[TBD] this task will some minor analysis.

#### General idea of project work

1. Get 5-6 data samples from MDDial, read them and try to understand the goal of dataset.
2. Now, you need to use Large Language Models (LLMs) such as BART, T5, GPT-3, etc. and try to achieve SOTA on this dataset. We will release some baseline results, however, you need to develop efficient prompting techniques to improve the results on this dataset.
3. You need to develop prompting techniques to synthesis similar samples as MDDial and use them for training.
4. You need to achieve almost similar results as step (2) using smaller model and synthesized dataset.

## Literature to Read

1. [Chain of Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)
2. [Least-to-Most Prompting Enables Complex Reasoning in Large Language Models](https://arxiv.org/abs/2205.10625)
3. [DialoGPT: Large-Scale Generative Pre-training for Conversational Response Generation](https://arxiv.org/abs/1911.00536)


## Data

See the MDDial dataset in [`data/`](data) folder.

#### Statistics of MDDial Dataset

| Statistic | Train | Test |
| --- | --- | --- |
| Total Dialogues | 1725 | 237 |
| Avg. turns per dialogue | 5.8 | 5.9 |
| Max. turns in a dialogue | 16 | 13 |
| Min. turns in a dialogue | 1 | 1 |
| Avg. words per dialogue | 53.5 | 55.4 |
| Avg. words per patient utterance | 5.6 | 5.6 |
| Avg. words per doctor utterance | 6.7 | 6.6 |
