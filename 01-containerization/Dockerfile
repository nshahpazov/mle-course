FROM ubuntu:16.04

LABEL maintainer="Nikola Shahpazov"

# path variables
ARG STARSPACE_PATH=https://github.com/facebookresearch/Starspace.git
ARG BOOST_PATH=https://github.com/Musicoll/KiwiDependenciesPrebuilt/releases/download/v1.3/boost_1_63_0.zip

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

# sh -c ./Starspace/starspace train -trainFile ${INPUT_PATH} -model ${OUTPUT_PATH}
CMD ["sh", "-c", "./Starspace/starspace train -trainFile ${INPUT_PATH} -model ${OUTPUT_PATH}"]
