# Artifact Appendix

Paper title: Wave Hello to Privacy - Efficient Mixed-Mode MPC using Wavelet Transforms

Artifacts HotCRP Id: 6

Requested Badge: Available

## Description
The accuracy directory contains the files to reproduce accuracy results.
The experiments directory contains the files to reproduce the runtime results.

### Security/Privacy Issues and Ethical Concerns
None.

### Hardware Requirements
We recommend using 128 GiB of RAM.

### Software Requirements
Runtime experiments require to be run with Ubuntu OS.

### Estimated Time and Storage Consumption
The accuracy tests take about half an hour to complete while runtime experiments should complete faster than that.

## Environment
In the following, describe how to access our artifact and all related and necessary data and software components.
Afterward, describe how to set up everything and how to verify that everything is set up correctly.

### Accessibility (All badges)
The artifact can be found at https://github.com/NillionNetwork/WaveHelloToPrivacy with commit 2905326.

### Main Results and Claims

#### Main Result 1: Wavelet Approximation Accuracy
Accuracy as measured by Mean Absolute Error increases exponentially as bit size is decreased.
Haar wavelet approximation improves this error.
Biorthogonal wavelet sees much lower error rates, and almost flat error as bit size decreases.
See Figure 7 and Section 3.4 in the paper.

#### Main Result 2: Runtime
As compared to prior works Curl and Pika, protocols in this paper run orders of magnitude faster.

### Experiments

#### Experiment 1: Accuracy
Generate the accuracy data that supports result 1. Takes approximately 30 minutes.

```bash
cd accuracy
python accuracy.py
```

#### Experiment 2: Runtime
Generate the runtime data that supports result 2. Takes approximately 30 minutes.

```bash
cd experiments
./run_all.sh
```