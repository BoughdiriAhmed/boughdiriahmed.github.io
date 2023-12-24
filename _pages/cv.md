---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* Preparatory Program for entry to French Grandes Écoles d’Ingénieurs, 2018
* MSc in Computer Science and Mathematics Engineering, 2022
* MSc Computer vision and machine learning, 2022

Work experience
======
* April 2023 – September 2023: Research Engineer at INRIA, PreMeDICaL
  * Working under the supervision of Julie Josse and Erwan Scornet on Causal inference.

* April 2022 – October 2022: Research Intern at EPFL, LCAV
  * Worked under the supervision of Julien Fageot on statistical analysis of sparse inverse problem algorithm.
  * Adapted and re-wrote a paper on sparse inverse problem to the periodic case.

* April 2021 – July 2021: Research Intern at ENS ULM & CNRS
  * Worked on biology applications of machine learning under the supervision of Guillaume Dugu ́e and Pierre Latouche.
  * Built an acquisition setup and calibrated multiple cameras in order to reconstruct a 3D model of rats.
  * Trained a neural network to track the behaviors of the rats using multiple camera views with DeepLabCut.
    
* January 2021 – April 2021: Research Intern at Air France & CERMICS
  *  Worked under the supervision of Axel Parmentier on the prediction of the delays of airplanes using a stochastic model.
  *  Applied a Lagrangian relaxation on the pricing sub-problem to derivate a lower bound of the minimization problem
  *  Implemented a sub-gradient method to minimize delay costs based on the previous stochastic model.

  
Projects
======
* October 2019: Operations Research Project
  * Finalist in an operations research contest co-organized by Renault and École des Ponts.
  * Implemented an algorithm that dictates when and where to deliver materials to the Renault factories in order to optimize time, CO2 emissions and costs.
  *  The solution we developed was 40% more efficient than the standard solution by Renault.

* November 2018 – March 2020: Self Driving Vehicle
  * In a group of three supervised by Fawzi Nashashibi, we designed and programmed a semi-autonomous driving vehicle for disabled people capable of moving freely in public areas or museums.
  * Implemented a SLAM algorithm in order to localize the vehicle in closed and known environments.
  * Trained a CNN to detect and recognise objects near the car to ensure a safer drive.

Publications
======
  <ul>{% for post in site.publications %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Talks
======
  <ul>{% for post in site.talks %}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>
  
Teaching
======
  <ul>{% for post in site.teaching %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
