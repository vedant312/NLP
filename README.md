# NLP
We used a previous model and trying to do changs in it.

Setup
Create a virtual environment with python >= 3.7.

Install the dependency packages in requirements.txt:

pip install -r requirements.txt
If you want to create your own dataset using preprocess.py, you also need to download the en_core_web_sm model for English language support of SpaCy:

python -m spacy download en_core_web_sm

Process the CSV data files:

python preprocess.py

Train a model:

python train.py -mode train -ckpt_dir ckpt -train_set data/train.json -dev_set data/dev.json\
-cpnet_path CPNET_PATH -cpnet_plm_path CPNET_PLM_PATH -cpnet_struc_input -state_verb STATE_VERB_PATH\
-wiki_plm_path WIKI_PLM_PATH -finetune

Predict on test set using a trained model:

python -u train.py -mode test -test_set data/test.json -dummy_test data/dummy-predictions.tsv\
-output predict/prediction.tsv -cpnet_path CPNET_PATH -cpnet_plm_path CPNET_PLM_PATH\
-cpnet_struc_input -state_verb STATE_VERB_PATH -wiki_plm_path WIKI_PLM_PATH -restore ckpt/best_checkpoint.pt


Run the evaluation script using the ground-truth labels and your predictions:

python evaluator/evaluator.py -p data/prediction.tsv -a data/answers.tsv --diagnostics data/diagnostic.txt
