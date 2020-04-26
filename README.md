# AnnotatedSentence

This resource allows for matching of Turkish words or expressions with their corresponding entries within the Turkish dictionary and the Turkish PropBank, morphological analysis, named entity recognition and shallow parsing.

For Developers
============

You can also see [Java](https://github.com/starlangsoftware/AnnotatedSentence), [Python](https://github.com/starlangsoftware/AnnotatedSentence-Py), or [C#](https://github.com/starlangsoftware/AnnotatedSentence-CS) repository.

## Requirements

* [C++ Compiler](#cpp)
* [Git](#git)


### CPP
To check if you have compatible C++ Compiler installed,
* Open CLion IDE 
* Preferences >Build,Execution,Deployment > Toolchain  

### Git

Install the [latest version of Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## Download Code

In order to work on code, create a fork from GitHub page. 
Use Git for cloning the code to your local or below line for Ubuntu:

	git clone <your-fork-git-link>

A directory called AnnotatedSentence-CPP will be created. Or you can use below link for exploring the code:

	git clone https://github.com/olcaytaner/AnnotatedSentence-CPP.git

## Open project with CLion IDE

To import projects from Git with version control:

* Open CLion IDE , select Get From Version Control.

* In the Import window, click URL tab and paste github URL.

* Click open as Project.

Result: The imported project is listed in the Project Explorer view and files are loaded.


## Compile

**From IDE**

After being done with the downloading and opening project, select **Build Project** option from **Build** menu. After compilation process, user can run TestAnnotatedSen.cpp .

## Data Format

The structure of a sample annotated word is as follows:

	{turkish=yatırımcılar}
	{analysis=yatırımcı+NOUN+A3PL+PNON+NOM}
	{semantics=0841060}
	{namedEntity=NONE}
	{shallowParse=ÖZNE}
	{propbank=ARG0:0006410}

As is self-explanatory, 'turkish' tag shows the original Turkish word; 'analysis' tag shows the correct morphological parse of that word; 'semantics' tag shows the ID of the correct sense of that word; 'namedEntity' tag shows the named entity tag of that word; 'shallowParse' tag shows the semantic role of that word; 'propbank' tag shows the semantic role of that word for the verb synset id (frame id in the frame file) which is also given in that tag.

Detailed Description
============
+ [AnnotatedCorpus](#annotatedcorpus)
+ [AnnotatedSentence](#annotatedsentence)
+ [AnnotatedWord](#annotatedword)
+ [Automatic Annotation](#automatic-annotation)


## AnnotatedCorpus

İşaretlenmiş corpusu yüklemek için

	AnnotatedCorpus(File folder, String pattern)
	a = AnnotatedCorpus(new File("/Turkish-Phrase"), ".train")

	AnnotatedCorpus(File folder)
	a = AnnotatedCorpus(new File("/Turkish-Phrase"))

Bir AnnotatedCorpus'daki tüm cümlelere erişmek için

	for (int i = 0; i < a.sentenceCount(); i++){
		AnnotatedSentence annotatedSentence = (AnnotatedSentence) a.getSentence(i);
		....
	}

## AnnotatedSentence

Bir AnnotatedSentence'daki tüm kelimelere ulaşmak için de

	for (int j = 0; j < annotatedSentence.wordCount(); j++){
		AnnotatedWord annotatedWord = (AnnotatedWord) annotatedSentence.getWord(j);
		...
	}

## AnnotatedWord

İşaretlenmiş bir kelime AnnotatedWord sınıfında tutulur. İşaretlenmiş kelimenin morfolojik
analizi

	MorphologicalParse getParse()

İşaretlenmiş kelimenin anlamı

	String getSemantic()

İşaretlenmiş kelimenin NER anotasyonu

	NamedEntityType getNamedEntityType()

İşaretlenmiş kelimenin özne, dolaylı tümleç, vs. shallow parse tagı

	String getShallowParse()

İşaretlenmiş kelimenin dependency anotasyonu

	UniversalDependencyRelation getUniversalDependency()
	
## Automatic Annotation

Bir cümlenin Predicatelarını otomatik olarak belirlemek için

	TurkishSentenceAutoPredicate(FramesetList framesetList)

sınıfı kullanılır. Örneğin,

	a = TurkishSentenceAutoPredicate(new FramesetList());
	a.autoPredicate(sentence);

ile sentence cümlesinin predicateları otomatik olarak işaretlenir.

Bir cümlenin argümanlarını otomatik olarak belirlemek için

	TurkishSentenceAutoArgument()

sınıfı kullanılır. Örneğin,

	a = TurkishSentenceAutoArgument();
	a.autoArgument(sentence);

ile sentence cümlesinin argümanları otomatik olarak işaretlenir.

Bir cümlede otomatik olarak morfolojik belirsizlik gidermek için

	TurkishSentenceAutoDisambiguator(RootWordStatistics rootWordStatistics)
	TurkishSentenceAutoDisambiguator(FsmMorphologicalAnalyzer fsm, RootWordStatistics rootWordStatistics)
								  
sınıfı kullanılır. Örneğin,

	a = TurkishSentenceAutoDisambiguator(new RootWordStatistics());
	a.autoDisambiguate(sentence);

ile sentence cümlesinin morfolojik belirsizlik gidermesi otomatik olarak yapılır.

Bir cümlede adlandırılmış varlık tanıma yapmak için

	TurkishSentenceAutoNER()

sınıfı kullanılır. Örneğin,

	a = TurkishSentenceAutoNER();
	a.autoNER(sentence);

ile sentence cümlesinde varlık tanıma otomatik olarak yapılır.

Bir cümlede anlamsal işaretleme için

	TurkishSentenceAutoSemantic()

sınıfı kullanılır. Örneğin,

	a = TurkishSentenceAutoSemantic();
	a.autoSemantic(sentence);

ile sentence cümlesinde anlamsal işaretleme otomatik olarak yapılır.

## Cite
If you use this resource on your research, please cite the following paper: 

```
@INPROCEEDINGS{yildiz18, 
	author={O. T. {Yıldız} and K. {Ak} and G. {Ercan} and O. {Topsakal} and C. {Asmazoğlu}}, 
	booktitle={2018 2nd International Conference on Natural Language and Speech Processing (ICNLSP)}, 
	title={A multilayer annotated corpus for Turkish}, 
	year={2018}, 
	pages={1-6}
}

@article{acikgoz,
	title={All-words word sense disambiguation for {T}urkish},
	author={O. Açıkg{\"o}z and A. T. G{\"u}rkan and B. Ertopçu and O. Topsakal and B. {\"O}zenç and A. B. Kanburoğlu and {\.{I}}. Çam and B. Avar and G. Ercan and O. T. Y{\i}ld{\i}z},
	journal={2017 International Conference on Computer Science and Engineering (UBMK)},
	year={2017},
	pages={490-495}
}

@inproceedings{ertopcu17,  
	author={B. {Ertopçu} and A. B. {Kanburoğlu} and O. {Topsakal} and O. {Açıkgöz} and A. T. {Gürkan} and B. {Özenç} and İ. {Çam} and B. {Avar} and G. {Ercan} and O. T. {Yıldız}},  
	booktitle={2017 International Conference on Computer Science and Engineering (UBMK)},  title={A new approach for named entity recognition},   
	year={2017},  
	pages={474-479}
}

@INPROCEEDINGS{topsakal17,
	author={O. {Topsakal} and O. {Açıkgöz} and A. T. {Gürkan} and A. B. {Kanburoğlu} and B. {Ertopçu} and B. {Özenç} and İ. {Çam} and B. {Avar} and G. {Ercan} and O. T. {Yıldız}}, 
	booktitle={2017 International Conference on Computer Science and Engineering (UBMK)}, 
	title={Shallow parsing in Turkish}, 
	year={2017}, 
	pages={480-485}
}
