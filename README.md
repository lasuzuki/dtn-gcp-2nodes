# Running DTN on Google Cloud using Two Nodes communication

This project has been developed by Dr Lara Suzuki :woman_technologist: [![Twitter](https://img.shields.io/twitter/url/https/twitter.com/larasuzuki.svg?style=social&label=Follow%20%40larasuzuki)](https://twitter.com/larasuzuki) and supervised by Vint Cerf :technologist: [![Twitter](https://img.shields.io/twitter/url/https/twitter.com/vgcerf.svg?style=social&label=Follow%20%40vgcerf)](https://twitter.com/vgcerf), both at Google Inc.

[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/lasuzuki/StrapDown.js/graphs/commit-activity)
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
![Profile views](https://gpvc.arturio.dev/lasuzuki)
[![GitHub contributors](https://img.shields.io/github/contributors/Naereen/StrapDown.js.svg)](https://GitHub.com/lasuzuki/StrapDown.js/graphs/contributors/)
[![Open Source Love svg1](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/)
[![saythanks](https://img.shields.io/badge/say-thanks-ff69b4.svg)](https://saythanks.io/to/lasuzuki)

[![ForTheBadge built-with-science](http://ForTheBadge.com/images/badges/built-with-science.svg)](https://GitHub.com/lasuzuki/)

## Introduction

In this project we demonstrate how to run DTN on two nodes on Google Cloud using NASA's implementation of the bundle protocol - ION.

The ION (interplanetary overlay network) software is a suite of communication protocol implementations designed to support mission operation communications across an end-to-end interplanetary network, which might include on-board (flight) subnets, in-situ planetary or lunar networks, proximity links, deep space links, and terrestrial internets.

## DTN on Google Cloud 101

We strongly recommend that you firstly get familiar with the Loopback communication of ION running on a single node on Google Cloud Platform. The Tutorial is available on [GitHub](https://github.com/lasuzuki/dtn-gcp).

## Getting Started with Two Google Cloud VMs

On [Google Cloud Console](console.cloud.google.com), at the top left corner, `click` on the hamburger icon. Scrow down until you find `Compute Engine`. Hove over `Compute Engine` and then `click` on `VM Instances`.

<img src="https://github.com/lasuzuki/dtn-gcp/blob/main/blob/img1.png" width=400 align=center>


When prompted, click `Create` a new instance. Create two instances in different regions. In this tutorial we have created one instance named `Golstone` in `Zone: us-central1` and the another instance named `Madrid` in `Zone: europe-west2-c`. The diagram below illustrates the two node communication that we will be developing in this tutorial.


