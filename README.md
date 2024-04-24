# NLU_Project_COMP34812-
Evidence Detection. Given a claim and a piece of evidence, determine if the evidence is relevant to the claim.  Binary Classification task.  Implemented Bi-directional LSTM with GlobalAveragePooling

Code Structure -> 
- Firstly, in the colab notebook the input file on which to make preditions should be uploaded(same directory).
- The "input_file_name" variable should be set to the name of the input file allowing the code to load this file when ran.

- Then the code can be ran(all cells). The code first connect to my google drive as that is where the GloVe Embeddings are stored which are used to encode the tokenized words
from the corpus of claims and evidences.
- The reason for this is due to the fact that downloading the GloVe embeddings from http://nlp.stanford.edu/data/glove.6B.zip was a challenge occassionaly due to the website being down.
- Hence, instead the GloVe embeddings were downloaded from https://huggingface.co/stanfordnlp/glove/blob/main/glove.6B.zip and stored in my google drive in a folder called "glove" as a zip file.
- In order to attempt to download from http://nlp.stanford.edu/data/glove.6B.zip, the PATH_TO_GLOVE variable can be removed from the initialization of the TextVectorizer(this would leave the embedding_folder set as default and mean that the code will attempt to download from stanford) however, this can lead to a timeout error and the code crashing.

- After connecting to google drive, the input file is read, then the same data preprocessing steps as with the training dataset are taken on the input file's claims and evidences. This inlcudes lowering the cases of the words, splitting compound words, replace special characters, removing reference markers from end of evidences, filtering uncommon symbols, stripping leading or trailing white spaces.

- Then the data claim and evidences are encoded via the use of GloVe embeddings and custom TextVectorizer class which allows for dealing with OOVs via random embedding initializations for out of word vocabs. This approach is taken from the following github repo for fact checking: https://github.com/TheOnesThatWereAbroad/FactChecking/blob/main/FactChecking.ipynb

- My trained Bi-direcation lstm with GlobalAverage pooling is loaded from my google drive. It can also be found here: https://livemanchesterac-my.sharepoint.com/:f:/g/personal/masroor_ahmad_student_manchester_ac_uk/Ev_MaV6QfY5CkFAbuuYrj-EBWHop-u1Ti32_QKMXIEil1Q?e=tfVnOw   on my onedrive. The link expires Expires on Friday, May 24, 2024.

- Then, finally the trained model is made use of to make predictions on the encoded claims and evidences with a threshold of 0.5. Where values greater than 0.5 are considered to be 1s and less are considered to be 0s.

- The results are then output to a csv file called "predictions.csv"

