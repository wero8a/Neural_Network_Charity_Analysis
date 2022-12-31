# Neural_Network_Charity_Analysis
![image](https://user-images.githubusercontent.com/110706169/210124991-2783cf8d-aa94-474c-82f1-688a68a2ac3b.png)

## Overview
 The purpose of this analysis is to help Beks create a binary classifier that is capable of predicting whether applicants will be successful if funded by Alphabet Soup, a multi-billion dollar business. Beks received a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years. Within this dataset are a number of columns that capture metadata about each organization, such as the following:

  * EIN and NAME—Identification columns
  * APPLICATION_TYPE—Alphabet Soup application type 
  * AFFILIATION—Affiliated sector of industry
  * CLASSIFICATION—Government organization classification
  * USE_CASE—Use case for funding
  * ORGANIZATION—Organization type
  * STATUS—Active status
  * INCOME_AMT—Income classification
  * SPECIAL_CONSIDERATIONS—Special consideration for application
  * ASK_AMT—Funding amount requested
  * IS_SUCCESSFUL—Was the money used effectively
## Results
* ### Data Preprocessing:
  - What variable(s) are considered the target(s) for your model? 
     
    ![image](https://user-images.githubusercontent.com/110706169/210122636-2d495d31-54ff-487d-836b-4158eab1c615.png)
     
     Our target variable in this analysis will be the **IS_SUCCESSFUL** column because if we can predict this value to be either 0 or 1 accurately, it can        help prevent Alphabet Soup from funding organizations that are likely to not succeed.

  - What variable(s) are considered to be the features for your model?
    
     ![image](https://user-images.githubusercontent.com/110706169/210123119-c086d7bd-6cb0-4fe2-bb29-a49b26c00977.png)
     

  - What variable(s) are neither targets nor features, and should be removed from the input data? 
    
    ![image](https://user-images.githubusercontent.com/110706169/210123185-721edc58-4cb0-45de-8a66-8686d41d6465.png)

* ### Compiling, Training, and Evaluating the Model:
 
  - How many neurons, layers, and activation functions did you select for your neural network model, and why? 
    
     ![image](https://user-images.githubusercontent.com/110706169/210123298-54cb17f0-78a8-4eeb-912a-c755a333781b.png)
    
    The number of nuerons, layers, and activation functions selected were derived from many iterations of multiple different models and feature  optimizations. In this case, **there are 128 neurons in layer 1, 64 neurons in layer 2, and 32 neurons in layer 3; all three layers with the Relu activation function.**
    
  - Were you able to achieve the target model performance? 
    
    ![image](https://user-images.githubusercontent.com/110706169/210124612-9942755d-8886-4900-b3e3-51eb20dd396b.png)

    Yes, with **Loss: 69%** and  **Accuracy: 78%**
    
  - What steps did you take to try and increase model performance?
    
     First, I checked how important some of the data in the columns were for the model.
    
    ![image](https://user-images.githubusercontent.com/110706169/210123513-05417667-3dc0-49ba-abd2-bc3ab34763b3.png)
    ![image](https://user-images.githubusercontent.com/110706169/210123551-606196e7-7739-4b3b-a775-bd2dbe90b55a.png)
     
     I compare **SPECIAL_CONSIDERATIONS** against **IS_SUCCESSFUL** column. Since there is a non-linear relation and the values are heavily skewed, I decided to drop this column. 

    ![image](https://user-images.githubusercontent.com/110706169/210124150-b62a3af2-a522-4545-8a7c-79d8894dc772.png)
    
    The **STATUS** column was dropped becuase it does not help the model.
    
    In order to improve the performance of the model I added a bin feature derived from the **ASK_AMT** column.
    
    ![image](https://user-images.githubusercontent.com/110706169/210124291-c72e1c9f-8ea3-4780-b1fd-ef81a400b4dc.png)
    
    After **ASK_AMT_BINS** column is created the **ASK_AMT** column must be removed from the dataframe. After binning the ask amount, the model was up to 70~71% accuracy, but the model_loss was over 1. I used the following tensorflow layer parameter: 
    
    ![image](https://user-images.githubusercontent.com/110706169/210124464-dca01532-44c2-4824-98e3-6ea3fe7f43df.png)

    The purpose of a kernel regularizer is to prevent overfitting by adding a penalty to the model's loss function for using large weight values in the kernels of the model's layers.
    
    ![image](https://user-images.githubusercontent.com/110706169/210124720-0ee97815-f962-4fdb-8eb7-27cd33f4acbe.png)
    
    In order to continue improving the model, the **NAME** column was binned because it provides valuable information. There are repeat organizations that recieved funding from Alphabet Soup hundreds of times. Once binned we reduced the unique values from 19k down to 355. Big enough to help our model and small enough to not require too much computing power. 

## Summary 

An accuracy of 78% was reached, and in order to go further with this model we would need more relevant metadata. I would recommend trying to replicate this model with the scikit-learn library using RandomForestClassifiers because they are great for categorical data that is noisy or has non-linear relationships.
  
