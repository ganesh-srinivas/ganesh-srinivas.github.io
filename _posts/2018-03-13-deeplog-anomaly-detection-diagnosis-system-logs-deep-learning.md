---
layout: post
title: "DeepLog: Anomaly Detection and Diagnosis of System Logs through Deep Learning"
date: 2017-02-23
---
[DeepLog: Anomaly Detection and Diagnosis of System Logs through Deep Learning](https://www.cs.utah.edu/~lifeifei/papers/deeplog.pdf). Min Du, Feifei Li. ACM CCS 2017.

DeepLog is a system that performs anomaly detection and diagnosis from system logs through deep learning. It utlizes a recurrent neural network called Long Short Term Memory (LSTM) to model the system log as a natural language sequence. DeepLog detects anomalies when log patterns deviate from the model trained from log data under normal execution.

The [Spell](https://www.cs.utah.edu/~lifeifei/papers/spell.pdf) log parser is used to obtain two structured datasets from the syslog (figure below): a sequence of log keys (message types) and a sequence of parameter value vectors. Spell is an online streaming parser that utilizes a longest common subsequence based approach. The time complexity to process each log entry *e* is close to linear (to the size of *e*). I've only taken a cursory look at the Spell paper and need to study it more carefully to understand how the parsing happens.

<img alt="Image: Log key and parameter value vector extraction from syslog entries" src="/assets/13mar2018/13mar2018-deeplog-log-entries-keys-parameter-vector.png" align="center">

Anomaly detection is performed at two levels: 
1. A log key anomaly detection LSTM model predicts the next log message type (log key). If it is wrong for any log entry, the operator is alerted that there is an anomaly in the execution flow.

2. If there is no anomaly in the execution flow, the parameter value and performance anomaly detection model is invoked. If the predicted parameter vector for that particular log key is very different from the actual parameter vector, the operator is alerted. The second model performs regression, in high-dimension space of the parameter feature vector. Therefore, the mean-squared error (MSE) is used as the loss function when training this model and when deciding to alert the operator.

<img alt="Image: DeepLog architecture" src="/assets/13mar2018/13mar2018-deeplog-architecture.png" align="center">

The paper also focusses on "Workflow Construction from Multi-Task Execution" (Section 4) for aiding in anomaly diagnosis. They propose two ways of going about this: using the execution path anomaly LSTM model and density-based clustering.



Questions:
1. How do the authors propose to do workflow construction? The construction process they've described coded as if-else rules?
