---
layout: about
title: About
permalink: /
news: false # includes a list of news items
paper: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---
Wannan Yang<sup>1,3</sup>, Chen Sun<sup>2</sup>, Roman Huszár<sup>1,3</sup>, Thomas Hainmueller<sup>1,4</sup>, Kirill Kiselev<sup>3</sup>, György Buzsáki<sup>1,3*</sup>

Affiliations:

1.Neuroscience Institute and Department of Neurology, NYU Grossman School of Medicine, New York University, New York, USA,
2.Mila - Quebec AI Institute, Montréal, Canada,
3.Center for Neural Science, New York University, New York, USA,
4.Department of Psychiatry, New York University Langone Medical Center, New York, USA  


---


How does the brain select what to consolidate during sleep? Our new work sheds light on the brain's mechanism for memory.
We propose that awake ripples act as a memory tag 🏷️-- the memories that are tagged by awake ripples are consolidated during sleep!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/about/cartoon_github.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">

</div>

Using dual sided probes, we were able to record up to 500 neurons simultaneously while animal perform an alternation task on the figure-8 maze.


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/task_3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

UMAP visualization revealed that population activity of the hippocampus corresponded to a latent space that topologically
resembled the physical environment. This visual, though beautiful, was not surprising since hippocampus is known to keep
a ‘cognitive map’ of the world. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/pos_manifold_4.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


What was really unexpected was when we colored the neural manifold by trial number, we  saw the hippocampal states systematically 
vary according to trial sequence.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/trial_manifold_5.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


As per Heraclitus, “No man ever steps in the same river twice. For it’s not the same river and he’s not the same man.” 
Even as the animal revisits the same places, the brain state is never the same twice, always in perpetual flux, changing
in a systematic way. ⏳


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <iframe width="677" height="500" src="https://www.youtube.com/embed/BiV5FDGRY-c" title="UMAP manifold (unsupervised) for figure-8 maze task." frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
    </div>
    <div class="col-sm mt-3 mt-md-0">
    </div>
</div>


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/manifold_pos_rotation.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
    </div>
</div>

When animals consume reward, synchronous population events, aka sharp wave ripples, usually take place. Ripples 'replay'
past experiences. Crucially, with the sensitivity of our methods, we were able to decode not only which places were replayed 
but also which lap events were replayed. 


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/awake_replay_7.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


During NREM sleep 😴, ripples resume their activity. Are awake ripples related to those during subsequent sleep (post-sleep)? 
We compared their population activities.



<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/sleep_replay_8.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

The distribution patterns of trial identity during post-sleep were highly correlated with that during maze replay, but not
with pre-sleep replay. Mixed-effect linear regression analysis confirmed that post-sleep replay pattern were best explained 
by that during awake replay. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/sleep_awake_9.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

We replicated our main conclusions using 4 different methods – including decoding from the original high dimensional space
using different distance metrics, decoding from UMAP low-dimensional embedding, as well as PCA space. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/about/main_consistent_10.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Taken together, our results suggest that awake ripples act as a memory tag. Experience tagged by the awake ripples are 
selectively consolidated numerous times during sleep. 

---

