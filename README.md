# DialectDecoder
Hello! Thank you for your interest in DialectDecoder. Here is an overview of how it all fits together. 

## Required packages
- pygame
- torch
- tqdm
- Pillow
- matplotlib
- pandas
- scikit-learn
- librosa
- numpy

## Getting Started
Input Files: 
- A selection of songs grouped by dialect label folders that you want to train on. See https://github.com/GrahamDB/WCS_Song_WAV_data repository for an example of how the songs we trained on are organized and sorted.
- A metadata sheet with 5 columns: file path containing the labeled folder, file name, bird label (a number corresponding to the dialect label), latitude, and longitude of where the song was recorded. See DialectDecoder/metadata for an example metadata sheet.


Using the software (Note, make sure all of your directories/names are correct before running each script)

The following you should only have to do once.
1. Decide how many classes you want to train on, how many and the type of anomalous classes you want to add in, etc. 
1.	Have your songs in folders, similar to what is shown in the cut_songs folder. 
2.  Update the dialect label to number definitions in `prep/make_metadata.py` and `train/knn_classifier.py`.
3.  Update the bird_label array with the chosen dialect labels in `train/CNN_classifier.py`.  The first label is mapped to 0, the second to 1, etc.
3.  Update the bird_classes array with the chosen dialect labels in `2_DialectDecoder.py`, `3_update_networks.py` and `Training_DialectDecoder.py`.  The first label is mapped to 0, the second to 1, etc.
3.	Generate your metadata and generate/crop the spectrograms for the DialectDecoder by running 0_prep_data.py.

These you’ll do more than once depending on what you’re using the labeling birds game for.
7.	Change experiment_name to name your experiment (make sure it’s consistent across all numbered files). 
5.	Run 1_train_networks.py which will train the CNN and k-NN for the experiment.
6.	Run 2_DialectDecoder.py  and classify the desired number of images.
7.	After labeling all (or a subset) of the images, add in the newly classified images and retrain the CNN and k-NN with 3_update_networks.py.

Of course, the above is just the recommended use. Feel free to play around with the files to accommodate your needs.

## Details
### What each script in DialectDecoder does: 

0_prep_data.py — Runs all files in the prep folder that you need to create your spectrograms to train and use DialectDecoder on

prep:
-	gen_specs.py  — Generate the spectrograms from the audio data.
-	make_metadata.py — Makes a .csv file with the appropriate metadata needed for the CNN and the label game.
-	cropper.py — Takes in the spectrograms made by gen_specs.py, crops them down to the appropriate size, and saves them to a new folder (note, the new folder has to exist). You might have to grant python permission to do this, I solved this using `chmod 775 cropper.py`. 

1_train_networks.py — Runs all the programs in the train folder to train the CNN and k-NN for use in DialectDecoder.

train:
-	split_data.py — Splits data into whatever folders you want. Used to split into train/validate/test sets.
-	CNN_classifier.py — The file that makes and trains CNNs.
-	knn_classifier.py — The file that makes and trains k-NNs.
-	get_location.py — A function to pull the location of a recorded song given the filename.
-	update_CNN.py — Trains a new CNN based off the weights from the first CNN created with train.py.
-	button.py — Makes the button and dropdown classes for the game.

2_DialectDecoder.py — The script that runs the labeling game. Run this in terminal to start the game.

3_update_networks.py — The script that allows you to add in the newly labeled data

### What is in each non-script folder:
-	__pycache__ — Artifact of running the python code
-	CNN_Networks — A place to store trained CNN networks.
-	data — All song data (.wav files) and spectrogram data (.png files)
-	kNN_networks — A place to store trained k-NN classifiers
-	metadata — A place to store all metadata files
-	output files — The directory where all of the output files live








