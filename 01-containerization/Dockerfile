FROM ubuntu:16.04

LABEL maintainer="Nikola Shahpazov"

# path variables
# ARG STARSPACE_PATH=https://github.com/facebookresearch/Starspace.git
# ARG BOOST_PATH=https://github.com/Musicoll/KiwiDependenciesPrebuilt/releases/download/v1.3/boost_1_63_0.zip
# ARG TRAIN_DATA_PATH=https://drive.google.com/u/0/uc?id=11z-oSzbmGJp2S4HAnh09nBdkaVvuxYy8&export=download

# working directory
WORKDIR /starspace

# install prerequisites
RUN \
    apt-get update && apt-get install -y \
    autoconf \
    automake \
    libtool \
    build-essential \
    unzip \
    git \
    wget

# build boost lib
RUN \
    wget $BOOST_PATH && \
    unzip boost_1_63_0.zip && \
    mv boost_1_63_0 /usr/local/bin

# build starspace
RUN \
    git clone $STARSPACE_PATH && \
    cd Starspace && \
    make 

# RUN mkdir data && wget -O data/starspace_input_file.txt $TRAIN_DATA_PATH

CMD [ "./Starspace/starspace", "train", "-trainFile", "./data/starspace_input_file.txt", "-model", "./data/starspace_model"]
