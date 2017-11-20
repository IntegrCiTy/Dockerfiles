FROM continuumio/miniconda3

USER root

##### Install OBNL ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

### Import required dependecies 

# Create a new virtual environment to manage OBNL
RUN conda create --name obnl-env python=3.5

## From pip
RUN /bin/bash -c "source activate obnl-env && pip install --ignore-installed -U setuptools"

### Install OBNL

# install OBNL temporary branch
RUN git clone -b feature/connection-util https://github.com/IntegrCiTy/obnl.git

# install OBNL dependencies
WORKDIR obnl
RUN /bin/bash -c "source activate obnl-env && pip install -r requirements.txt"
RUN /bin/bash -c "source activate obnl-env && python setup.py install"

# install the OBNL wrapper
RUN git clone -b develop https://github.com/IntegrCiTy/obnl-wrapper.git

# install OBNL wrapper dependencies
WORKDIR obnl-wrapper
RUN /bin/bash -c "source activate obnl-env && pip install -r requirements.txt"
RUN /bin/bash -c "source activate obnl-env && python setup.py install"

# install the OBNL run script
RUN git clone -b develop https://github.com/IntegrCiTy/obnl-run.git

# install OBNL runner dependencies
WORKDIR obnl-run
RUN /bin/bash -c "source activate obnl-env && pip install -r requirements.txt"
RUN /bin/bash -c "source activate obnl-env && python setup.py install"

##### Configure environment ++++++++++++++++++++++++++++++++++++++++++++++++++++

ENV PATH /opt/conda/envs/obnl-env/bin:$PATH

ENV PYTHONPATH ${PWD}:${PYTHONPATH}

ENTRYPOINT ["python", "run.py"]

# docker run -d --rm integrcity/obnl <HOST> <TOOL_PASSWORD> <OBNL_PASSWORD>
