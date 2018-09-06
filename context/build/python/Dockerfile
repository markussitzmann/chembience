ARG build_label
FROM chembience/base:$build_label
LABEL maintainer="markus.sitzmann@gmail.com "

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.5.1-Linux-x86_64.sh && \
    /bin/bash /Miniconda3-4.5.1-Linux-x86_64.sh -b -p /opt/conda && \
    rm Miniconda3-4.5.1-Linux-x86_64.sh

ENV PATH /opt/conda/bin:$PATH

COPY requirements.txt /

RUN CONDA_PY=36 conda install anaconda-client --yes && \
    CONDA_PY=36 conda config --add channels conda-forge && \
    CONDA_PY=36 conda create --verbose --yes -n chembience

RUN /bin/bash -c "source activate chembience" && \
    CONDA_PY=36 conda install --yes --file /requirements.txt