# Sentiment Analysis Suite
This repo contains a suite of python script to train your own ensemble model for sentiment analysis. The ensemble model is made up of a SVM with Naive Bayes features (nbsvm), a RNN with LSTM gates(lstm), a RNN with GRU gates and word vector embedding layers(gru), and a Microsoft's Gradient Boosted Tree - LightGBM (lgb).

## Model scripts
### Training
```
python model_train.py --option_arguments
```
Train the 4 individual models using the given training data, saves the model files into the given model folder
#### Data Format
The dataset is a csv file with two columns, label and text. Where label is the sentiment tags.

|label|text|
|---|---|
|-1 |I hate pie!|
|1 |I love pie!|

#### Training Arguments
##### General Arguments

- `--num_classes`: Number of classes in your dataset 
- `--val_split`: Proportion of data to use for validation during training
- `--path_data`: Path to data in csv format (e.g. `/home/data/my_data/training.csv`)
- `--path_embs`: Path to word embedding to be used in the model
- `--directory`: Directory to save model and log files to 
- `--skip_nbsvm`: Do not train the nbsvm model
- `--skip_lstm`: Do not train the lstm model
- `--skip_gru`: Do not train the gru model
- `--skip_lgb`: Do not train the lgb model

##### Model specific arguments
LSTM

- `--emb_size_lstm`: Size of the LSTM embedding layer
- `--epochs_lstm`: Number of max LSTM epochs to train
- `--recurrent_size_lstm`: Size of the recurrent layer for LSTM
- `--batch_size_lstm`: training batch size for LSTM
- `--max_feat_lstm`: Max number of word features for LSTM

GRU

- `--emb_size_gru`: Size of the GRU embedding layer
- `--epochs_gru`: Number of max GRU epochs to train
- `--recurrent_size_gru`: Size of the recurrent layer for GRU
- `--batch_size_gru`: training batch size for GRU
- `--max_feat_gru`: Max number of word features for GRU

### Prediction
```
python model_predict.py <file_path(type: csv)> <x_col_name> <weight_path> <out_file_path>
```
Use the trained models to predict the given dataset, and save the results as csv
#### Data Format
|text|
|---|
|I dislike pie.|

#### Prediction arguments
`file_path`: path to data in csv format (e.g. `/home/data/my_data/to_predict.csv`)
`x_col_name`: text columns to predict (e.g. `text` or `user_message`)
`weight_path`: where the models are saved (`directory` of training script)
`out_file_path`: where to store the prediction result