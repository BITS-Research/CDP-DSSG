# CDP-DSSG

Council Data Project - Councils in Action for Data Science for Social Good

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
