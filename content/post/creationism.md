+++
title = "Interpretability Creationism"

date = 2021-07-28T00:00:00
draft = true

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = []

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

summary = "Nothing in Deep Learning Makes Sense Except in the Light of SGD."

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

<img src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Reed_warbler_cuckoo.jpg" alt="By Per Harald Olsen - Own work, CC BY-SA 3.0" width="200"/>



Certainly SGD is not literally evolution, but post-hoc analysis in machine learning [has a lot in common](https://twitter.com/ch402/status/1533164918886703104) with scientific approaches in biology, and likewise requires an understanding of the origin of model behavior. Therefore, the following holds whether looking at parasitic brooding behavior or at the inner representations of a neural network: if we do not consider how a system develops, it is difficult to distinguish a pleasing story from a useful analysis.

We have many pleasing [just-so stories](https://en.wikipedia.org/wiki/Just_So_Stories) in NLP. Much has been made of interpretable artifacts such as [syntactic attention distributions](https://aclanthology.org/2022.acl-long.269.pdf) or [sentiment neurons](https://openai.com/blog/unsupervised-sentiment-neuron/). How can we know if such a pattern of behavior is actually used by the model?
Causal modeling can help, but interventions to test the influence of particular features and patterns may target only particular types of behavior explicitly. In practice, it may be possible only to perform certain types of slight interventions on specific units within a representation, failing to reflect interactions between features properly. Furthermore, in staging these interventions, we create distribution shifts that a model may not be robust to, regardless of whether that behavior is part of a core strategy. Significant distribution shifts can cause erratic behavior, so why shouldn't they cause spurious interpretable artifacts?

The study of evolution has provided a number of ways to interpret the artifacts produced by a model. They might be vestigial, like a human tailbone. They may have dependencies, with some features and structures relying on the presence of other properties earlier in training, like the requirement for light sensing before a complex eye can develop. Some artifacts might represent side effects of training, like how junk DNA constitutes a majority of our genetic code without influencing our phenotypes.

We have a number of theories for how such unused artifacts might emerge while training models. For example, the [Information Bottleneck Hypothesis](https://arxiv.org/abs/1703.00810) predicts how inputs may be memorized early in training, before representations are compressed to only retain information about the output. These early memorized interpolations may not ultimately be useful when generalizing to unseen data, but they are essential in order to eventually learn to specifically represent the output. We also can see the possibility of vestigial features, because early training behavior is so distinct from late training: [earlier models are more simplistic](http://arxiv.org/abs/1905.11604). In the case of language models, they [behave similarly to ngram models](http://arxiv.org/abs/2109.06096) early on and [exhibit linguistic patterns](https://www.aclweb.org/anthology/2020.emnlp-main.16) later.

While I may be unimpressed by explanations of static fully trained models, I have engaged in similar analysis myself. I've published papers on [probing static representations](https://arxiv.org/pdf/2010.02180.pdf), and the results often seem intuitive and explanatory. However, the presence of a feature at the end of training is hardly informative about the inductive bias of a model on its own! Consider [Lovering et al.](https://openreview.net/forum?id=mNtmhaDkAr), who found that the ease of extracting a feature at the start of training, along with an analysis of the finetuning data, has deeper implications for finetuned performance than we get by simply probing at the end of training.

One example of an explanation based on static models is [syntactic hierarchical behavior](https://nlp.stanford.edu/pubs/hewitt2019structural.pdf). How can we know that model strategy reflects a hierarchy, rather than showing stronger local behavior because the correlations between nearby words happened to be stronger? For example, perhaps constituents like "football match" are more predictable due to the frequency of their co-occurrence, compared to more distant relations like that between "uncle" and "football" in the sentence, "My uncle drove me to a football match". In fact, we can be more confident that some language models are hierarchical, because early models encode more local information in [LSTMs](https://arxiv.org/abs/1811.00225) and [Transformers](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#argument-phase-change), and they learn longer distance dependencies more easily when those dependencies can be [stacked onto short familiar constituents](https://arxiv.org/abs/2010.04650) hierarchically.

I recently had to manage the trap of static explanations myself. My coauthors had found that, when training text classifiers repeatedly with different random seeds, [models can occur in a number of distinct clusters](https://arxiv.org/abs/2205.12411). Further, we could predict the generalization behavior of a model based on which other models it was connected to on the loss surface. Now, we suspected that different finetuning runs could find models with different generalization behavior because their trajectories entered different basins on the loss surface. But was this really a claim we could make? What if some of the basins actually corresponded to earlier stages of a model. Eventually those models would leave for the basin with better generalization, so our only real result would be that some finetuning runs were slower than others. We had to confirm that training trajectories could actually become trapped in a basin, providing an explanation for the diversity of generalization behavior in trained models. Indeed, when we looked at several checkpoints, we did find that models that were very central to the bad-generalization cluster would become *even more* deeply connected to other poorly generalizing models over the course of training. Instead of offering a just-so story, we explored the evolution of observed behavior to confirm our hypothesis.

![k](/img/clusters.png)

My proposal is simple. Are you developing a method of interpretation or analyzing some property of a trained model? Don't just look at the end of training. Apply that analysis to several checkpoints. If you are finetuning a model, check several points both early and late in training. If you are analyzing a large language model, [MultiBERTs](https://arxiv.org/abs/2106.16163) and [Mistral](https://nlp.stanford.edu/mistral/getting_started/download.html) both provide intermediate checkpoints sampled from throughout training on masked and autoregressive language models, respectively. Does the behavior that you've analyzed change over the course of training? Does your belief about the model's strategy actually make sense after observing what happens early in training? There's very little overhead to an experiment like this, and you never know what you'll find!
