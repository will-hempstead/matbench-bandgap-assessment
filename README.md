# matbench-bandgap-assessment

Assessment from 'Data Analytics for Chemists' module taken as part of 'Digital Chemistry' MSc at Imperial College London. 
Our task is to explore the experimental bandgap dataset from matbench (https://matbench.materialsproject.org/Leaderboards%20Per-Task/matbench_v0.1_matbench_expt_gap/) and try out some different approaches to predict bandgap.

feature_engineering.ipynb: Feature engineering using sklearn permutation importance to rank features by effect on model performance. I've also made a model on the single most important feature to see how it performs - mae = 0.82 VS mae(all features) = 0.43. 

XGBoost_model.ipynb: Simple xgboost model trained on all features. Hyperparameter tuning and feature reduction using built in xgboost feature importance function to narrow down the smallest featureset we can use without decreasing model performance. 

neural_net.ipynb: Initial exploration of neural network trained on 34 most important features as assigned above. Workflow taken from workshop by Dr Alex Ganose. I train the model and assess performance by calculating mae = 0.47. Further work needed to play with model parameters and try to improve performance. 

transfer_learning.ipynb: An attempt to bring in a much larger DFT bandgap dataset to train a neural network, followed by finetuning on the experimental dataset by retraining with a lower training rate and mostly frozen network. So far worse mae than nn trained just on experimental bandgap - more work needed. Ideas - need to investigate dft dataset and do some feature engineering on this - possibly removing irrelevent materials eg organics? Also investigate fine-tuning step eg learning rate.

two_step.ipynb: A two-stage approach to address zero-inflation of dataset. Classifier classifies if y_pred is zero ('0') or greater than zero ('1'), and then regressor predicts value if output is '1'. To make the model more deployable I have bundled the two models into a class, and used cross validation to assess peformance. So far most meaningful improvement in performance vs vanilla xgboost, mae = 0.37 VS mae = 0.43.
