# Hadronic Tau identification 
### Comparing machine learning models for the identification of hadronically decaying tau leptons in ATLAS Open Data.

This project was completed as part of the IRIS Big Data ATLAS Project 2026. The aim was to distinguish genuine hadronic tau decays from QCD jets and other background processes using publicly available Monte Carlo simulation data.

##### ML models we will compare:
  * Decision Tree
  * Random forest
  * XGBoost
  * Neural Network
# How the models work
#### 1) Reads the root files of the CERN Monte Carlo simulation data
#### 2) Extract kinematic variables for tau and lepton candidates
#### 3) Construct engineered features describing tau-lepton relationships
#### 4) Train the model using Monte Carlo truth labels
#### 5) Generate ROC curves and calculate AUC scores



# Engineered features
### Only kinematic variables are available to the public, limiting our accuracy. Real ATLAS analysis on the other hand, also uses detector-response features such as shower-shape + topocluster-based variables. As a result, several engineered features were constructed from the available kinematic variables. The most informative was the angular separation between the tau candidate and accompanying lepton:

ΔR = √[(Δη)² + (Δφ)²]

### Feature importance studies consistently identified ΔR as one of the strongest discriminating variables across all tree-based models.



# Feature importance (included in all models bar Neural Network)
<img width="400" height="300" alt="Dtree featureimportance" src="https://github.com/user-attachments/assets/f72955d5-f85d-4cb6-b621-d216de3577a1" />

Decision tree

<img width="400" height="300" alt="Randforest featimportance" src="https://github.com/user-attachments/assets/08841026-d3c7-4d68-8787-e78b958736b9" />

Random Forest

<img width="400" height="300" alt="XGB featimp" src="https://github.com/user-attachments/assets/173c4946-c13a-49e1-9d41-5ebc42fb14e6" />


XGBoost

### Across all models, ΔR, E/pt, tau pt and lep pt were among the most important features, highlighting the importance of including lepton features and engineered variables. Despite using different machine-learning architectures, all tree-based models identified similar variables as the most important discriminators. This suggests that the learned behaviour is driven by genuine physical information rather than model-specific artefacts.

# 3d Loss surface
### Present in the Neural network model. Represents a geometric, visual representation of the loss function.

<img width="400" height="340" alt="NN Loss surface" src="https://github.com/user-attachments/assets/d5a92f27-d378-4b5c-9082-a24a4a09ad5c" />

#### The model converged within ~5 epochs with train and val loss remaining tightly coupled, indicating no overfitting
#### The flat region after epoch 5 shows the model reached a stable minimum — early stopping then prevented unnecessary further training



# Results
## The models were evaluated using Receiver Operating Characteristic (ROC) curves and the Area Under the Curve (AUC) metric, which measures the ability of a classifier to distinguish signal from background over a range of classification thresholds.
### From best to worst the most accurate models were:
  * Neural Network
  * XGBoost
  * Random Forest
  * Decision tree
### This is to be expected. The complexity of the models doesn't seem to be the limiting factor but rather the features at our disposal. 
#### All models scored similarly, ~0.7
<img width="400" height="300" alt="decision tree final final" src="https://github.com/user-attachments/assets/bc3948ca-979a-4831-a47d-1f5b522b3166" />
<img width="400" height="300" alt="random forest roc curve" src="https://github.com/user-attachments/assets/d9ee7e94-4740-4ab0-9a0b-63c255c7a8aa" />
<img width="400" height="300" alt="xgboost finalfinal" src="https://github.com/user-attachments/assets/f158f4f1-f855-4bb5-8183-ada7af91105e" />
<img width="400" height="300" alt="Neural network 3" src="https://github.com/user-attachments/assets/6376b3f0-a91b-4d39-93cb-720f9d45ea2c" />

##### The results suggest that model complexity was not the primary limitation on performance. The relatively modest AUC scores are more likely a consequence of the restricted feature set available in the public dataset.

##### Professional ATLAS tau-identification algorithms utilise additional detector-response information, including calorimeter shower-shape and topocluster variables, which are not publicly available. Incorporating such information would likely improve classification performance significantly.

## Extra Information
#### Please note you require the https://opendata.cern.ch/record/15002 from CERN open data.

#### Make sure you change the placeholder 'filepath' to the filepaths of your root files.

