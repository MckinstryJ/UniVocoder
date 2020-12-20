# UniVocoder
An UniVocoder implementation using Tacotron for voice mimicking. 

Given you have a directory full of .wav files, run... data_prep.py function:
```bash
train_json(in_dir, out_dir) 
```
...to generate the train.json file needed for tacotron's preprocess.py file. 

The in_dir parameter needs to be the location of the .wav directory (can be relative). The out_dir parameter needs to be './datasets/(name of data)'. After that, you can call preprocess.py as specified in tacotron.

Once you have preprocessed the .wav files, you will need to add pronunication to the CMU Dictionary. A helpful tool is the LOGIOS Lexicon Tool. You must provide it with a list a words in a CSV file (i.e. ...
```bash
world
hello
Today
Monday
```

... and it will generate a new file that has...
```bash
world ---
hello ---
Today ---
Monday ---
```

From there, you must add this bit of code to train.py file within Tacotron:
```bash
...
```

After this...
