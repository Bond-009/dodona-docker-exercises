FROM ubuntu:18.04

# Use bash as shell
SHELL ["/bin/bash", "-c"]
# Set workdir
WORKDIR /course

# Install necessary tools
RUN apt-get update && \
    apt-get install -y --no-install-recommends bzip2 \
                                               ca-certificates \
                                               curl \
                                               fontconfig \
                                               git \
                                               language-pack-en \
                                               vim \
                                               unzip \
                                               wget \
    && apt-get clean

# Install Miniconda and add to PATH
RUN wget https://repo.continuum.io/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh && \
    bash Miniconda3-4.7.12.1-Linux-x86_64.sh -bf -p /usr/miniconda3/ && \
    rm Miniconda3-4.7.12.1-Linux-x86_64.sh && \
    /usr/miniconda3/bin/conda clean -tipsy && \
    ln -s /usr/miniconda3/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /usr/miniconda3/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

# Add conda to PATH and set locale
ENV PATH="/usr/miniconda3/bin:${PATH}"
ENV LC_ALL en_US.UTF-8
ENV LC_LANG en_US.UTF-8

# copy environment.yml into the image
COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH=/usr/miniconda3/envs/pipeline-tools-1.0.0/bin/:$PATH

LABEL org.opencontainers.image.title="analysispipeline basic RNA-seq" \
      org.opencontainers.image.description="image provides basic tools for RNA-seq pipeline" \
      org.opencontainers.image.source="https://github.com/vibbits/containers-workshop" \
      org.opencontainers.image.revision="1.0.0" \
      org.opencontainers.image.vendor="VIB Bioinformatics Core" \
      org.opencontainers.image.licenses="MIT"

# build
# docker build -t analysispipeline:1.0.1 -f Dockerfile .
# run on example data
# docker run -u="$(id -u):$(id -g)" --rm -v ~/methplotlib/examples/:/data -w="/data/" methplotlib \
# bash -c "methplotlib -m NA19240-methylation_ACTB_calls.tsv.gz NA19240-methylation_ACTB_frequency.tsv.gz \
#          -n calls frequencies -w chr7:5,525,542-5,543,028 \
#          -g GRCh38-ACTB-locus.gtf.gz \
#          --simplify \
#          -b DNase_cluster_ACTB.bed.gz"
