# Chatbot-That-Cares
The motivation for this project is to build an empathetic chatbot which has the competence to listen to people, understand the user’s state and respond empathetically.
It can be considered as a platform where people can
express all their sadness, concerns, issues, worries and
even happy moments. The chatbot can act as a friend,
analyse the mood of the user and respond with empathy.

# How did we do this?

1. The pre-trained GPT2 model from huggingface is used
and then fine tuned on large-scale multi-turn empathetic
dialogue dataset.
2. Data is in a one-to-one conversational setting where the
speaker talks about a situation and the listener
understands the emotion and responds empathetically.
3. The original GPT2 model is trained with a single input
sequence. For the current use case, the dialogues from
each speaker along with the history are concatenated.
4. Training is based on GPT2LMHeadModel architecture
5. The model is fine-tuned with AdamW optimizer with a
learning rate of 5e-4.

# Evaluation strategy
▶ No standard metric for measuring the empathetic capability

▶ Evaluation is done by letting users subjectively rate their experience

▶ Check the survey.pdf

# Survey and Results
▶ We compared the outputs of the original GPT2 and finetuned GPT2 by
surveying 50 people and computing the average score.

▶ People are given a situation like an incident and are asked to convey their
emotions with the chatbot.

▶ The user then analyzes the responses from the chatbot and rate it accordingly.

▶ The average score for each metric for original GPT2 model and GPT2 model
fine-tuned on ED dataset is shown below

| Metric  | GPT 2 | Fine-tuned GPT 2 |
| ------------- | ------------- | ------------- |
| Fluency  | 3.7  | 3.74 |
| Diaglogue Quality  | 1.5  | 3.48 |
| Human-likeness  | 1.54  | 3.76 |

# How to run the code

1. Downloading the data
-- Download the train and valid csv files from the ED dataset homepage https://paperswithcode.com/dataset/empatheticdialogues

2. Preprocessing the csv files
-- Run the script
python data/clean_csv.py --data_path '<path for the files>'
-- this script outputs a cleaned version of train and valid csv files

3. Tokenization and saving the data as pickle files
-- Run the script
python src/tokenize_data.py --data_path '<path for the cleaned csv files>' --prefix '<train/valid>' --model '<gpt2 model need to be specified>'
-- This script provides the .pckle files for train and valid dialouges token ids

4. Check the arguments for training in config.yaml

5. Run the training file to start training
-- Run the script
python trainer.py
-- Best model will be saved in models directory, logger will be saved in experiments folder and if wandb logging is enabled, wandb logs the metrics

6. Chcek the arguments for inference in inference_config.yaml and specify the checkpoint

7. Run the inference code
--Run the script
python inference.py
-- You can start chatting with the chatbot

