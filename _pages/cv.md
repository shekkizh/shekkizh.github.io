---
layout: archive-cv
title: "Sarath Shekkizhar"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}
{% if page.author and site.data.authors[page.author] %}
{% assign author = site.data.authors[page.author] %}{% else %}{% assign author = site.author %}
{% endif %}

# {{author.name}}

<div id="contact" align="center">

<i class="fa fa-fw fa-map-marker" aria-hidden="true"></i> {{ author.address }}
<a href="{{ site.url }}"><i class="fas fa-fw fa-link" aria-hidden="true" style="margin-left:1em"></i> {{ site.data.ui-text[site.locale].homepage | default: "Website" }}</a>

<a href="mailto:{{ author.email }}"><i class="fas fa-fw fa-envelope" aria-hidden="true" style="margin-left:1em"></i>shekkizh@usc.edu</a>

<a href="https://www.linkedin.com/in/{{ author.linkedin }}" style="margin-left:1em"><i class="fab fa-fw fa-linkedin" aria-hidden="true"></i> {{author.linkedin}}</a>

<a href="https://github.com/{{ author.github }}"><i class="fab fa-fw fa-github" aria-hidden="true" style="margin-left:1em"></i> {{ author.github }}</a>

</div>

### **Staff Scientist, Salesforce**

Working on foundational and applied research on AI agents with a focus on improving reasoning and safety.

## Education

### **Ph.D.** in Electrical and Computer Engineering `Aug 2017 - May 2023`

```
GPA: 3.93
```

