---
layout: page
title: 🧠 🔐 2. Trial Decoding
description: Demo codes to decode event identity with 4 different methods. 
img: assets/img/publication_preview/rotation_trial.gif
importance: 2
category: Colab Notebook
toc:
  sidebar: left
---



The companion notebook will walk you through the steps of trial identity decoding form spiking data! 

🔗 Follow the demo code in Colab Notebook
[here](https://colab.research.google.com/drive/1D3BdR_TwraXgx7FEAUYx9MZkX5QEWjb1?usp=drive_link)! You will learn how to decode trial identity from population activity using four different methods!



---
# Part 1: How does UMAP work?

# Part 2: Supervised dimensionality reduction

In order to better visualize the trial-by-trial representation drift and check if the progression of population representation 
drift aligns with the order of the events, we took advantage of the [supervised dimensionality reduction feature of the UMAP](https://umap-learn.readthedocs.io/en/latest/supervised.html).

We plotted the result of supervised dimensionality reduction with UMAP and first colored it with linearized position (Fig. 1) and then
colored it with trial block number (Fig. 2).

<div class="l-page">
    <iframe src="{{ '/assets/html/demo/umap_supervised_pos.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="1000px" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Fig 1. An <mark>interactive</mark> plot showing the supervised UMAP embedding of the neural data when a mouse was running on the figure-8 maze.
(Left) UMAP embedding of population activity. Each point corresponds to the low-dimensional representation of
one binned spiking data. (Right) running trajectory of a mouse on the figure-8 maze.  Both the neural manifold and the running trajectory
were colored by the animal's linearized position. 
</div>

> ##### TIP!
> This is an interactive plot! You can rotate the manifold and examine the manifold from different angles!!
> This figure might take a few seconds to render! Try to rotate the interactive plot such that the manifolds for the early
> trials (blue ones) are at the bottom of the plot and the red manifolds are at the top.
{: .block-tip }



<div class="l-page">
    <iframe src="{{ '/assets/html/demo/umap_supervised_trial.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="1000px" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Fig 2. Similar to the previous plot, this <mark>interactive</mark> plot shows the supervised UMAP embedding of the neural data when a mouse was running
on the figure-8 maze.Both the neural manifold and the running trajectory were colored by trial block number. 
</div>


---

# Part 3: Trial decoding

To quantify the trial sequence information present in the state space, we tested if trial block membership can be 
accurately decoded from the population activity. 

Here we give a very high level overview of the main steps of UMAP.

Successive five trials composed a trial block, and a 
specific label was assigned to each trial block. Decoding was performed using a k-nearest neighbor (kNN) decoder. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="/assets/img/demo/2/UMAP_explain.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
    </div>
</div>
<div class="caption">
    Fig 3. Similar to the previous plot, this <mark>interactive</mark> plot shows the supervised UMAP embedding of the neural data when a mouse was running
on the figure-8 maze.Both the neural manifold and the running trajectory were colored by trial block number. 
</div>

# Part 4: Cross-validation with 'leaving one trial out'

For cross-validation, we used the standard 10-fold cross-validation as well as the more targeted 'leaving one trial out' method.
We want to highlight the 'leaving one trial out' cross-validation procedure here because we believe it is the most convincing evidence
that the population activity pattern varied systematically across trials. This is because as long as the different trial patterns are 
sufficiently differentiable, they can be decoded.  We need a method from which we can conclude beyond decodadability, but
can demonstrate that the variation is actually structured!

'Leaving one trial out' is such a method. To elaborate, 'leaving one trial out'  is expected to yield high decoding accuracy 
only if the state space of the data changed in a structured way, evolving along one axis according to the sequence of trial events.
This is because this validation method makes sure that the training set does not contain any data that shar the trial block 
membership with the test set, the test data could be decoded only to the next closest trial block (but not the same trial block) 
in the state space (Fig. 3 C). Note that the diagonal (red dashed line) of the confusion matrix had 0 decoding probability because the training and
test data did not share any data from the same trial block. Since the neural embedding was
structured according to the progression of trial events, the test data were correctly decoded to
their nearest neighbors.


<div class="row mt-3">
    {% include figure.liquid path="/assets/img/demo/2/validation_methods_github.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="caption">
    Fig 4. Leave entire trial block out validation results from four different decoding methods. 
</div>
{% details Click here to read the full figure legend. %}
(A) Illustration of the hold entire trial block out validation method. Top, neural manifold from all
the data in one example session. To give an example of the cross-validation procedure, data
from one trial block (trial block 4; blue) was highlighted. Middle, the highlighted trial block in
A was held out as test data. After removing the test data, a kNN decoder was trained only using
training data (grey). Bottom, the test data was then embedded with the learned manifold
(generated from training data), and the kNN decoder was used for trial block membership
decoding. Test data was decoded to the trial block label of its nearest neighbor (trial block 3)
on the training data manifold. Training data was gray and test data was colored by the identity
of the decoded trial block.

(B)
Illustration of the 10-fold cross-validation method. Top, neural manifold generated from all
the data in one example session. 10% of the data were highlighted (colored by their true trial
block identity). The highlighted data was held out as test data. Middle, after removing the t est data,
a kNN decoder was trained only using training data (grey). Bottom, embedding the test
data with the training manifold and us ing the kNN decoder for trial block identity decoding.
Training data was gray and test data was colored by the identity of the decoded trial block (trial
block 3).

(C) Confusion matrix obtained using hold entire trial block out validation. Note that the diagonal
(red dashed line) of the confusion matrix had 0 decoding probability because the training and
test data did not share any data from the same trial block. Since the neural embedding was
structured according to the progression of trial events, the test data were correctly decoded to
their nearest neighbors.

(D) Confusion matrix from UMAP trial block decoding using hold entire trial block out validation.
{% enddetails %}

---



# Part 5: Decoding from the original high-dimensional space and PCA space

Can we trust the decoding result based on uMAP embedding? We know that dimensionality reduction can potentially distort the 
relationship between data points in the original dimensional space. In order to make sure our conclusion is not the result of
potential distortion during the dimensionality reduction process, we repeated the KNN decoding and leave one out cross validation 
procedure from the original high-dimensional space (Fig. 4 B and C) as well as PCA space (Fig. 4A).

<div class="row mt-3">
    {% include figure.liquid path="/assets/img/demo/2/validation_methods_other_github.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="caption">
    Fig 5. Confusion matrix of trial block decoding results.
</div>

As we can see, all those methods yield consistent conclusion with UMAP.


---

# Part 6: Can we use UMAP for trial decoding?
Does UMAP introduce any distortion that could affect accuracy of the trial decoding results? In oder to demonstrate that we
could use UMAP for trial decoding, we need to demonstrate that the trial block membership is consistent between the high and low-dimensional
space.

<div class="row mt-3">
    {% include figure.liquid path="/assets/img/demo/2/decoding_high_low.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="caption">
    Fig 6. Consistent trial block membership between the low-dimensional and the original high-dimensional space.
</div>
{% details Click here to read the full figure legend. %}
(A) Diagram explaining the main steps of trial block decoding from the original high -dimensional
space. Step 1: by default, a weighted nearest neighbor (kNN) graph, which connects each
datapoint to its nearest neighbors, was constructed and used to generate the initial topological
representation of the training dataset (dots in three different colors). Step 2: the trial block
membership of the test dat a (purple triangle) was decoded by taking the mode of its k nearest
neighbors. For example, the example test data point (purple triangle) was decoded to be trial
block 3 because all of its three nearest neighbors in the original high-dimensional space belong to trial block 3 (purple).

(B) Diagram explaining the main steps of trial block decoding from the low
-dimensional space generated by UMAP. Step 1 was the same as in panel (A). Step 2: optimize the low
-dimensional representation to preserve the topological representation as much as possible to
that in the original high-dimensional space. Step 3: The trial block membership of the test data
(purple triangle) was decoded by taking the mode of its nearest neighbors in the low -dimensional embedding. For example, 
the example test data point (purple triangle) was decoded to be trial block 3 because all its three nearest neighbors in the low
-dimensional space belong to trial 3 block (purple).
{% enddetails %}


---


# Part 7: Can electrode drift explain what we see?

<div class="row mt-3">
    {% include figure.liquid path="/assets/img/demo/2/stationary.png" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>
<div class="caption">
    Fig 7. Assessment of single-unit stability over time.
</div>
{% details Click here to read the full figure legend. %}
(A) Waveform amplitude over time (on-maze duration) for all the cells in an example session. Spikes of
individual neurons are color-coded by amplitude. The spike amplitude value was extracted from Amplitudes.npy,
which was generated by Kilosort/Phy. It is a measure of each spike's amplitude in the template space.

(B) Scatter plot of waveform amplitude in the first quarter of on- maze recording compared to the last quarter ,
for all the isolated units from the entire figure- 8 maze dataset (Pearson correlation coefficient, N = 4469 cells from 6 animals).

(C) Single-unit waveform centroid displacement across time, from a representative session , plotted in 3-D space. Centroid
was computed by taking the spatial average across electrode positions weighted by the squared mean waveform amplitude at 
each electrode (see Methods for details). Waveform centroid for each single unit during the first quarter (blue circles) 
and last quarter of recording (red triangles) were connected by red lines (note: most of them were very short and not visible). 
The large semi-transparent orange and blue circles indicate the positions of the dual-sided probe’s 128 electrode sites (blue, and
orange, front and back sides of the dual-sided probe, respectively).

(D) Cumulative distribution of unit centroid displacement between the first and the last quarter of maze
recording for all the cells in the dataset (median = 2.81- um, Q1 = 1.37- um, Q3 = 5.46- um; N= 4469 cells from 6 animals).

{% enddetails %}

---
# How to cite us ? 

Enjoyed reading this post and found our demo code useful? It can be cited as follows:

Wannan Yang, Chen Sun, Roman Huszár, Thomas Hainmueller, Kirill Kiselev, György Buzsáki. 
"Selection of experience for memory by hippocampal sharp wave ripple." _Science_ (2024).


