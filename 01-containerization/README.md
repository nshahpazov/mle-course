# 01 Containerization

### Description

The following docker setting takes the [https://github.com/facebookresearch/StarSpace](Starspace model)
encapsulated in a Docker environment to train the model on a particular dataset given by the user.


### Prerequisites

Before running the model, you should have an input file in the data directory in the working directory.
### Instructions

1. Build the docker container through the current `Dockerfile`  by running

```bash
make build
```

2. Train the model with the following command

```bash
make train input=starspace_input_file.txt output=model
```

where `input` should be set to the input file for training in the `data directory` and `output` should be
set to the name of the output model which will be present in the `data directory` after the run.

Example file can be found [https://drive.google.com/file/d/11z-oSzbmGJp2S4HAnh09nBdkaVvuxYy8/view?usp=sharing](here)
