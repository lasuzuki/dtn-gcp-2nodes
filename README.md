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


When prompted, click `Create` a new instance. Create two instances in different regions following the guidance in section one of the [DTN 101 tutorial](https://github.com/lasuzuki/dtn-gcp). In this tutorial we have created one instance named `Golstone` in `Zone: us-central1` and the another instance named `Madrid` in `Zone: europe-west2-c`. The diagram below illustrates the two node communication that we will be developing in this tutorial.

<img src="https://github.com/lasuzuki/dtn-gcp/blob/main/blob/2nodes_ION.png" width=400 align=center>

## The configuration files

In this section we will walk you through the creation of the `host1.rc` file. Follow the same steps to create the same file for `host2.rc`.

### The `ionadmin` configuration

The `ionadmin` configuration file administrates and configures the interface for the local ION node contacts and manages shared memory resources used by ION.
````
## begin ionadmin 
# Initialization command (command 1). 
# Set this node to be node 1 (as in ipn:1).
# Use default sdr configuration (empty configuration file name '').
1 1 ''

# Start ion node
s

# Add a contact.
# It will start at +1 seconds from now, ending +3600 seconds from now.
# It will connect node 1 to itself.
# It will transmit 100000 bytes/second.
a contact +1 +3600 1 1 100000

# Add more contacts.
# The network goes 1--2
# Note that contacts are unidirectional, so order matters.
a contact +1 +3600 1 2 100000
a contact +1 +3600 2 1 100000
a contact +1 +3600 2 2 100000

# Add a range. This is the physical distance between nodes.
# It will start at +1 seconds from now, ending +3600 seconds from now.
# It will connect node 1 to itself.
# Data on the link is expected to take 1 second to reach the other
# end (One Way Light Time).
a range +1 +3600 1 1 1

# Add more ranges.
# We will assume every range is one second.
# Note that ranges cover both directions, so you only need define one range for any combination of nodes.
a range +1 +3600 1 2 1
a range +1 +3600 2 2 1

# Set this node to consume and produce a mean of 1000000 bytes/second.
m production 1000000
m consumption 1000000
## end ionadmin 
````
## ### The `ltpadmin` configuration

````
# Initialization command (command 1).
1 32

# Add a span. (a connection)
a span 1 10 10 1400 10000 1 'udplso `external_IP_of_node_1`:1113'

# Add another span. (to host2) 
# Identify the span as engine number 2.
# Use the command 'udplso 10.1.1.2:1113' to implement the link itself.  In this case, we use udp to connect to host2 using the default port.
a span 2 10 10 1400 10000 1 'udplso `external_IP_of_node_2`:1113'

# Start command.
# This command actually runs the link service output commands (defined above, in the "a span" commands).
# It also starts the link service INPUT task 'udplsi `internal_IP_of_node_1`:1113' to listen locally on UDP port 1113 for incoming LTP traffic.
s 'udplsi `internal_IP_of_node_1`:1113'
## end ltpadmin 
````


