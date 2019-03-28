---
layout: page
title: Projects
permalink: /projects/
---

{% for project in site.portfolio %}

{% if project.redirect %}
<div class="project">
    <div class="thumbnail">
        <a href="{{ project.redirect }}" target="_blank">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>
{% else %}

<div class="project ">
    <div class="thumbnail">
        <a href="{{ site.baseurl }}{{ project.url }}">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}    
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endif %}

{% endfor %}

_*previous blog_
<br/>
<br/>
<hr/>
<br/>
<br/>

## Recent Highlights

<br/>
<br/>

# **ORB-SLAM2 for Object Localization** [[Code]](https://github.com/lefthandwriter/orbslam2)

- Exploring monocular ORB-SLAM2 (C++) for localizing traffic objects with respect to a moving vehicle

- [[Blog post]](https://lefthandwriter.github.io/vision/2019/03/14/slam-deeplearning.html) exploring Visual SLAM and deep learning in complementary forms

![image-center]({{ site.url }}{{ site.baseurl }}/assets/projects/orbslam2.png){: .align-center height="90%" width="90%"}

<br/>
<hr/>
<br/>

# **Road Crack Segmentation** [[Code]](https://github.com/lefthandwriter/KittiSeg)

- Adapted KittiSeg for performing road crack segmentation on the CRACK500 dataset

![image-center]({{ site.url }}{{ site.baseurl }}/assets/projects/crack_segmentation.png){: .align-center height="90%" width="90%"}

<br/>
<hr/>
<br/>

# **Koopman Operator Approach for Signalized Traffic** [[Publication]](http://coogan.ece.gatech.edu/papers/pdf/ling2018koopman.pdf) [[Talk]](/assets/presentations/koopman-slides-final.pdf)

- Developed a data-driven method for modeling traffic queues at signalized intersections and detecting imminent congestion, based on Koopman Operator Theory and Dynamic Mode Decomposition 

- Involved a 135GB traffic event dataset from Sensys Networks, design of an SQL database, visualizations with plotly and usage of a REST API to get travel time data from Acyclica GO

![image-center]({{ site.url }}{{ site.baseurl }}/assets/projects/signalizedtraffic.jpg){: height="90%" width="90%"}

<br/>
<hr/>
<br/>
