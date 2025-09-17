# Artifact Documentation for FSE'26: Improving Alarm Ranking with Code Property Graphs

## 1. Introduction

This document accompanies the artifact for the FSE'26 paper entitled "Improving Alarm Ranking with Code Property Graphs." The provided artifact is encapsulated within a Docker image and includes:

- The implementation of our proposed approach, Combo.
- The baseline alarm ranking approach, Valar.
- The train-and-predict approach, Classify, as described in the paper.
- Preprocessed datasets (D2A and FV) in NPZ format.

## 2. Artifact Setup

This artifact is distributed as a Docker image. Please follow the steps below to set up the environment:

1. **Load the Docker Image**

   Execute the following command to load the Docker image:
   ```bash
   cat combo.tar.part-* > combo.tar
   docker load -i combo.tar
   ```
   This command will import the image with the tag `combo:1.0`.

2. **Run the Docker Container**

   Launch the container interactively using:
   ```bash
   docker run --rm -it combo:1.0
   ```
   Upon entry, the working directory will be set to `/combo`.

3. **Initialize Environment Variables**

   Before executing any experiments, initialize the required environment variables by sourcing the setup script:
   ```bash
   source setup.sh
   ```

## 3. Executing the Artifact

To display the available command-line options, run:
```bash
./main/main -h
```

### Command-Line Arguments

```
usage: main [-h] [--dataset DATASET] --approach APPROACH [--seed SEED] [--n_instances N_INSTANCES]
            [--code_representation {cfg,ddg,pdg,nlp}] [--projects [PROJECTS ...]]

Script for alarm ranking using active learning

optional arguments:
  -h, --help            show this help message and exit
  --dataset DATASET     Dataset: fv, d2a
  --approach APPROACH   Approach: valar, combo, classify
  --seed SEED           Seed value.
  --n_instances N_INSTANCES
                        Size of cache.
  --code_representation {cfg,ddg,pdg,nlp}
                        Code representation. Choose from 'cfg', 'ddg', 'pdg', 'nlp'.
  --projects [PROJECTS ...]
                        List of specified projects.
```

### Example Usage

- To execute Combo on the FV dataset with a cache size of 1:
  ```bash
  main/main --dataset fv --approach combo --n_instances 1
  ```
- To execute Valar on the D2A dataset with a cache size of 50:
  ```bash
  main/main --dataset d2a --approach valar --n_instances 50
  ```
- To execute Classify on the FV dataset:
  ```bash
  main/main --dataset fv --approach classify
  ```

The resulting statistics will be stored in `/combo/logRank/{dataset}-stats`, and detailed alarm ranking histories will be available in `/combo/logRank/{dataset}-history`.

## 4. Directory Structure

The artifact directory is organized as follows:

```
/combo
├── main/        # Python implementation of Combo
├── datasets/    # Input datasets and benchmarks
│   ├── d2a/
│   └── fv/
├── log/         # Output logs for each run
├── logRank/     # Detailed alarm ranking results
├── setup.sh     # Script to initialize environment variables
```
