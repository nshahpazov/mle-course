# building the docker image
_build:
	@echo "Building the docker image from the Dockerfile"
	docker build -t starspace .

# creating a volume to store the data and export it from
create_volume:
	@echo "Creating a data volume"
	@docker volume create starspace_data_volume

# refreshing the data
refresh_data:
	@echo "Copying the data to the data volume"
	@docker run -v starspace_data_volume:/starspace/data --name helper busybox true
	@docker cp data helper:/starspace/
	@docker rm helper

# entire build with all prerequisites
build: _build create_volume refresh_data

# helper to refresh the data
container := $(shell docker run -d -v starspace_data_volume:/starspace/data busybox true)

# export the model to the host machine's data directory in the working directory
export_output_model:
	@echo "Exporting the starspace model to the data directory"
	docker cp $(container):/starspace/data/$(output) ./data/
	docker cp $(container):/starspace/data/$(output).tsv ./data/

# train with the docker image
_train:
	@echo "Training"
	docker run -it \
		-e INPUT_PATH=/starspace/data/$(input) \
		-e OUTPUT_PATH=/starspace/data/$(output) \
		--mount type=volume,source=starspace_data_volume,target=/starspace/data \
		starspace

# entire train procedure
train: refresh_data _train export_output_model
