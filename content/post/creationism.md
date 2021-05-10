+++
title = "Against Creationism"

date = 2021-04-28T00:00:00
draft = true

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = []

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

summary = "A petty rant on the failure of attempts to understand machine learning models by looking only at inference time."

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true

+++


For centuries, Europeans agreed that the presence of a cuckoo egg was a great honor to a nesting bird, as it granted an opportunity to exhibit Christian hospitality. The devout bird enthusiastically fed her holy guest, even more so than she would her own (evicted) chicks (Davies, 2015). In 1859, Charles Darwin’s studies of another occasional brood parasite, finches, called into question any rosy, cooperative view of bird behavior (Darwin, 1859). Without considering the evolution of the cuckoo’s role, it would have been difficult to recognize the nesting bird not as a gracious host to the cuckoo chick, but as an unfortunate dupe.


Whether looking at parasitic brooding behavior or at the inner representations of a neural network, if we do not consider how a system develops, it is difficult to distinguish a pleasing story from a useful analysis. In NLP, how can we know if a pattern emerges as informative structure which is used by the model? Apparent syntactic patterns may well be vestigial effects from strategies early in training,[^1] or even side effects of training, input structure encodings with no bearing on the final predictions. We consider similarity (Chapter 4) and sparsity (Chapter 6) not at one checkpoint, but throughout training. We even illustrate how an LSTM’s training strategy makes it well-suited to hierarchical structured data (Chapter 5). These analyses lend a dimension to our understanding that is missing from the "creationist" view of a single checkpoint, manifested without history or evolution.

[^1]: For one origin story, see the Information Bottleneck Hypothesis.
