---
title: "Sign Language Processing"
link-citations: true
geometry: margin=3cm
css: style.css
linkcolor: Black
secnumdepth: 3
header-includes:
- |
  \usepackage{pdflscape}
author:
- Amit Moryossef | Bar-Ilan University | amitmoryossef@gmail.com
abstract: |
    This project aims to organize the sign language processing literature, datasets, and tasks.
    Sign Language Processing (SLP) is a field of artificial intelligence
    concerned with automatic processing and analysis of sign language content.
    This is a work in progress. The contents of this document will be refined over the course of 2020-2022.
...


## Introduction

Sign languages (also known as signed languages) are languages that use the visual modality to convey meaning through manual articulations in combination with non-manual elements.
Similar to spoken languages, sign languages are natural languages governed by a set of linguistic rules [@sandler2006sign], 
both emerging through an abstract, protracted aging process and evolved over time without meticulous planning.
They are also distinct from spoken languages---i.e., American Sign Language (ASL) is not a visual form of English.
Sign languages are not universal, and they are not mutually intelligible with each other, although there are also striking similarities among sign languages.

Sign Language Processing [@bragg2019sign] is an emerging field of artificial intelligence concerned with automatic processing and analysis of sign language content.
It is a subfield of both natural language processing and computer vision.
Challenges in sign language processing frequently involve machine translation of sign languages to spoken language text (sign language translation), 
from spoken language text (sign language production), or sign language recognition for sign language understanding.

One of the challenging aspects regarding translation of sign languages is that as they are more disjoint from spoken languages,
the translation process requires more interpretation, thus different interpreters would translate spoken or sign language differently.
This is a major challenge in translation evaluation, where for example a sequence of signs could be interpreted into a different sentence in spoken language, or vice versa.
The challenge exacerbates where a sign does not have a spoken language translation, and thus translation might be impossible, 
or when trying to translate some content with subtext like humor and puns, it might be impossible to convey the content and subtext together.

## Corpora

### Data Formats

