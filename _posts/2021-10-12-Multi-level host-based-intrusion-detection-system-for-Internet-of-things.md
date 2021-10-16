---
layout: post
title: "[Review] Multi-level host-based intrusion detection system for Internet of things"
tags: HIDS IoT Review
author: "Pranjal Chakraborty"
---

### [Multi-level host-based intrusion detection system for Internet of things, 2020](https://journalofcloudcomputing.springeropen.com/articles/10.1186/s13677-020-00206-6)

#### Key informations
* Proposed host-based intrusion detection framework for IoT devices.
* Used tracing techniques and ML/DL.
* Dataset used for training are prepared or generated, and labeled, within the work.

#### Information from the paper
* Types of attacks used for making the dataset: Mirai, Nmap scan (not necessarily an attack, but integral part of an attack), Metasploit, Ransomware, a spying tool depeloped by the authors, and a two-prong web interface attack using DirBuster and Nikto.
* Tracing overheads are measured using ```sysbench```.
* LSTM is used for constructing the DL architecture (? but no metric was shown). OneClass SVM is used too, which is particularly useful for anomaly detection.

#### Possible improvement(s)
* Can the analysis be done in another edge device? ```tflite``` might come in handy in this case.
* The CNN implementation that is talked about in the first paper could be tried.
