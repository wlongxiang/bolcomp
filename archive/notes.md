# Old Notes

We tried to learn a multimodal classifier in this way: first, learn a separate text classifier
using only the two text columns (title and description), then we predict the probability
of each training sample, in the end we get two probabilities as outputs (for label Y and label N)
, in turn these two probabilities are concatanated to the original features to
train autogluon stacking models. We do the same for images.

What we found is: this way does not improve the final validation acc. This could be
due to: 1) the image/text classifier are overfitted. In fact, the text classifier
reports around 0.9+ accu. This causes the AG model to report insane acc. as high as 
0.94. This is easy to fathom because the model can just use the score by image/text classifier
to "cheat".

Then we also go on to use the text embeddings as features. It also turns out to overfit easily.

In th end, the sota is just with binary features, and more folds (20 folds x 2 fold sets).
Though we train with addition 3 layers of stacking (makes 5 in total), the best performing
one is on L3 ensemble, which could have been produced by the default stacking layer.

- `data/featurizd/V2` contains binary features (has_title, has_desc, has_image_url), plus
the text embeddings extracted from text predictor. Note: useless cols (globalID, etc.) are dropped.

- `data/featurizd/V1` contains binary features (has_title, has_desc, has_image_url), plus
  the text/image classifier output probabilities. Note: useless cols (globalID, etc.) are dropped.
  
