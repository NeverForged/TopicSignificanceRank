# TopicSignificanceRank
### Goal
In order to determine the number of topics to use when applying LDA to a matrix of telemetry events from a video game, I searched through the literature for an nlp-independent (and human work independent) method for evaluating the topics of an LDA model to assess the number of topics.  Since the data I am using pertains to actions in a game (1700 different actions in [Minecraft: Education Edition](https://education.minecraft.net/), such as breaking a wooden block, opening [CodeConnection](https://education.minecraft.net/trainings/code-builder-for-minecraft-education-edition), or making something).  I have no semantics to run gensim cosine similarities between words, so I can't use coherence.  Log-Likliehoods and Perplexity seemed to just run off (see [this example](https://www.machinelearningplus.com/nlp/topic-modeling-python-sklearn-examples/#13compareldamodelperformancescores), but even had they gone with fewer topics, they may not have hit a maximum).  Using a statistic definition of 'Junk' topics makes sense, since I can run statistics, so I went with the method [described here](https://mimno.infosci.cornell.edu/info6150/readings/ECML09_AlSumaitetal.pdf).

### Writng the Code
- Opened up a git repo and started a Jupyter Notebook
- Hit Section 3 of [the paper](https://mimno.infosci.cornell.edu/info6150/readings/ECML09_AlSumaitetal.pdf) and added distributions.
- Section 4 led to the U, V, and B variables, as well as S1, S2, S, and Psi.
- Psi was the biggest challenge.  Paper was vague, especially with regards to the weights in the Psi equation.  Ended up setting them all to 1/3, to avoid over-filtering based on number of topics (since this is intended to be a way to determine the optimal number of topics)

### Testing the Code
- First, looking if it works (word frequency is not the best thing to look at, which makes sense)
- Next, compare log-likliehood, perplexity, Psi, S, and TSR for a model.