**University of Southern California**, Los Angeles, CA <br>
Advisor: [Antonio Ortega](https://viterbi.usc.edu/directory/faculty/Ortega/Antonio).

### **M.S.** in Computer Science `Aug 2017 - May 2022`

```
GPA: 4.0
```

**University of Southern California**, Los Angeles, CA

### **M.S.** in Electrical Engineering (Computer Vision, Machine Learning) `Aug 2012 - Dec 2013`

```
GPA: 3.86
```

**University of Southern California**, Los Angeles, CA

### **B.Tech.** in Electronics and Communication `July 2008 - June 2012`

```
GPA: 9.12
```

**National Institute of Technology, Tiruchirappalli**, India

## Publications

{% for post in site.publications reversed %}

### <a href="{{post.paperurl}}">{{post.title}}</a> {% if post.awards %} **[{{post.awards}}]**{% endif %}

{{post.authors}},
_{{ post.venue }}_, {{ post.date | default: "1900-01-01" | date: "%Y" }}
{% endfor %}

## Patents

{% for patent in site.patents reversed %}

### **{{patent.title}}**, {{patent.application_number}}, _{{patent.status}}_

{{patent.authors}}, _Filed: {{ patent.filing_date | date: "%B %Y" }}_

{% endfor %}

## Work Experience

### **Member of Technical Staff, Tenyx (Acquired by Salesforce)** `June 2023 - October 2024`

Part of the founding team at Tenyx building Voice AI for customer support. Was primarily focused on research and creating intellectual property. Key accomplishments include research on continual learning [[VB article](https://venturebeat.com/ai/tenyx-aims-to-fix-llms-catastrophic-forgetting-problem/)], building TenyxChat series of models [[VB article](https://venturebeat.com/ai/exclusive-ai-startup-tenyxs-fine-tuned-open-source-llama-3-model-outperforms-gpt-4/)], and geometric characterization of LLMs [[HN Discussion](https://news.ycombinator.com/item?id=40899309)]. Was also involved in product development, particularly in endpointing, audio disambiguation, and agent governance.

### **Research Intern**, Google, Sunnyvale, CA `Sep 2022 - Dec 2022`

Host: Mohamed Farghal, Animesh Nandi, Behavior Protections, Counter-Abuse Technology.<br>
Worked on understanding the impact of input data used in training graph models and scalable sampling approaches to improve semi-supervised graph learning. Preliminary experiments with proposed graph learning showed 3x increased recall in abuse detection.

### **Software Engineer 2**, KLA Tencor, Milpitas, CA `Mar 2014 - Oct 2016`

Designed and developed tools to classify and visualize defect modulations for Process Window Qualification in wafer fabrication. Also, implemented and co-owned components for analysis and classification using decision trees and random forests.

### **Freelance Researcher**, Toonchat [(Demo: youtu.be/B7LyoWksHHE)](https://youtu.be/B7LyoWksHHE) `Jan 2014 - Jun 2014`

Worked with animators and researchers on real-time face tracking under the advice of Dr. Eric Petajan for low bandwidth animations and anonymous video chat clients

### **Software Developer**, Laboratory of Neurological Imaging, USC `Aug 2013 - Dec 2013`

Worked under the supervision of Dr. John Van Horn as part of the Information Visualization project, a platform to interact and analyse large amounts of brain data

<!-- ### **Intern**, Bharat Heavy Electrical Ltd, India `June 2011 - July 2011`
Designed an assembly level microcontroller program to measure the bend angles in pipes of different sizes. -->

<!-- ## Other Research Works

### **Manifold embedding using NNK Graphs** `Jan 2020 - May 2020`
Revisited data embedding using graphs in terms of robustness and stability with respect to hyperparameters. NNK graphs are significantly sparser compared to other graph constructions, while being able to capture the structure of noisy manifolds.

### **Manifold Regularized Variational Autoencoder (VAE)** `Aug 2019 - Dec 2019`
Studied disentanglement in VAEs with explicit regularization using graphs. This work was motivated from the perspective of locality often enforced in autoencoders using noisy sampling of embeddings.

### **Are combined Fuzzy Cognitve Maps (FCM) always better than individual maps?** `Aug 2018 - Dec 2018`
Analysed the performance of decisions taken by individuals in a simple game against that of the additive. Combined FCM reduces the effect of error associated with each individual.

### **Impact of l<sub>p</sub>-norm choice on K-nearest neighbor graph construction** `Jan 2018 - May 2018`
Explored the impact of distance norms for k-nearest neighbor graph construction in high dimensional spaces using eigen analysis. Lower norms produce data clusters better than euclidean and higher norms.

### **Graph based Image Segmentation**, Prof. Antonio Ortega `Aug 2013 - Dec 2013`
Performed experiments and analysis on graph based approach to image Segmentation. Leveraged methodologies for finding approximate Fiedler vector on a graph laplacian as an alternative to doing normalized cuts.

### **3D Face Recognition System**, Dr. Jongmoo Choi, Prof. Gerard Medioni `May 2013 - Aug 2013`
Developed on the core recognition library and created an evaluation framework and data set for benchmarking. Made integration efforts on incorporating 3D modelling module for recognition.

### **Dynamic Face Warping**, Prof. Antonio Ortega `Jan 2013 - June 2013`
Implemented a real time facial tracking and warping module in DaVinci DSP board. The project emphasized working under constrained resources and was targeted towards applications in mobile.

### **Optical Character Recognition**, Prof. S. Deivalakshmi `Jan 2012 - June 2012`
A neural network based character recognition system for use with motor vehicle license plate recognition was developed. The system was evaluated with different fonts and lighting confitions.

### **Classification of Mammograms**, Prof. S. Deivalakshmi `Aug 2011 - Dec 2011`
A method to differentiate and identify the nature of tumor in mammograms using discriminant analysis on extracted features was developed and evaluated on the MIAS database.

## Open-source Works
### **Deeplearning Projects using Tensorflow** [(github.com/shekkizh/TensorflowProjects)](https://github.com/shekkizh/TensorflowProjects)
*Highlights*: DCGAN for generating flowers/ faces, Face completion using context, Deep dream, VGG visualization, Image Inversion, Style Transfer

### **Neural Networks Experiments** [(github.com/shekkizh/neuralnetworks.thought-experiments)](https://github.com/shekkizh/neuralnetworks.thought-experiments)
Experiments on Activation functions, Model Pruning (Optimal Brain Damage), Unsupervised Learning using AutoEncoders, VAEs, GANs

### **Fully Convolutional Networks for Semantic Segmentation** [(github.com/shekkizh/FCN.tensorflow)](https://github.com/shekkizh/FCN.tensorflow)
Tensorflow implementation of FCNs for segmentation as in CVPR paper applied on MIT scene parsing challenge dataset

### **Energy Based Generative Adversarial Networks** [(github.com/shekkizh/EBGAN.tensorflow)](https://github.com/shekkizh/EBGAN.tensorflow)
Model implementation of Junbo et. al's paper of training GAN with energy based objective in tensorflow

### **Image Colorization** [(github.com/shekkizh/Colorization.tensorflow)](https://github.com/shekkizh/Colorization.tensorflow)
Experiments on leveraging CNNs for colorizing grayscale images by statistical knowledge gained about objects and colors from a dataset.

### **Image Processing Projects** [(github.com/shekkizh/ImageProcessingProjects)](\href{https://github.com/shekkizh/ImageProcessingProjects)
*Highlights*: Eye Tracking, Facial Tracking and Localization, Seam carving, Image Stitching, Image calibration, Image filters, Object detection and processing -->

## Co-Mentoring

### Carlos Hurtado Comín, Universitat Politècnica de Catalunya (Visiting Researcher, USC) `Mar 2022 - June 2023`

### Aryan Gulati, University of Southern California (CURVE program, USC) `Aug 2021 - June 2023`

### David Bonet Solé, Universitat Politècnica de Catalunya (Visiting Researcher, USC) `Dec 2020 - Aug 2021`

### Keisuke Nonaka, KDDI Research (Visiting Researcher, USC) `Aug 2019 - July 2020`

<!-- ## Teaching Experience

### Course Producer, CS 561 Foundations of Artificial Intelligence, Dr. Sheila Tejada `Fall 2013`

### Course Grader, EE 483 Introduction to DSP, Prof. Edgar Satorius `Summer, Spring 2013` -->

## Academic and Co-Curricular Activities

- **IEEE Rising Star in Signal Processing** awarded at ICASSP 2023
- **IEEE Best Student Paper** Award, ICIP 2020
- Reviewer, IEEE Journals -- JSAIT, TSIPN, SPL, TNNLS
- Reviewer, Conferences -- ICASSP, ICLR, NeurIPS, LoG, ICML
- Mentor, Viterbi Graduate Mentorship Program, Fall 2021
- Viterbi Graduate Student Association (VGSA) Senator, Fall 2017, Spring 2020

<!-- ## Software Projects (Recent)

### **Audentic**, No-Code Voice AI Solution for Web Experiences ([audnetic.io](https://www.audentic.io/))

### **Detextit**, AI-powered solutions for 3D design workflows ([detextit.com](https://www.detextit.com/))

### **Promptact**, Learn prompting by reverse-engineering behavior ([promptact.vercel.app](https://promptact.vercel.app/)) -->

<!-- ### Footer

Last updated: Oct 2021 -->

<!--
- _Coordinator_, ECE Campus Placement Committee 2012, NIT-Tiruchirappalli
- _Organizer_, Guest Lectures, Texas Instruments workshop, ECE Probe 2010 & 2011, NIT-Tiruchirappalli
- _Event Manager_, Robotic Event, Pragyan 2009 & 2010, NIT-Tiruchirapalli
- Ranked among the top 1%, All India Engineering Entrance Exam, 2008
- Ranked among the top 10%, Talent Exam 2007, National Assoc. of Physics and Chemistry Teachers
- Discussant, UAI 2021
- Volunteer, NeurIPS, ICLR, ICML
- Volunteer, USC Vision and Voices, 2018
- Attended BayLearn 2018 (Machine Learning Symposium)
- *Organizer*, Guest Lectures,  Probe 2010, ECE Department, NIT, Tiruchirappalli
- *Event Coordinator*, Pip Bot Robotic Event,  Pragyan 2009, NIT, Tiruchirapalli
- Attended *Bay Area Deep Learning School, 2016*.
- One of 30 teams selected to present at USC Stevens Student Innovator Showcase, 2012. A concept on eye tracking [WYSIWYG] for HCI was presented. -->
