# DataImager
Contains the DataImager library to convert datasets into Images to use with Neural Nets

library : DataImager.py
make sure to take a look at the 'howtouse.py'

Be sure to create in the directory you work in, a folder named 'dataimages' with subfolders 'train' and 'test'

The idea is to take a dataset and turn each object into an image that will feed a computer vision algorithm.

for now, this only works with dataset in which each feature contains categories.

You will need to pre-process your dataset:
- fill missing values
- categorize each feature
- map each category in each feature to Integers. ( use sklearn's preprocessing.LabelEncoder() for instance )
- split your data into : 
    - X : training dataset
    - y : label corresponding to training dataset
    - X_test : dataset for prediction
    
Each Input object is converted to image as follow : 

we look at each feature, and count the number of categories inside each of them. 
then we take the feature that has the largest number of categories and store this number. 
This is the height of our images. Indeed, we are going to create an image where each columns corresponds
to a feature, and each row corresponds to a category. 
This is why the height of our image needs to correspond to the largest number of categories.

( To generate the image examples, I used a dataset with 12 features and the largest number of categories was 11)

using the *mode '1'* in di.datatoimg(X,Xtest,wmode='1',savemode=True):
    each pixel column corresponds to a different feature. 
Thus, we have an image of size : 'max_number_of_categories' x 'number_of_features' 
you can see the result : *test_image_1.png* (12x12)

using the *mode 'w'* in di.datatoimg(X,Xtest,wmode='w',savemode=True):
    each feature will have a given column width in the image.
To calculate each feature's width, we create the covariance matrix and perform eigendecomposition, extract eigenvalues and normalize them to unit ( the same way you would do performing PCA ), assigning rounded eigenvalue to each feature, we have our widths. 
you can see the result : *test_image_w.png* (100x12) 

# Notes 
Be aware that savemode is set to False by default.

# improvements : 

- a first idea would be to change how certain features would be converted : 
speaking in terms of mode '1', if we call N the height of the image, if we have a certain 
feature that has M categories, such that M < N/2, instead of putting row1=categ1, row2=categ2, etc., 
we could jump rows in beetween each category, we would certainly add more clarity to the image. 
- Do the same kind of conversion for non-categorized features.
- Give the possibility to map the features on the image differently ( not only columns). 
- Give the possibility to use color channels to store more datas. 

