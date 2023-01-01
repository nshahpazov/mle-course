# Description

The following docker setting takes the [https://github.com/facebookresearch/StarSpace](Starspace model)
encapsulated in a Docker environment to train the model on a particular dataset given by the user.

# Instructions to execute the model through a docker environment

1. Build the docker container through the current `Dockerfile`  by running 

```bash
docker build -t starspace .
```

2. Create the docker volume

```bash
docker volume create starspace_data_volume
```

3. Copy the data directory to the docker data volume

```bash
docker run -v starspace_data_volume:/starspace/data --name helper busybox true
docker cp data helper:/starspace/
docker rm helper
```

4. Run the docker image

```bash
docker run -it \
 -e INPUT_PATH=/starspace/data/starspace_input_file.txt \
 -e OUTPUT_PATH=/starspace/data/starspace_model \
 --mount type=volume,source=starspace_data_volume,target=/starspace/data \
 starspace
```

5. Copy the data to the data volume

```
CID=$(docker run -d -v starspace_data_volume:/starspace/data busybox true) && \
docker cp $CID:/starspace/data/starspace_model ./data/ && \
docker cp $CID:/starspace/data/starspace_model.tsv ./data/
```