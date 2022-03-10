# CDP-DSSG

Council Data Project - Councils in Action for Data Science for Social Good

**Preliminary Feedback / Questions**

- Whether a subset of the dataset will be labeled in advance or if students themselves will be doing any manual labeling
- Preliminary modeling attempts and results
- Criteria / constructs used for ideology labeling
- Potential impacts on individual legislators as a result of this work; dynamics and impact of this work may vary greatly from the Supreme Court context

We address each of these below. 

## Annotation and Classification

> How much annotation will students or we need to do to begin work on an
> interruption classifier?

A few methods for quickly setting up _some_ dataset for training a classifier
(or to use as a comparison).

### Pattern Matching

Match on sentence starting or ending patterns, i.e.:

```
"Wait,..."
"Hold on,..."
"Sorry,..."
"...--"  # potentially labeled by stenographer
```

This definitely will not include all interruption behaviors but it can
act as a starting point from a pure text view.

### Low Confidence Speaker Annotation

We recognize that when speaker interruption occurs, the transcript may not
actually record the overlapping words in the sentence data.

Looking to the audio, we can attempt to use the trained speaker classification
model as a method for identifying crosstalk. For example, when a
council member talks over another council member, our model _should_ have
lower confidence than our threshold requirement to properly label the
speaker and potentially have similar confidence for multiple known speakers:

i.e. for us to label a sentence with a known speaker we require a model
confidence of 0.98 but the model may have confidence values for the
speaker labels of `"speaker_1": 0.73, "speaker_2": 0.71`

However, this method, because we only train a model for elected official
annotation, would fail if a public commenter or presenter are the interrupter
or interruptee.

### Annotation Storage

Regardless of strategy for bootstrapping the dataset, there should be a
manual review of the dataset to ensure the labels are accurate.

Additionally, it may be useful to store the context of interruption.
For example, is the interruption a clarification / quick question, or simply
overtalking and domineering behavior.

Finally, as noted in the Low Confidence Speaker Annotation method, the storage
of these annotations should likely not be on the "sentence level" but rather
stored as an independent list of interruption times stored in the "transcript
annotations" block.


### Preliminary modeling attempts and results 


### Criteria / constructs used for ideology labeling
This is admittedly a challenging classification task. Elected officials at the municipal level often do not have an affiliation with a political party (though not always). For the municipalities we have identified three have no party and two have party affiliations: 
- - Boston - formal party identification 
- - Seattle - no formal party identification 
- - Portland - no formal party identification 
- - DC - formal party identified
- Oakland - no formal party identified

For cities with no formal party identification, there exist other valuable proxies for their political ideologies: 
- Many elected officials have served in a previous capacity where they have formally declared a party. For example https://www.portland.gov/hardesty/meet-jo-ann previously served as a Democrat in the Oregon State Legislature 
- Ballotopedia has a questionnaire where candidates answer specifically about their political philosophy e.g https://ballotpedia.org/Nikki_Fortunato_Bas 
- And most politicians are members of a political party - whether or not they formally use that affiliation in their governing it is a valuable piece of data

The Councils-in-Action dataset will include metadata about each elected official that serves on a city council, their age, tenure, district served, and a political ideology estimate with a confidence rating. 

### Potential impacts on individual legislators
There are potential benefits and harms to increasing the transparency of city council deliberations, and we acknowledge that the results of this work may focus attention on elected officials. But, we argue that this is an important part of their elected duties - being held accountable for actions, even subtle and unintentional actions, that shape the structure and outcomes of a debate. Shedding light on these processes, and the impacts that individuals have in decisionmaking contexts is, overall, a net positive. 
