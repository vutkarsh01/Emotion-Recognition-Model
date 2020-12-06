# Emotion-Recognition-Model
## Introduction:
1. The **vop_model** folder contains codes that use wav files along with their corresponding
vowel regions for training the model. The **non_vop_model** folder contains code that only
uses wav files for training. The **vop_model/emodbdata/wav** folder contains the training
set and **vop_model/emodbdata_test/wav** folder contains the testing set. All the results
are shown in the presentation.


## Downloading EmoDB database:
1. Download the Database from [**EmoDB**](https://drive.google.com/drive/folders/1UyZSdCm1UWE1tsD8wyVDrQNSL-45DbFg).

   - **NOTE** : We have already downloaded the database and split the files into training and
testing sets in the folders **vop_model/emodbdata/wav** and
**vop_model/emodbdata_test/wav**.


## Detecting VOPs :
1. Run the **vop_model/ex_vop.m** file in matlab to create text files from wav files in the
**vop_model/emodbdata/wav** folder. We have already done that for all the files and
stored all the text files in the **vop_model/vop_txt** folder. The text files contain VOP
timestamps for corresponding wav files.
**NOTE** : We have done this for all the files so that if the user wishes to shuffle the training
and testing data, he can do that easily and will not have to run the
**vop_model/ex_vop.m** file again for a different training set.


## Labelling Data :
1. Run the files : **vop_model/readdataemodb.ipynb** ,
**vop_model/readdataemodb_train.ipynb** and
**vop_model/readdataemodb_test.ipynb**. You can run these files in a jupyter notebook or the google colab. These files create **vop_model/emodb.pkl​ ,
vop_model/emodb_train.pkl** and **vop_model/emodb_test.pkl** respectively. These **.pkl**
files contain data and corresponding labels. We have already created them.


## Running the model :
1. Run the file **vop_model/speech_emotion_model.ipynb** in jupyter notebook or google
colab. This will give the final accuracy and confusion matrix.


## Getting comparative results :
1. Run the code for the **non_vop_model** folder following the above steps. This folder is for
the model trained without VOPs, only using the wav files.
2. Vary the number of MFCC features used to get other comparative results shown in the
presentation. Set **mfc = 21**, **dell = 21** and **filtt = 21** for the files :
**non_vop_model/readdataemodb.ipynb**, **vop_model/readdataemodb.ipynb** ,
**vop_model/readdataemodb_train.ipynb** and **vop_model/readdataemodb_test.ipynb**
to get the comparative results.
3. The current codes use both, the wav files and vowel regions, to train the model. To see
the result where only vowel regions are used to train the model, comment out the
following lines in **vop_model/speech_emotion_model.ipynb:**
   - f2 = open('./emodb_train.pkl', 'rb')
   - data2,label2 = cPickle.load(f2)
   - data2 = scal.fit_transform(data2,label2)
   - x_train2 = data2
   - y_train2 = label2
   - x_train = np.concatenate((x_train,x_train2))
   - y_train = np.concatenate((y_train,y_train2))

