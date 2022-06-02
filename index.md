## Be With You (与你同在)
Music is better than words, please enjoy:

<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/1279451359&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe><div style="font-size: 10px; color: #cccccc;line-break: anywhere;word-break: normal;overflow: hidden;white-space: nowrap;text-overflow: ellipsis; font-family: Interstate,Lucida Grande,Lucida Sans Unicode,Lucida Sans,Garuda,Verdana,Tahoma,sans-serif;font-weight: 100;"><a href="https://soundcloud.com/user-275952960-599169161" title="Jiatong" target="_blank" style="color: #cccccc; text-decoration: none;">Jiatong</a> · <a href="https://soundcloud.com/user-275952960-599169161/be-with-you" title="Be with you (与你同在)" target="_blank" style="color: #cccccc; text-decoration: none;">Be with you (与你同在)</a></div>

## Motivation and Highlights

Our song creation stems from our thinking about the relationship between humans and artificial intelligence (AI), which was originally designed to support humans by providing assistance with simple problems. However, with the continuous development, we expect that AI will eventually be able to deeply understand human beings and share pleasure with human beings. We imagine this future in our song, which is born through a combination of various deep learning algorithms and in-depth collaboration with humans.

The highlights are as follows:
- We explore extensive collaborations between humans and AI in three aspects: melody generation, lyrics generation, and singing voice synthesis. 
- We apply AI algorithms to push our performance limits, which we cannot achieve alone. 
- We emphasize the diverse perspective of different groups within both the creation and performance of our song.

## Workflow, Collaboration, and Songwriting Process
### General workflow
Our song creation process includes three general stages: Lyric & Theme Generation, Music Score Preparation, and Music Production. They are conducted in sequential order, as shown in Figure 1. In Lyric & Theme generation stage, the lyric generation and theme generation models iteratively refine the lyrics and their corresponding theme with the help of the general public. Then, lyrics-theme pairs are expanded with a melody generation model, and are further polished in the second music score preparation stage. For the last stage, the music score is passed to the music production team and several singing synthesis models to produce the final song. Note that humans and AI models are highly collaborative in all three stages.

