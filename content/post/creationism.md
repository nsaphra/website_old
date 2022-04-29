+++
title = "Interpretability Creationism"

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


For centuries, Europeans agreed that the presence of a cuckoo egg was a great honor to a nesting bird, as it granted an opportunity to exhibit Christian hospitality. The devout bird enthusiastically fed her holy guest, even more so than she would her own (evicted) chicks [(Davies, 2015)](https://app.thestorygraph.com/books/37ed3b62-8a3a-448b-9e37-cd5e5f51c640). In 1859, Charles Darwin’s studies of another occasional brood parasite, finches, called into question any rosy, cooperative view of bird behavior [(Darwin, 1859)](https://app.thestorygraph.com/books/44185106-8198-42ef-bacf-8a9bf691e654). Without considering the evolution of the cuckoo’s role, it would have been difficult to recognize the nesting bird not as a gracious host to the cuckoo chick, but as an unfortunate dupe. The historical process is essential to understanding its biological consequences; as evolutionary biologist Theodosius Dobzhansky put it, [Nothing in Biology Makes Sense Except in the Light of Evolution](https://en.wikipedia.org/wiki/Nothing_in_Biology_Makes_Sense_Except_in_the_Light_of_Evolution#cite_note-Dobz_Nothing-1).


Whether looking at parasitic brooding behavior or at the inner representations of a neural network, if we do not consider how a system develops, it is difficult to distinguish a pleasing story from a useful analysis. In NLP, much has been made of the syntacticity or interpretability of attention distributions (). How can we know if a pattern of behavior is actually used by the model? Causal modeling () can help, but interventions to test the influence of particular features and patterns may target only certain behavior explicitly, but in doing so they create distribution shifts that a model may not be robust to, regardless of whether that behavior is part of a core strategy. Apparent syntactic patterns may well be vestigial effects from strategies early in training (perhaps formed prior to a [phase shift](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#argument-phase-change)). They may even constitute side effects of training[^1], input structure encodings with no bearing on the final predictions, if they had only been removed earlier on.

[^1]: For one origin story, see the [Information Bottleneck Hypothesis](https://arxiv.org/abs/1703.00810).
