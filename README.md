# SarcasmDetection - CS 7650 NLP Final Project
## Directory Structure
- utils
    - dataloader.py (data parser to use torchtext for models)
    - gather_data.py [deprecated]
    - transform_dataset.py (converts and preprocesses raw dataset into model-ready format
    - transform_response_only.py (same as transform_dataset.py but only uses response, no context)
- baselines.py (TF-IDF based BoW models)
- create_submission.sh (zip script for competition ready input)
- download_prepare_data.sh (script to download competition data, preprocess + transform and place in right spots)
- generate_stats.py (script to output relevant summary statistics for data)
- lstm_model.py (lstm model for sarcasm [deprecated])
- test_model.py (takes saved pytorch model and evaluates for competition [deprecated])
- simple_bert.py (trains bert-based model)
- requirements.txt (python package requirements)

## Quickstart
To install python3.7 requirements:  

    pip install -r requirements.txt

First download the competition data & format it for our models  

    ./download_prepare_data.sh

Then train and generate predictions using one of the following models:  
### baseline tfidf
    python baselines.py

### bert
    python simple_bert.py --data_source twitter --model bert --data_dir bert_data --save_model simple_bert.pt
    python simple_bert.py --data_source twitter --model bert --data_dir bert_data --predict True --pretrained_model simple_bert.pt

### roberta
    python simple_bert.py --data_source twitter --model roberta --data_dir roberta_data --save_model simple_roberta.pt
    python simple_bert.py --data_source twitter --model roberta --data_dir roberta_data --predict True --pretrained_model simple_roberta.pt

### xlnet
    python simple_bert.py --data_source twitter --model xlnet --data_dir xlnet_data --save_model simple_xlnet.pt
    python simple_bert.py --data_source twitter --model xlnet --data_dir xlnet_data --predict True --pretrained_model simple_xlnet.pt

Generating predictions will generate a file like *twitter_answer.txt*, convert to .zip by:  

    ./create_submission.sh


Performing error analysis can be done with the "--confusion True" flag, printing out the confusion matrix and writing to a *twitter_analysis.txt* file, containing a file of "sequence, predicted tag, ground truth tag"
