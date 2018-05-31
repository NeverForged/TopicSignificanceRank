# TopicSignificanceRank
### Goal
In order to determine the number of topics to use when applying LDA to a matrix of telemetry events from a video game, I searched through the literature for an nlp-independent (and human work independent) method for evaluating the topics of an LDA model to assess the number of topics.  Since the data I am using pertains to actions in a game (1700 different actions in [Minecraft: Education Edition](https://education.minecraft.net/), such as breaking a wooden block, opening [CodeConnection](https://education.minecraft.net/trainings/code-builder-for-minecraft-education-edition), or making something).  I have no semantics to run gensim cosine similarities between words, so I can't use coherence.  Log-Likliehoods and Perplexity seemed to just run off (see [this example](https://www.machinelearningplus.com/nlp/topic-modeling-python-sklearn-examples/#13compareldamodelperformancescores), but even had they gone with fewer topics, they may not have hit a maximum).  Using a statistic definition of 'Junk' topics makes sense, since I can run statistics, so I went with the method [described here](https://mimno.infosci.cornell.edu/info6150/readings/ECML09_AlSumaitetal.pdf).

### Writng the Code
- Opened up a git repo and started a Jupyter Notebook
- Hit Section 3 of [the paper](https://mimno.infosci.cornell.edu/info6150/readings/ECML09_AlSumaitetal.pdf) and added distributions.
- Section 4 led to the U, V, and B variables, as well as S1, S2, S, and Psi.
- Having no real method for determining Psi's in the paper, I computed the psi in S as '1' and the overall psi as the normalized Psi from the text.

### Testing the Code
- First, looking if it works (word frequency is not the best thing to look at, which makes sense)
- Comparison of TSR as a function of max_iter -> should get better as we add more iterations, so should show a difference as we get better.
- Comparison of TSR as a function of n_components -> Should be the same (or have local maxima/minima)
- create artifical good and bad models and check results.