![image](https://user-images.githubusercontent.com/22814472/171135232-39e75f22-03ae-43f4-a489-bec3e0b22785.png)

### Detailed workflow

Given the general workflow defined in Section 3.1, our detailed workflow for each stage is illustrated in Figure 2 below. In all the three stages, AI models (i.e., orange blocks), musical specialists (i.e., yellow blocks), and general public (i.e., blue blocks) are interconnected.

![image](https://user-images.githubusercontent.com/22814472/171136309-e0d0dfe9-cab5-4d69-9082-89641eb68a62.png)


#### Lyric & theme generation (first stage)

For the first stage, we first apply a pre-trained lyric generation model (i.e., a neural language model) to generate N short lyrics samples based on some key words  that are randomly inserted given the lengths of sentences. Then, we invite the general public to vote on the generated lyrics samples through social media (i.e., WeChat). The voting helps us to narrow down the major concepts that we want to convey in the song. Afterwards, we extract format information, namely rhythm template, from the lyrics. Given the rhythm template, we apply a theme generation model that can generate the corresponding musical theme from the given lyrics. Initially, the music theme generation is not stable because of the limited amount of open-source, Mandarin, annotated data. Therefore, our team invite musical professionals to go over thousands of open-accessible Mandarin Pop songs and annotate them with related structure information (e.g., intro, verse, chorus, etc.). With the introduction of the fine-grained annotated data, we observe a much more reasonable melody from the model. 

As this procedure does not directly involve any semantic information but only the prosody information, the theme generation could potentially generate more diverse themes. Therefore, we further use the power of the crowd (i.e., voting) to find a reasonable match. 

#### Music score preparation (second stage)
Given the matched lyrics and music theme, we further produce the melody for the whole song using a melody generation model, which was trained on our fine-grained dataset. Similarly, we conduct the voting to achieve a balance between musical advisors and public taste. With our musical advisors, the music arranger and the songwriter in our team re-organize the matched melody and lyrics into a full music score. We initially expect the song to be performed in solo. However, as we realize several insights from the generated melody and limitation in performances with a single singer, we decide to use a duet-format with both male and female singers. 

#### Music production (second stage)
Because of regional regulations, it is difficult to acquire enough resources (e.g., available singers, recording studios, and musical instrument players). In the music production stage, we minimize the dependency in song production by mostly using the available sources. For musical instruments, we mainly use the available materials from Logic, Kontakt, and Sibelius. Meanwhile, we also use several singing voice synthesis (SVS) models to construct the first demonstration. With neural networks, we can generate reasonable singing voices, but sometimes, it still suffers from rigid performances. To tune outputs from SVS models, we also use a parametric vocoder to allow a visualization over pitch contour in singing voices. This enables even general public to modify the voice for naturalness. In general, the process allows quite fast iterations and remote collaboration overseas.

For the final production, we use both human voices and AI-synthesized voices in the duet and conduct music mixing for better performance.

## Human-AI collaboration
- In the first stage, we interact with AI models by voting and extra music structural information based on musical expertise. The voting procedure iterates through several rounds. During the iteration, we not only detect some model training issues from engineer perspective, but also some musical issues from musical aspects, which could be either polished by better human knowledge injection to the model, or by musical specialists directly. Meanwhile, AI models also bring several insights which cannot be easily brought up without them. In this stage, we don’t just apply machine learning models, we also expect to communicate with them musically..
- In the second stage, the collaboration between AI and humans is more straightforward: the music arranger and the songwriter modify the results from AI models. The primary reason is that we still observe a lack of structure in the generated music score, though we already emphasize the structural information in model training and design. With the help of musicians, we further formulate the structure of generated results to reduce the flatness problem in AI-oriented music generation.
- In the third stage, deep learning based SVS models fasten the iteration of music production and lower the threshold for general public to participate into the creation. In conventional concatenative singing synthesis, the naturalness can be assured but with sacrifice to limited singer availability and requirements for users to be familiar with music bases. But with more recent algorithms, we can directly get almost natural singing without too much professional knowledge and skills in music production toolboxes. However, to get more natural singing, we still need to tune some parts of the music score and pitch contours. Another point worth mentioning is that SVS models in fact pushing our limits in musical performances. Due to limited resources, we could not find a suitable singer to sing the second part of the song. However, with the SVS model, we can easily get a high-quality singing voice without worrying about looking for professional singers.

## AI Models
For lyrics generation, we adopt T5 , a pretrained sequence-to-sequence language model and finetune it in SongNet framework . In addition, we introduce extra music information, such as rhythm patterns in lyrics, to generate with fine-grained formats and better content control. This suggests a preliminary verse/chorus structure for the generated lyrics. This model is a unified model for any inputs with rhythm information. Therefore, we also use the model to generate lyrics from human modified melody to achieve feedback loop as illustrated in the first stage (i.e., Lyric & theme generation) of Figure 2. More technical details will be released in other technical conferences. 
For both theme generation and melody generation, we use TeleMelody  to generate the melody condition on lyrics. This model employs rhythm template as the bridge between lyrics and melody. As it would result in melody-lyrics alignment automatically, we use the model for our conditional theme and melody generation (as illustrated in Figure 2).
For singing synthesis models, we produce our music with ACE Singer  based on RefineGAN  and use Bytesing V3  for acoustic modeling. 

## Diversity, Ethical, and Cultural Considerations
We care about diverse perspectives in cultural, gender, and musical backgrounds, respectively.
- Culture perspective: We emphasize our effort in cultural perspective in both language and music design. 
  - Language selection: We observe that the contests in 2020 and 2021 are mostly in either instrumental or English. Meanwhile, most open-source music & NLP AI algorithms and models, if using natural languages, are always based on English. Therefore, in our project, we design the whole pipeline in Mandarin, including training, evaluation, and finetuning of our AI models. Though suffering from limited resources, we expect to share our voice with people worldwide.
  - Music style: apart from music genres of Pop, Blues, R&B, and Hip-hop, we manage to train our AI model by introducing Chinese songs with Chinese traditional instruments and pentatonic scale.
- Gender perspective: For the gender aspect, we initially set the song as an ensemble of males and females. The ensemble voices provide our song creation with the maximum potential.
- Musical background perspective: All our team members believe that music should be without barriers, especially for those without formal music education. We anticipate a future when everyone with or without musical background can not only enjoy the music but also participate in various steps of music creation. Towards this hope, we conduct the music created by interacting with people with different background knowledge.

## Lyrics
|     Singer                                                       |     AI                                                          |
|------------------------------------------------------------------|-----------------------------------------------------------------|

|     世界曾寂静得一如既往(The   world was as silent as ever)      |                                                                 |
|     直到你在我身旁   (Until you are by my side)                  |                                                                 |
|     生命便倔强得无人可挡   (Life is stubborn and unstoppable)    |                                                                 |
|     你就是我的翅膀 (But   you are my wings)                      |                                                                 |
|                                                                  |     你带我去远方 (You take me far away)                         |
|                                                                  |     陪我穿越时空 哦 (Through time and   space, oh)              |
|                                                                  |     我听见你在唱 (I hear you singing)                           |
|                                                                  |     着未来如你所想 (The   future is as you think)               |
|     带我穿过迷惘 (Take me through   confusion)                   |     带我穿过迷惘 (Take me through   confusion)                  |
|     未知染上了渴望 (The   unknown is infected with desire)       |     未知染上了渴望 (The   unknown is infected with desire)      |
|     释放我想象 (Release my   imagination)                        |     释放我想象 (Release my   imagination)                       |
|     未来不同寻常 (Future will be   unusual)                      |     未来不同寻常 (Future will be   unusual)                     |
|     带我告别惆怅 (Take me goodbye to   melancholy)               |     带我告别惆怅 (Take me goodbye to   melancholy)              |
|     时间洒满了希望   (Time is full of hope)                      |     时间洒满了希望   (Time is full of hope)                     |
|     世界的万象 (Everything in the   world)                       |     世界的万象 (Everything of the   world)                      |
|     咫尺可及的力量   (Power at our fingertips)                   |     咫尺可及的力量   (Power at our fingertips)                  |
|     就在我手掌 (Are in our palm)                                 |     就在我手掌 (Are in our palm)                                |
|     -----                                                        |     -----                                                       |
|     世界曾寂静得一如既往(The   world was as silent as ever)      |                                                                 |
|     直到你在我身旁   (Until you are by my side)                  |                                                                 |
|     生命便倔强得无人可挡   (Life is stubborn and unstoppable)    |                                                                 |
|     你就是我的翅膀 (But   you are my wings)                      |                                                                 |
|     带我穿过迷惘 (Take me through   confusion)                   |     过迷惘 (Through confusion)                                  |
|     未知染上了渴望(The   unknown is infected with desire)        |     未知染上了渴望 (The   unknown is infected with desire)      |
|     释放我想象 (Release my   imagination)                        |     我想象 (My imagination)                                     |
|     未来不同寻常 (Future will be   unusual)                      |     未来并不同寻常   (Future will not be usual)                 |
|     带我告别惆怅 (Take me goodbye to   melancholy)               |     啦 (La)                                                     |
|     时间洒满了希望   (Time is full of hope)                      |     啦啦 (Lala)                                                 |
|     世界的万象 (Everything of the   world)                       |     啦 (La)                                                     |
|     咫尺可及的力量   (Power at our fingertips)                   |     啦 (La)                                                     |
|     就在我手掌 (Are in our palm)                                 |     啦 (La)                                                     |
|                                                                  |     跟着我跟着我 (Follow me, follow me)                         |
|     去探索 (To explore)                                          |     去浩瀚世界去探索 (To   explore the vast world)              |
|                                                                  |     听我说听我说 (Listen to me, listen   to me)                 |
|     回忆也会更深刻   (Memories will be deeper)                   |     回忆也会更深刻   (Memories will be deeper)                  |
|     怀念的梦想的 (Missing and dreaming)                          |     怀念的梦想的 (Missing and dreaming)                         |
|     每一天都能叫醒耳朵   (Wake up your ears every day)           |     每一天都能叫醒耳朵   (Wake up your ears every day)          |
|     啦啦啦啦 (Lalalala)                                          |     告诉我告诉我 (Tell me tell me)                              |
|     你还想去体会什么   (What else do you want to experience)     |     你还想去体会什么   (What else do you want to experience)    |
|     带我穿过迷惘 (Take me through   confusion)                   |     过迷惘 (Through confusion)                                  |
|     未知染上了渴望 (The   unknown is infected with desire)       |     未知染上了渴望 (The   unknown is infected with desire)      |
|     释放我想象 (Release my   imagination)                        |     释放我想象 (Release my   imagination)                       |
|     未来不同寻常 (Future will be   unusual)                      |     未来不同寻常 (Future will be   unusual)                     |
|     带我告别惆怅 (Take me goodbye to   melancholy)               |     带我告别惆怅 (Take me goodbye to   melancholy)              |
|     时间洒满了希望   (Time is full of hope)                      |     时间洒满了美好希望   (Time is full of beautiful hope)       |
|     世界的万象 (Everything of the   world)                       |     世界的万象 (Everything of the   world)                      |
|     咫尺可及的力量   (Power at our fingertips)                   |     咫尺可及的力量   (Power at our fingertips)                  |
|     就在我手掌 (Are in our palm)                                 |                                                                 |


## Our team

The AIM3 team is a joint team with both musical specialists and AI researchers. The passion for music and computer algorithms brought us together across the Pacific Ocean from various backgrounds. Our team members are primarily from academic institutions. Some are also from the musical, technical or financial industries.

### Team members

Jiatong Shi (Producer & AI researcher, Carnegie Mellon University)

Hang Yin (Music arranger & Songwriter, Xi’an Lingxin Culture Media)

Tao Qian (AI engineer, Renmin University of China & ByteDance AI Lab SA)

Keyi Zhang (Songwriter, Zhonghe Capital)

Yuning Wu (AI engineer and imaginary designer, Renmin University of China)

Shuai Guo (AI engineer, Renmin University of China)

Zhaodong Yao (Musical advisor, Tottori University)

Huazhe Li (Musical advisor, Tsinghua University)

Peter Wu (Technical advisor, University of California, Berkeley)

Qin Jin (General advisor, Renmin University of China)

