# HBD-Data-Project
## Working Group 1: Text Analysis
### Anonymization
This repository contains scripts and projects on anonymization of clinical letters

## How to use
You can run the script by calling 
> python ita_deidentification.py

You can change the script behavior by editing the config.json file.  

### Models
Set the desired models to use in the config.json file, under the "models" section. Leave the field empty if you don't want to anonymize it.  
Currently these are the fields that can be anonymized:
#### Telephone
Supported models: regex  
Covered cases (regex):  
>3491234567  
+393491234567  
00393491234567  
(+39)3491234567  
+(39) 349 8505734  
349 8505734  
3498505734   
+39 349 850 5734  
349 850 5734  
0543 721370  
0543721370  
06 43721370  
064 3721370  
064/3721370  

#### Zipcode
Supported models: regex  
Covered cases (regex):  
>47122  
01010  

#### Email
Supported models: regex  
Covered cases (regex):  
>mario.rossi@libero.it  
m.r@l.it  
m5.r2@v2.it  

#### Date
Supported models: regex  
Covered cases (regex):  
>28/06/2022  
10 9 2021  
4/09/2022  
Gennaio 2020.  
7 gennaio 2020  
18 gennaio 2021  
7-1-2000  
12/22  

#### Fiscal code
Supported models: regex  

#### Person
Supported models: stanza, spacy

#### Organization
Supported models: stanza, spacy

#### Address
Supported models: stanza, spacy

### Mask modes
Set the desired mask mode and special character in the "mask" section of the config.json file.  
Currently the following modes are supported:
* **tag** : The anonymized text is replaced with a tag containing the entity type (telephone,person etc.). _(default option)_
* **tag_l** : Same as tag but preserving original data length. Missing data is filled with the special character. [Note: Length is preserved only if the anonymized entity is longer than the tag.]
* **anon_l** : The anonymized text is gonna be converted to special character, preserving original data length.
* **anon** : Same as anon_l but anonymized text is replaced with fixed length special characters.
* **random (TODO!)** : Replace the anonymized text with a randomly generated text of the same entity type.

You can use any single character as **special_character** (default is star), which is gonna be used to replace the anonymized text.

With the "date_level" parameter you can choose how to anonymize dates. Supported modes are:
* **hide** : Anonymize dates according to the chosen mask mode _(default option)_
* **month** : Keep only the month
* **year** : Keep only the month and the year

### Models details
* **regex** : This model was developed by HBD-anonymization team to specifically recognize some italian entities (like fiscal code and postal code) and some more generic ones (like telephones and dates) using regular expressions.  
More info: https://en.wikipedia.org/wiki/Regular_expression
* **spacy** : spaCy is an open-source software library for advanced natural language processing. The model used in this script is it_core_news_lg, a pipeline comprehending tokenization, lemmatization and named entity recognition, trained on a large news database. Supported entities are: **person**, **organization** and **address**.  
More info: https://spacy.io/models/it#it_core_news_lg
* **stanza** : stanza is The Stanford NLP Group's official Python NLP library. The model used in this script is the italian pipeline, comprehending tokenization and NER, trained on FBK dataset. Supported entities are: **person**, **organization** and **address**.  
More info: https://stanfordnlp.github.io/stanza/ner_models.html


