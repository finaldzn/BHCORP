# BEEIA Model

![poster](mdfile\Poster.png)


_______________

A general explanation of the project can be found here, with specifics concerning performance and the choices that were done to come up with this result : 

[Projet Closure Report](projectclosurereport.pdf)

**Summary** :
- Getting all the files ready
- Give data to the database
- Start Training 
- Testing
- Export the model to TFLITE and android
- Future evolutions

________________

This is a work has been done by : 
- Victor Mouradian *contact*: <victor.mouradian@gmail.com>
- Virgile Procureur *contact*: 
<procureurv@gmail.com>
- Paul Pichlak *contact*:
<paulpichlak@gmail.com>
- Tobias Ohana  *contact*: <tobias1998@hotmail.fr>
- Wassim Serradj *contact*: <wassim078@hotmail.fr>

This work has been done for the company BEEIA and for [ESILV](https://www.esilv.fr) in the context of pi² projects.

This file goes into the specific concerning the object recognition model, for more information concerning the app or the connected hive please visit their associated pages.

________
## Setting up everything 

To continue we are going to need a few files :

- the data wich is pictures of queen bees labelized and organised with pascalvoc.

    - [Google Drive](https://drive.google.com/drive/folders/1toBosuzPOAizm9NzIlMJHsgRZ7KsNpJ4?usp=sharing), the data can only be upload to google drive as github has a 100mb limit on files.
   
- the last trained model, so you can start again from a check point
    - [SSD](https://drive.google.com/drive/folders/1-2SuaSwxefXZMqi9IFSnt_mlL5Qu4Vg6?usp=sharing)
    - [RNN](https://drive.google.com/open?id=1ElKTOz-Tx74cyHFt9hMErEwdwaVWy6QR)

Those file are available on this shared drive, I advice you make a local copy of it so you can work on your own.

- Copy the google colab [file](https://colab.research.google.com/drive/1e9s61mfkgQniunoi6vBFMDGelnq9SALP/) and create your own so you can add your modifications. The file is also present [in the notebook folder](notebook\all_in_one.ipynb)

Please refer to the comments on the colab file to get the hang of it there.
_________
## Give data to the database

1. Find a video (youtube or else) with queen bees
2. Open the video with the labelling software [VOTT](https://github.com/microsoft/VoTT)
3. Labelize frame by frame the queen bees and everything else you want the model to be able to recognize.
4. Export your data under the "pascal_voc" format.
_______
## Create the inference graph and model
You can use the notebook for everything regarding the model

There is the all_in_one notebook that details each step if you want everything in one file.

### Create the records
To create the records (you can skip this part as the results are in the data folder), the output should be a **pascalvoc_training.record** file : 

- [Google Colab](https://colab.research.google.com/drive/1ACZeaWkk7UBG8y1MIHnkmm-1YUf68IrR)
- [Notebook folder](notebook\dataset_creation.ipynb)

### Train the model 
To start training on the models, the output should be a folder called **inference graph** : 
- [Google Colab](https://colab.research.google.com/drive/1A-fo0Yrn7MfdwtV3DDna31lPjv2N119R)
- [Notebook folder](notebook\train.ipynb)

### Convert into Tflite
To convert the obtained model (works only with SSD models), the output should be a **model.tflite** file :

- [Google Colab](https://colab.research.google.com/drive/17j7pLSozdRq2sO708hDkKVXDKzqiOXUX)
- [Notebook folder](notebook\convert_tflite.ipynb)
_____________
## Testing

They are a few files you can use for testing your model and do predictions.
Those files are known to work with the **RNN** model, the **SSD** model has issue working with those files.


```
py predictions/object_dection_image.py
```
For example, this file will allow you to predict on an image, you need to specify the path for the inference graph and for the picture. Some test pictures are available in the  [./testfiles](./testfiles) folder


RNN model  prediction
![rnn](mdfile\Annotation.png)




___________
## Export the model to TFLITE and android

For the export to TFLITE please follow the instructions on the colab file.

Once you have your model.tflite file you can then upload it to the BEEIA android app and change it. At the next launch the app should have the updated model

- [Here is the repo for the app](https://github.com/finaldzn/BeeIA)
- Or [here](./Android_app)

More instructions are available there.

SSD model prediction

![ssd](mdfile\beeia_pic.jpg)
_____

## Future evolutions

The model at the time of writing had a few issues. A low recognition on the app (80% max).

I think a few evolutions would make the model better here it is : 
- Add a few regular bee picture to the model and train it on them so the model can differantiate more easily between regular bees and queen bees
- Figure out how to quantized the tflite model, today this is not possible (Refer to the notebook for more informations)
- Make the model work on TF 2.x
