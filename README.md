# Capstone Project - Predicting Pet Adoption Speed
#### Jordan Weiss [GitHub](https://github.com/weisja4/pet_adoption_capstone)

### Table of Contents
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Data Dictionary](#Data-Dictionary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Resources](#Resources)



## Problem Statement:
Around the world millions of dogs and cats sit in shelters, waiting for their forever-homes, which many will never find. Over the course of history, our pets become reliant on humans for food, shelter, and companionship. As a result, dogs and cats need humans to adopt them from shelters and bring them into their homes. The demand for shelter animals varies widely based on the characteristics of each animal, as well as the website post for their adoption. 

We will seek to use data from PetFinder (Malaysia) describing each pet, as well as the metadata from their Petfinder posts to predict the speed at which pets get adopted. Specifically, we will make a classifier model that will predict the speed at which the pet is adopted. We will judge our success on the accuracy of our predictions. Additionally, we will set aside a portion of our data as a validation set to confirm our model’s ability to estimate new entries.

By predicting the speed at which pets get adopted, we hope to gain insight into actionable measures we can take to increase the rate and overall number of adoptions. 
   
  

## Executive Summary

__Data Source:__ https://www.kaggle.com/c/petfinder-adoption-prediction/data  

We were fortunate to have an existing dataset from Kaggle that contains, along with other information, detailed listings on approximately 15,000 cats and dogs that were listed on the PetFinder website in Malaysia, including the speed category of their adoption. From the "Data Source" listed above we used the set labled 'Train' for our analysis. The initial data was read into the "Splitting Data" notebook and divided into a training and test set as well as a holdout set, which was segmented out of the data to be revisited later for validation. 

Once we have our data read-in, we start with clean up and preliminary analysis. From the outset, we see the data is very clean, but has information we do not want to include, like resucer_id, state (in Malaysia) etc. that needed to be dropped. The largest change we made was to exclude listings of more than 3 pets as these were often entire litters of puppies/kittens rather than individual pets or bonded pairs/triples.

With the cleaned and split data in hand, scaled the data (standard scalar) and began our catagorical modeling. 

After categorical modeling we did regression analysis to attempt to estimate the actual time pets are in the shelter (rather than a speed category). These results were not very stong and not instructive. Though the excercize was worthwhile, there is not much predictive ability in the regression models. 

It is important to note that many of the categories that appear numerical are actually categorical, like breed and color. Those features were indluded using one-hot-encoding for modeling. 

__Modeling and Analysis__
We did our modeling from more simple to more complex utilizing the following models (in order we tested):
K-Nearest Neighbors  
Decision Tree   
Boot-Strapped Bagged Classifier
Random Forest  
Extra Trees  
Neural Network  
Each model was tuned to get to the best estimations for adoption speed. We ultimately selected the Random Forest model as it provided the best accuracy score on our test data.

## Data Dictionary
https://www.kaggle.com/c/petfinder-adoption-prediction/data
![Data Dictionary](https://www.kaggle.com/c/petfinder-adoption-prediction/data "Title")
Data Fields

#### Target  
 AdoptionSpeed - Categorical speed of adoption. Lower is faster. TARGET.
      >0: Adopted the day the pet was listed
      >1: Adopted after the first day, but within the first week of listing
      >2: Adopted after the first week, but within the first month of listing
      >3: Adopted between 31-90 days after listing
      >4: Adopted after 100 days, or never adopted    
      
#### Other Features
- __PetID:__ - Unique hash ID of pet profile - Dropped
- __Type:__ Type of animal (1 = Dog, 2 = Cat) - Categorical
- __Name:__ Name of pet (Empty if not named) - Dropped
- __Age:__ Age of pet when listed, in months
- __Breed1:__ Primary breed of pet (Refer to BreedLabels dictionary) - Categorical
- __Breed2:__ Secondary breed of pet, if pet is of mixed breed (Refer to BreedLabels dictionary) - Categorical
- __Gender:__ Gender of pet (1 = Male, 2 = Female, 3 = Mixed, if profile represents group of pets) - Categorical 
- __Color1:__ Color 1 of pet (Refer to ColorLabels dictionary) - Categorical
- __Color2:__ Color 2 of pet (Refer to ColorLabels dictionary) - Categorical
- __Color3:__ Color 3 of pet (Refer to ColorLabels dictionary) - Categorical
- __MaturitySize:__ Size at maturity (1 = Small, 2 = Medium, 3 = Large, 4 = Extra Large, 0 = Unknown - Categorical
__FurLength:__ Fur length (1 = Short, 2 = Medium, 3 = Long, 0 = Not Specified) - Categorical
__Vaccinated:__ Pet has been vaccinated (1 = Yes, 2 = No, 3 = Not Sure) - Categorical
__Dewormed:__ Pet has been dewormed (1 = Yes, 2 = No, 3 = Not Sure) - Categorical
__Sterilized:__ Pet has been spayed / neutered (1 = Yes, 2 = No, 3 = Not Sure) - Categorical
__Health:__ Health Condition (1 = Healthy, 2 = Minor Injury, 3 = Serious Injury, 0 = Not Specified) - Categorical
__Quantity:__ Number of pets represented in profile - Numerical 
__Fee:__ Adoption fee (0 = Free) - Numerical (Note: Malaysian Currency)
__State:__ State location in Malaysia (Refer to StateLabels dictionary) - Dropped
__RescuerID:__ Unique hash ID of rescuer - Dropped
__VideoAmt:__ Total uploaded videos for this pet - Numerical
__PhotoAmt:__ Total uploaded photos for this pet - Numerical
__Description:__ Profile write-up for this pet. The primary language is English, with some in Malay or Chinese. - Dropped



## Conclusions-and-Recommendations
Most of our models performed well in the range of 35%+ accuracy. We ultimately selected the Random Forest model as it produced the best results, which were about 11.5 percentage points above the baseline accuracy.  

We are able to conclude from our work that there are key factors that affect the speed at which dogs and cats are adopted. Those factors include age, spay/neuter status, breed and the number of photos available. Being able to more accurately predict the speed at which pets are adopted will allow us to better allocate resources to get the most pets into forever homes. 

Other Recommendations:
Include multiple pictures of the pet

Even if the breed is unknown or mixed, it is best to take a guess and include a breed rather than ‘mixed’

Spay/Neutering the pet helps in adoption, and helps keep the population down for the future

Focusing on pets identified as being more difficult to home may increase their likelihood of finding a forever home. 


## Resources
DATA SOURCE -                                              https://www.kaggle.com/c/petfinder-adoption-prediction/data
Background on Multiclass Classification - https://www.linkedin.com/pulse/kaggle-competition-multi-class-classification-image-alexandra/
Confusion Matrix for MCC - https://stackoverflow.com/questions/53886370/multi-class-multi-label-confusion-matrix-with-sklearn
Interpretation of Random Forest - https://towardsdatascience.com/interpreting-random-forest-and-other-black-box-models-like-xgboost-80f9cc4a3c38
Interpretation of Random Forest with Sklearn -             https://scikit-learn.org/stable/auto_examples/inspection/plot_permutation_importance.html
Model Saving/Loading , Pickling -                                                         https://machinelearningmastery.com/save-load-machine-learning-models-python-scikit-learn/
Feature Alignment for Testing - https://stackoverflow.com/questions/44266677/machine-learning-test-set-with-fewer-features-than-the-train-set



