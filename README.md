# UniVocoder

# TODO: upload current code for LJSpeech on both.

A 'Tacoder' implementation for TTS synthesis. In it, I use the Tacotron model to generate mel-spectrograms and then pass that into the generic Vocoder to generate a TTS audio file.

A good entry point into TTS, in my opinion, but there are a few flaws to this combination. In general, its slow  in its training and synthesis and the output is not ideal.

Given you have a directory full of .wav files, run... data_prep.py function:
```python
train_json(in_dir, out_dir) 
```
...to generate the train.json file needed for tacotron's preprocess.py file. 

The in_dir parameter needs to be the location of the .wav directory (can be relative). The out_dir parameter needs to be './datasets/(name of data)'. After that, you can call preprocess.py as specified in tacotron.

Once you have preprocessed the .wav files, you will need to add pronunication to the CMU Dictionary. A helpful tool is the LOGIOS Lexicon Tool. You must provide it with a list a words in a text file (i.e. ...
```bash
world
hello
Today
Monday
```
You might have a metadata.csv file that is a bit large so instead of manually listing out each word you can use the data_prep.py function:
```python
logios_lexicon()
```
This will generate the needed text file. Just add the file to the tool and it will generate a new file that has:

```bash
AND	AH N D
AND(2)	AE N D
REMOVE	R IY M UW V
ALL	AO L
```

From there, you must add this bit of code to text.py within the parse_text() function under the first line of code:
```bash
for i in range(len(words)):
    words[i] = words[i].translate(str.maketrans(dict.fromkeys(string.punctuation)))
while '' in words:
    words.remove('')
```

...then add a handful of specific words that weren't caught the first time. After that modify the code so that the batches are investigated individual (since some will be NoneType). From there I believe train.py should work for new data.
