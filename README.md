# SQuAD-it
## A large scale dataset for Question Answering in Italian

[SQuAD](https://rajpurkar.github.io/SQuAD-explorer/explore/1.1/dev/) [Rajpurkar et al. 2016]  is a large scale dataset for training of question answering systems on factoid questions. 
It contains more than 100,000 question-answer pairs about passages from 536 articles chosen from various domains of Wikipedia. 

**SQuAD-it** is derived from the SQuAD dataset and it is obtained through semi-automatic translation of the SQuAD dataset 
into Italian. It represents a large-scale dataset for open question answering processes on factoid questions in Italian. 
**The dataset contains more than 60,000 question/answer pairs derived from the original English dataset.** The dataset is split into training and test sets to support the replicability of the benchmarking of QA systems:

* `SQuAD_it-train.json`: it contains training examples derived from the original SQuAD 1.1 trainig material. 
* `SQuAD_it-test.json`: it contains test/benchmarking examples derived from the origial SQuAD 1.1 development material. 

More details about SQuAD-it can be found in [Croce et al. 2018]. The original paper can be found at this [link](https://link.springer.com/chapter/10.1007/978-3-030-03840-3_29).



### How to cite SQuAD-it


If you find SQuAD-it useful for your research, please cite the following paper:

~~~~
@InProceedings{10.1007/978-3-030-03840-3_29,
	author="Croce, Danilo and Zelenanska, Alexandra and Basili, Roberto",
	editor="Ghidini, Chiara and Magnini, Bernardo and Passerini, Andrea and Traverso, Paolo",
	title="Neural Learning for Question Answering in Italian",
	booktitle="AI*IA 2018 -- Advances in Artificial Intelligence",
	year="2018",
	publisher="Springer International Publishing",
	address="Cham",
	pages="389--402",
	isbn="978-3-030-03840-3"
}
~~~~


## Download

To download the SQuAD-it dataset, please refer to [https://github.com/crux82/squad-it](https://github.com/crux82/squad-it)

The resource is developed by the [Semantic Analytics Group](http://sag.art.uniroma2.it) of
the [University of Roma Tor Vergata](http://web.uniroma2.it/home). 
You can download a copy of the dataset (distributed under the CC BY-SA 4.0 license).

## Release format

The same format used in the SQuAD dataset is adopted: both train/test files are released in the following JSON format:

```
file.json
├── "data"
│   └── [i]
│       ├── "paragraphs"
│       │   └── [j]
│       │       ├── "context": "paragraph text"
│       │       └── "qas"
│       │           └── [k]
│       │               ├── "answers"
│       │               │   └── [l]
│       │               │       ├── "answer_start": N
│       │               │       └── "text": "answer"
│       │               ├── "id": "<uuid>"
│       │               └── "question": "paragraph question?"
│       └── "title": "document id"
└── "version": 1.1
```

The Wikipedia articles are split into paragraphs, one or more questions are made about each paragraph. The training set contains exactly one answer for each question, the test set contains one or more answers for each question. One of the most important properties of the dataset is that the answers are part of the paragraph and thus can be expressed as indices of the paragraph tokens, i.e., context `[ answer_start : answer_start + len(text)]`.

## Size of SQuAD-it

The original SQuAD dataset contains the following elements:

| Element | Training Set | Dev set |
| -------------- | --------------: | --------------: |
| Paragraphs  | 18 896 | 2 067 |
| Questions  | 87 599 | 10 570 |
|  Answers | 87 599 |34 726 |


Automatic translation lead to nearly 90% of translated paragraph-question-answer triplets.  Some of these triplets were not translated due to unknown characters or low lexical  coverage of the translation system. In many cases, the answer was not part of the translated paragraph any more after the translation, which lead to cancellation of most of the translations and lead to  approximately 45% of the translated triplets w.r.t. the original dataset.

Further corrections were made, such as exchange of the word order in the answer text, different morphological forms were looked for and others, and if such a modified answer was part of the paragraph, it was substituted. This increased the translated triplets to nearly 62% of the original.

The final SQuAD-it contains the following elements:

|  | Training Set IT	| Perc. w.r.t. SQuAD	| Test Set IT | Perc. w.r.t. SQuAD |	
| --------- | :---------: | :-----: |:---------:  | :-----: |
|	Paragraphs	|   18 506 | 97.9% | 2 010 | 97.2% | 
|	Questions	| 54 159 |  61.8% |7 609 | 72.0% |
|	Answers	| 54 159 |  61.8% |21 489 | 61.9%	|
					

## Evaluating a Neural Model over SQuAD-it

The DrQA system [Chen et al. 2017] was adapted to the Italian language. The system was modified in order to be able to measure the performance on the SQuAD-it dataset. The evaluation script and the description of the measures used (Exact Match and Macro F1) is available on the original SQuAD website, <https://rajpurkar.github.io/SQuAD-explorer/> (version v1.0 was used). The results were obtained on the Test Set. 


| |EM | F1 |
| --- | :---: | :---: |
|Results over the Test  Set |	56.1	| 65.9 |
 
 More details can be found in [Croce et al. 2018].



## Examples

Few examples of the answers given by the DrQA-it trained on SQuAD-it are hereafter reported. 

1. The answer to the question "*Dove si trovano le Isole Marshall?*"
is correct - "*Pacifico*".

	>* Question: Dove si trovano le Isole Marshall?
	>* Answer: Pacifico
	>* Sentence: Facente parte della Micronesia, le Isole Marshall sono un gruppo di atolli e isole situate nel **Pacifico**, poco a nord dell'equatore.
	>* Wikipedia Page: Isole Marshall

2. In this case, the answer to the question "*Quali sono gli stati che confinano con l'Austria?*" is "*Italia, Germania e Slovenia*", which is partially correct.
	>* Question: Quali sono gli stati con cui confina l'Austria?
	>* Answer: Italia, Germania e Slovenia
	>* Sentence: Ma quattro direttrici nord-sud che collegano il paese con i principali stati confinanti (**Italia, Germania E Slovenia**).
	>* Wikipedia Page: Austria


3. The answer to the question "*Dov'è nato Virgilio?*" is "*Ulassai*", which is correct, if referring to Virglio Lai, an Italian photographer, even though most people would be referring to the more famous Publius Vergilius Maro, (Publio Virgilio Marone, or simply Virgilio in Italian) born near Mantova 70 B.C.

	>* Question: Dove è nato Virgilio?
	>* Answer: Ulassai
	>* Sentence: Virgilio Lai (Ulassai, 1º Agosto 1926- Cagliari, 6 Aprile 2009) è fotografo del 1900 italiano.
	>* Wikipedia Page: Virgilio Lai


## References

[Rajpurkar et al. 2016] Pranav Rajpurkar, Jian Zhang, Konstantin Lopyrev, Percy Liang *SQuAD: 100,000+ Questions for Machine Comprehension of Text* In the Proceedings of the Conference on Empirical Methods in Natural Language Processing (EMNLP) — November 1–5, 2016 — Austin, Texas, USA.

[Chen et al. 2017] Danqi Chen, Adam Fisch, Jason Weston and Antoine Bordes *Reading Wikipedia to Answer Open-Domain Questions.* In the Proceedings of the  Annual Meeting of the Association for Computational Linguistics (ACL), 2017 Vancouver

[Croce et al. 2018] Danilo Croce, Alexandra Zelenanska, Roberto Basili *Neural Learning for Question Answering in Italian.* AI*IA 2018 -- Advances in Artificial Intelligence, 2018 Trento. pages 389-402


## Contacts

For any questions or suggestions, you can send an e-mail to <croce@info.uniroma2.it>

More details will be also added to [http://sag.art.uniroma2.it/demo-software/squadit/](http://sag.art.uniroma2.it/demo-software/squadit/)