The only widely accepted format for sign language data includes videos of the signing, 
and either a [gloss](https://en.wikipedia.org/wiki/Gloss_(annotation)) or a spoken language text translation.
Sign language videos may include a "depth" channel produced by a [time-of-flight camera](https://en.wikipedia.org/wiki/Time-of-flight_camera).

Sign languages have no formal written format. 
There are various language specific notations systems 
([Stokoe notation](https://en.wikipedia.org/wiki/Stokoe_notation) [@writing:stokoe2005sign] and [si5s](https://en.wikipedia.org/wiki/Si5s) for American Sign Language,
[SWL](https://zrajm.github.io/teckentranskription/freesans-swl.html) [@writing:bergman1977tecknad] for Swedish Sign Language, etc...)
and various universal notations systems ([SignWriting](https://en.wikipedia.org/wiki/SignWriting) [@writing:sutton1990lessons], [HamNoSys](https://en.wikipedia.org/wiki/Hamburg_Notation_System) [@writing:prillwitz1990hamburg]) but no writing system has been adopted widely enough, 
by the international Deaf community, that it could be considered the "written form" of a given sign language.

Additionally, sign language corpora may include human [poses](https://en.wikipedia.org/wiki/Pose_(computer_vision)), either recorded with [motion capture](https://en.wikipedia.org/wiki/Motion_capture) technologies,
or estimated from videos using [pose estimation](https://en.wikipedia.org/wiki/Pose_(computer_vision)#Pose_estimation) techniques.
Full body human poses include all the relevant information for sign language processing (manual or non-manual), except for visual cues such as props.

The following table exemplifies the various data formats.
For this example we use [SignWriting](https://en.wikipedia.org/wiki/SignWriting) as the writing system.
Note that the same sign might have two unrelated glosses, and the same gloss might have multiple valid texts.

```{=html}
<div id="formats-table" class="table">
```
formats.md
```{=html}
</div>
```


### Annotation Tools


##### ELAN - EUDICO Linguistic Annotator
[ELAN](https://archive.mpi.nl/tla/elan) [@wittenburg2006elan] is an annotation tool for audio and video recordings.
With ELAN a user can add an unlimited number of textual annotations to audio and/or video recordings. 
An annotation can be a sentence, word or gloss, a comment, translation or a description of any feature observed in the media. 
Annotations can be created on multiple layers, called tiers, which can be hierarchically interconnected. 
An annotation can either be time-aligned to the media, or it can refer to other existing annotations. 
The content of annotations consists of Unicode text and annotation documents are stored in an XML format (EAF).
ELAN is open source ([GPLv3](https://en.wikipedia.org/wiki/GNU_General_Public_License#Version_3)), and installation is [available](https://archive.mpi.nl/tla/elan/download) for Windows, macOS, and Linux.
PyMPI [@pympi-1.69] allows for simple python interaction with Elan files.


##### iLex
[iLex](https://www.sign-lang.uni-hamburg.de/ilex/) [@hanke2002ilex] is a tool for sign language lexicography and corpus analysis, 
that combines features found in empirical sign language lexicography and in sign language discourse transcription. 
It supports the user in integrated lexicon building while working on the transcription of a corpus and 
offers a number of unique features considered essential due to the specific nature of sign languages.
iLex binaries are [available](https://www.sign-lang.uni-hamburg.de/ilex/ilex.xml) for macOS.

##### SignStream
[SignStream](http://www.bu.edu/asllrp/SignStream/3/) [@neidle2001signstream] is a tool for linguistic annotations and computer vision research on visual-gestural language data
SignStream installation is only [available](http://www.bu.edu/asllrp/SignStream/3/download-newSS.html) for old versions of MacOS, and is distributed under MIT license.

##### Anvil - The Video Annotation Research Tool
[Anvil](https://www.anvil-software.org/) [@kipp2001anvil] is a free video annotation tool,
offering multi-layered annotation based on a user-defined coding scheme.
In Anvil, the annotator can see color-coded elements on multiple tracks in time-alignment. 
Some special features are cross-level links, non-temporal objects, timepoint tracks, coding agreement analysis, 
3D viewing of motion capture data and a project tool for managing whole corpora of annotation files.
Anvil installation is [available](https://www.anvil-software.org/download/index.html) for Windows, macOS, and Linux.


### Existing Datasets

Currently, there is no easy way or agreed upon format to download and load sign language datasets, and as such, evaluation on these datasets is scarce.
As part of this work, we streamlined loading of available datasets using [🤗Datasets](https://github.com/huggingface/datasets).
This allows researchers to load large and small datasets alike with a simple command, and be comparable to other works:

```python
from datasets import load_dataset
 
ngt = load_dataset('ngt')
wlasl = load_dataset('wlasl')
aslg_pc12 = load_dataset('aslg_pc12')
autsl = load_dataset('autsl', train_decryption_key='***')
...
```


The following table contains a curated list of datasets including various sign languages and data formats:

```{=ignore}
TODO [this thesis](https://scholarsarchive.byu.edu/cgi/viewcontent.cgi?article=6477&context=etd) page 26 has more datasets.
- Spanish Sign Language: María del Carmen Cabeza-Pereiro (cabeza@uvigo.es)
- Estonian Sign Language: ?
- Finnish Sign Language: Juhana Salonen, Antti Kronqvist (juhana.salonen@jyu.fi, antti.r.kronqvist@jyu.fi)
- Danish Sign  Language: Jette H. Kristoffersen, Thomas Troelsgård (jehk@ucc.dk, ttro@ucc.dk)


GSLC - https://www.academia.edu/1990408/GSLC_creation_and_annotation_of_a_Greek_sign_language_corpus_for_HCI
Emailed Eleni and Evita, need to make sure data is available

```


```{=latex}
\newgeometry{left=0.3cm,right=0.3cm,top=-1.5cm,bottom=-1.5cm}
\begin{landscape}
\hspace{1.5cm}
```

🎥 Video | 👋 Pose | 👄 Mouthing | ✍ Writing | 📋 Gloss | 📜 Text | 🔊 Speech

<div id="datasets-table" class="table">
datasets.md
</div>

```{=latex}
\end{landscape}
\restoregeometry
```


## Tasks


### Sign Language Detection

Sign language detection [@detection:borg2019sign;@detection:moryossef2020real] is defined as the binary-classification for any
given frame of a video whether a person is using sign-language or not.

@detection:borg2019sign introduced the classification of frames taken from YouTube videos as either signing or not. 
They take a spatial and temporal approach based on VGG-16 [@simonyan2015very] CNN to encode each frame 
and use a [GRU](https://en.wikipedia.org/wiki/Gated_recurrent_unit) [@cho2014learning] 
to encode the sequence of frames in a window of 20 frames at 5fps.
In addition to the raw frame, they also either encode optical flow history, aggregated motion history, or frame difference.

@detection:moryossef2020real improved upon their method by performing sign language detection in real-time.
They identified that sign language use involves movement of the body, and as such, designed a model that works on top of 
human poses rather than directly on the video signal.
They calculate the optical flow norm of every joint detected on the body, and apply a small yet effective contextualized model
to predict for every frame whether the person is signing or not.

### Sign Language Identification

Sign language identification [@identification:gebre2013automatic;@identification:monteiro2016detecting] is defined as the classification between two or more sign languages.
 
@identification:gebre2013automatic found that a simple random-forest classifier can distinguish between 
British Sign Language (BSL) and Greek Sign Language (ENN) with a 95\% F1 score.
This finding is further supported by @identification:monteiro2016detecting, which manages to differentiate between 
British Sign Language and French Sign Language (Langue des Signes Française, LSF) with 98\% F1 score in videos with static backgrounds,
and between American Sign Language and British Sign Language with 70\% F1 score for videos mined from popular video sharing sites. 
The authors attribute their success mainly to the different fingerspelling systems, which is two-handed in the case of BSL and one-handed in the case of ASL and LSF.

### Sign Language Recognition, Translation, and Production

Sign language translation is generally considered the task of translating between a video in sign language to spoken language text.
Sign language production is the reverse process, of producing a sign language video from spoken language text.
Sign language recognition is the task of recognizing the signs themselves in sign language.


In the following graph, we can see a fully connected pentagon where each node is a single data representation, 
and each directed edge represents the task of converting between one data representation to another.

We split the graph into two: 

- Every edge to the left, on the orange background, represents a task in computer vision. These tasks are inherently multilingual, thus generalize between sign languages.
- Every edge to the right, on the blue background, represents a task in natural language processing. These tasks are sign language specific, requiring a specific sign language lexicon or spoken language tokens.
- Every edge on both backgrounds represents a task requiring a combination of computer vision and natural language processing.

```{=html}
<p>
<span style="font-weight: bold;">Computer Vision</span>
<span style="font-weight: bold;float:right">Natural Language Processing</span>
<object type="image/svg+xml" data="assets/tasks/tasks.svg" class="logo"></object>
</p>
```

```{=latex}
\begin{minipage}{.5\linewidth}\begin{flushleft}\textbf{Computer Vision}\end{flushleft}\end{minipage}
\hfill
\begin{minipage}{.5\linewidth}\begin{flushright}\textbf{Natural Language Processing}\end{flushright}\end{minipage}

\includegraphics[width=\linewidth]{assets/tasks/tasks.pdf}
```


In total, there are 20 tasks conceptually defined by this graph, with varying amounts of previous research.
Every path between two nodes might or might not be valid, depending on how lossy the tasks in the path are.

---

#### Video-to-Pose

Video-to-Pose---commonly known as pose estimation---is the task to detect human figures in images and videos, 
so that one could determine, for example, where someone's elbow shows up in an image.
It was shown [@vogler2005analysis] that the face pose correlates with facial non-manual features like head direction.

This area has been thoroughly researched [@pose:pishchulin2012articulated;@pose:chen2017adversarial;@pose:cao2018openpose;@pose:alp2018densepose]
with objectives varying from predicting 2D / 3D poses, to a selection of a small specific set of landmarks or a dense mesh of a person.

OpenPose [@pose:cao2018openpose;@pose:simon2017hand;@pose:cao2017realtime;@pose:wei2016cpm] is the first real-time multi-person system to 
jointly detect human body, hand, facial, and foot keypoints (in total 135 keypoints) in 2D on single images.
While their model can estimate the full pose directly from an image in a single inference,
they also suggest a pipeline approach where first they estimate the body pose, and then independently estimate 
the hands and face poses by acquiring higher resolution crops around those areas.
With multiple angles of recording, OpenPose also offers keypoint triangulation in order to reconstruct the pose in 3D.

@pose:alp2018densepose takes a different approach with DensePose. 
Instead of classifying for every keypoint which pixel is most likely, they suggest similarly to semantic segmentation,
for each pixel to classify which body part it belongs to.
Then, for each pixel, knowing the body part, they predict where that pixel is on the body part, relative to a 2D projection of a representative body model.
This approach results in reconstruction of the full-body mesh, and allows sampling to find specific keypoints similar to OpenPose.

However, 2D human poses might not be sufficient to fully understand the position and orientation of landmarks in space,
and applying pose estimation per-frame does not take the video temporal movement information into account, 
especially in cases of rapid movement which contain motion blur.

@pose:pavllo20193d developed two methods to convert between 2D poses to 3D poses. 
The first, a supervised method, was trained to use the temporal information between frames to predict the missing Z-axis.
The second, an unsupervised method, leveraging the fact that the 2D poses are merely a projection of an unknown 3D pose, 
and train a model to estimate the 3D pose and back-project to the input 2D poses. This back-projection is a deterministic process, 
and as such, it applies constraints on the 3D pose encoder. 
@pose:zelinka2020neural follows a similar process, and adds a constraint for bones to stay of a fixed length between frames.

@pose:panteleris2018using suggests converting the 2D poses to 3D using inverse kinematics (IK), 
a process taken from computer animation and robotics to calculate the variable joint parameters needed to place the end of a kinematic chain, 
such as a robot manipulator or animation character's skeleton, in a given position and orientation relative to the start of the chain.
Demonstrating their approach on hand pose estimation, they manually explicitly encode the constraints and limits of each joint, resulting in 26 degrees of freedom.
Then, non-linear least-squares minimization fits a 3D model of the hand to the estimated 2D joint positions, recovering the 3D hand pose.
This is similar to the back-projection used by @pose:pavllo20193d, except here no temporal information is being used.



#### Pose-to-Video

Pose-to-Video, also known as motion-transfer or skeletal animation in the field of robotics and animation, is the
conversion of a sequence of poses to a realistic-looking video.
For sign language production, this is the final "rendering" to make the produced sign language look human.

@pose:chan2019everybody demonstrates a semi-supervised approach where they take a set of videos, 
run pose-estimation with OpenPose [@pose:cao2018openpose], and learn an image-to-image translation [@isola2017image]
between the rendered skeleton and the original video.
They demonstrate their approach on human dancing, where they can extract poses from a choreography, 
and render any person as if they were dancing that dance.
They predict two consecutive frames for temporally coherent video results and 
introduce a separate pipeline for a more realistic face synthesis, although still flawed.

@pose:wang2018vid2vid suggest a similar method using DensePose [@pose:alp2018densepose] representations 
in addition to the OpenPose [@pose:cao2018openpose] ones. 
They formalize a different model, with various objectives to optimize for such as background-foreground separation and
temporal coherence by using the previous two timestamps in the input.

Using the same method by @pose:chan2019everybody on "Everybody Dance Now", @pose:girocan2020slrtp asks, "Can Everybody Sign Now"?
They evaluate the generated videos by asking signers various tasks after watching them, and comparing the signers' ability to
perform these tasks on the original videos, rendered pose videos, and reconstructed videos.
They show that subjects prefer synthesized realistic videos over skeleton visualizations, 
and that out-of-the-box synthesis methods are not really effective enough, 
as subjects struggled to understand the reconstructed videos.

As a direct response, @saunders2020everybody shows that like in @pose:chan2019everybody, 
where an adversarial loss is added to specifically generate the face, adding a similar loss to the hand generation process
yields high resolution, more photo-realistic continuous sign language videos.

[Deepfakes](https://en.wikipedia.org/wiki/Deepfake) is a technique to replace a person in an 
existing image or video with someone else's likeness [@nguyen2019deep]. 
This technique can be used to improve the unrealistic face synthesis, resulting from not face-specialized models,
or even replace cartoon faces from animated 3D models. 

---

#### Pose-to-Gloss
Pose-to-Gloss---also known as sign language recognition---is the task to recognize a sequence of signs from a sequence of poses.

TODO

#### Gloss-to-Pose

Gloss-to-Pose---also known as sign language production---is the task to produce a sequence of poses that adequately represent
a sequence of signs written as gloss.

To produce a sign language video, @stoll2018sign constructs a lookup-table between glosses and sequences of 2D poses.
They align all pose sequences at the neck joint of a reference skeleton, and group all sequences belonging to the same gloss.
Then, for each group, they apply dynamic time warping and average out all sequences in the group to construct the mean pose sequence.
This approach suffers from not having an accurate set of poses aligned to the gloss, and from unnatural motion transitions between glosses.

To alleviate the downsides of the previous work, @stoll2020text2sign constructs a lookup-table of gloss to a group of sequences of poses rather than creating a mean pose sequence.
They build a Motion Graph [@min2012motion] - which is a Markov process that can be used to generate new motion sequences that are representative of real motion,
and select the motion primitives (sequence of poses) per gloss with the highest transition probability.
To smooth that sequence and reduce unnatural motion, they use Savitzky–Golay motion transition smoothing filter [@savitzky1964smoothing].


---

#### Video-to-Gloss
Video-to-Gloss---also known as sign language recognition---is the task to recognize a sequence of signs from a video.

For this recognition, @cui2017recurrent constructs a three-step optimization model.
First, they train a video-to-gloss end-to-end model, where they encode the video using a spatio-temporal CNN encoder, 
and predict the gloss using a Connectionist Temporal Classification (CTC) [@graves2006connectionist].
Then, from the CTC alignment and category proposal, they encode each gloss-level segment independently, trained to predict the gloss category,
and use this gloss video segments encoding to optimize the sequence learning model. 

@cihan2018neural fundamentally differ from that approach and opt to formulate this problem as if it is a natural-language translation problem.
They encode each video frame using AlexNet [@krizhevsky2012imagenet], initialized using weights that were trained on ImageNet [@deng2009imagenet].
Then they apply a GRU encoder-decoder architecture with Luong attention [@luong2015effective] to generate the gloss.
In follow-up work, @camgoz2020sign use a transformer encoder [@vaswani2017attention] to replace the GRU 
and use a CTC to decode the gloss. They show a slight improvement with this approach on the video-to-gloss task.

#### Gloss-to-Video
TODO

---

#### Gloss-to-Text
Gloss-to-Text---also known as sign language translation---is the natural language processing task of translating
between gloss text representing sign-language signs and spoken language text. 
These texts commonly differ by terminology, capitalization, and sentence structure.

@cihan2018neural experimented with various machine-translation architectures and compared between using an LSTM vs. GRU for the recurrent model,
as well as Luong attention [@luong2015effective] vs. Bahdanau attention [@bahdanau2014neural], and various batch-sizes. 
They concluded that on the RWTH-PHOENIX-Weather-2014T dataset, which was also presented by this work, 
using GRUs, Luong attention, and a batch size of 1 outperforms all other configurations.

In parallel with the advancements in spoken language machine translation, 
@yin2020better proposed replacing the RNN with a Transformer [@vaswani2017attention] encoder-decoder model, showing improvements on both
RWTH-PHOENIX-Weather-2014T (DGS) and ASLG-PC12 (ASL) datasets both using a single model, and ensemble of models.
Interestingly, in gloss-to-text they show that using the sign language recognition (video-to-gloss) system output outperforms using the gold annotated glosses.

Building on the code published by @yin2020better, @todo TODO show it is beneficial to pre-train these translation models
using augmented monolingual spoken langaugea corpora.  
They try three different approaches for data augmentation: 
(1) Back-translation; 
(2) General text-to-gloss rules, including lemmatization, word reordering, and dropping of words; 
(3) Language pair specific rules, that augment the spoken language syntax to its corresponding sign langauge syntax.
When pretraining, all augmentations show improvements over the baseline for both RWTH-PHOENIX-Weather-2014T (DGS) and NCSLGR (ASL). 


#### Text-to-Gloss
Text-to-gloss---also knows as sign language translation---is the task to translate between a spoken language text and sign language gloss.

@zhao2000machine used a Tree Adjoining Grammar (TAG) based system for translating between English sentences and American Sign Language glosses.
They parse the English text, and simultaneously assemble an American Sign Language gloss tree, using Synchronous TAGs [@shieber1990synchronous;@shieber1994restricting], 
by associating the ASL elementary trees with the English elementary trees, and associating the nodes at which subsequent substitutions or adjunctions can take place.
Synchronous TAGs have been used for machine translation between spoken languages [@abeille1991using] but this is the first application to a signed language.

For the automatic translation of gloss-to-text, @dataset:othman2012english identified the need for a large parallel sign language gloss and spoken language text corpus.
They develop a part-of-speech based grammar to transform English sentences taken from the Gutenberg Project ebooks collection [@lebert2008project] into American Sign Language gloss.
Their final corpus contains over 100 million sentences, and 800 million words, and is the largest English-ASL gloss corpus that we know of.
Unfortunately, only a small sample of this corpus is available online.

---

#### Video-to-Text
Video-to-text---also knows as sign language translation---is the entire task of translating a raw video to spoken language text.

@camgoz2020sign proposed a single architecture to perform this task, that can use both the sign language gloss and 
the spoken language text in joint-supervision.
They use the pre-trained spatial embeddings from @koller2019weakly to encode each frame independently, and encode the frames with a transformer.
On this encoding, they use a Connectionist Temporal Classification (CTC) [@graves2006connectionist] to classify the sign language gloss.
Using the same encoding, they also use a transformer decoder to decode the spoken language text one token at a time.
They show that adding gloss supervision improves the model over not using it, and that it outperforms previous video-to-gloss-to-text pipeline approaches [@cihan2018neural].

Following up, @camgoz2020multi propose a new architecture that does not require the supervision of glosses, called
"Multi-channel Transformers for Multi-articulatory Sign Language Translation".
In this approach they crop the signing hand, the face, and perform 3D pose estimation to obtain three separate data channels.
They encode each data channel separately using a transformer, then encode all channels together and concatenate the separate channels for each frame.
Like their previous work, they use a transformer decoder to decode the spoken language text, but unlike their previous work,
do not use the gloss as an additional supervision. 
Instead, they add two "anchoring" losses to predict the hand shape and mouth shape from each frame independently, 
as silver annotations are available to them using the model proposed in @koller2019weakly.
They conclude that this approach is on-par with previous approaches requiring glosses, 
and so they have broken the dependency upon costly annotated gloss information in the video-to-text task.


#### Text-to-Video
TODO

---

#### Pose-to-Text
Pose-to-text---also knows as sign language translation---is the task of translating a captured or estimated pose sequence to spoken language text.

@dataset:ko2019neural demonstrate impressive performance on the pose-to-text task by inputting the pose sequence into a
standard encoder-decoder translation network. 
They experiment both with GRU and various types of attention [@luong2015effective;@bahdanau2014neural], and with a Transformer [@vaswani2017attention],
and show similar performance, with the transformer underperforming on the validation set and overperforming on the test set which consists of unseen signers.
They experiment with various normalization scheme, mainly, subtracting the mean and dividing by the standard deviation of every individual keypoint
either with respect to the entire frame, or to the relevant "object" (Body, Face, and Hand).

#### Text-to-Pose
TODO https://arxiv.org/abs/2004.14874
TODO https://arxiv.org/pdf/2011.09846.pdf

---

#### Writing-to-$X$
As of 2020, there is no research discussing the translation task between a writing system to any other modality. 

#### $X$-to-Writing
As of 2020, there is no research discussing the translation task between any modality to a writing system.

---

```{=ignore}
#### Pose-to-Writing
TODO

#### Writing-to-Pose
TODO

---

#### Video-to-Writing
TODO

#### Writing-to-Video
TODO

---

#### Writing-to-Text
TODO

#### Text-to-Writing
TODO

---

#### Writing-to-Gloss
TODO

#### Gloss-to-Writing
TODO

```


### Fingerspelling 

Fingerspelling is the act of spelling a word letter-by-letter, borrowing from the spoken language alphabet [@battison1978lexical;@wilcox1992phonetics;@brentari2001language].
This phenomenon, found in most sign languages, often occurs when there is no previously agreed upon sign for a concept,
like in technical language, colloquial conversations involving names, conversations involving current events, 
emphatic forms, and the context of code switching between the sign language and corresponding spoken language [@padden1998asl;@montemurro2018emphatic].
The relative amount of fingerspelling varies between sign languages, and for American Sign Language (ASL) accounts for 12–35% of the signed content [@padden2003alphabet].

@patrie2011fingerspelled describe the following terminology to describe three different forms of fingerspelling:

- **Careful**---slower spelling where each letter pose is clearly formed.
- **Rapid**---quick spelling where letters are often not completed and contain remnants of other letters in the word.
- **Lexicalized**---a sign produced by often using no more than two letter-hand-shapes [@battison1978lexical].<br>
For example, lexicalized `ALL` uses `A` and `L`, lexicalized `BUZZ` uses `B` and `Z`, etc...

#### Recognition
Fingerspelling recognition--a sub-task of sign language recognition--is the task to recognize fingerspelled words from a sign language video.

@dataset:fs18slt introduced a large dataset available for American Sign Language fingerspelling recognition.
This dataset includes both the "careful", and "rapid" forms of fingerspelling, collected from naturally occurring videos "in the wild" which are more challenging than studio scenario.
They train a baseline model to take a sequence of images cropped around the signing hand, and either use an autoregressive decoder, or a CTC.
They found that the CTC outperforms the autoregressive decoder model, but both achieve very low recognition rate (35-41% character level accuracy) compared to human performance (around 82%).

In a followup work, @dataset:fs18iccv collected nearly an order-of-magnitude larger dataset, and designed a new recognition model.
Instead of detecting the signing hand they detect the face, and crop a large area around it. 
Then, they perform an iterative process of zooming in to the hand using visual attention, in order to retain sufficient information in high resolution of the hand.
Finally, like their previous work, they encode the image hand crops sequence, and use a CTC to obtain the frame labels.
They show that this method outperforms their original "hand crop" method by 4%, 
and that using the additional data collected they can achieve up-to 62.3% character level accuracy.
Looking through this dataset, we note that the videos in the dataset are taken from longer videos, and as they are cut, they do not retain the signing before the fingerspelling.
This context relates to language modeling, where at first one fingerspells a word carefully, and when repeating it, might fingerspell it rapidly, 
but the interlocutors can infer they are fingerspelling the same word.

#### Production

Fingerspelling production--a sub-task of sign language production--is the task to produce a fingerspelling video for words.

In its most basic form, "Careful" fingerspelling production can be trivially solved using pre-defined letter handshapes interpolation.
@adeline2013fingerspell demonstrates this approach for American Sign Language and English fingerspelling.
They rig a hand armature for each letter in the English alphabet ($N=26$) and generate all ($N^2=676$) transitions between every two letters using interpolation or manual animation.
Then, to fingerspell full words, they chain pairs of letter transitions.
For example, for the word "CHLOE", they would chain the following transitions sequentially: `#C` `CH` `HL` `LO` `OE` `E#`.

However, to produce life-like animations, one must also consider the rhythm and speed of holding letters, and transitioning between letters, 
as those can affect how intelligible fingerspelling motions are to an interlocutor (@wilcox1992phonetics).
@wheatland2016analysis analyzes both "careful" and "rapid" fingerspelling videos for these features. 
They find that for both forms of fingerspelling, on average, the longer the word, the shorter the transition and hold time.
Furthermore, they find that less time is spent on middle letters on average, and the last letter is held on average longer than the other letters in the word.
Finally, they use this information to construct an animation system using letter pose interpolation and control the timing using a data-driven statistical model.

```{=ignore}
## Citation

While work on this document is still ongoing, if you want to refer to it, please use the following bibtex:

```bibtex
@misc{moryossef2021slp, 
    title={Sign Language Processing}, 
    author={Moryossef, Amit},
    url={https://amitmy.github.io/sign-language-processing/}, 
    year={2021}
}
```


## References

gtag.html
