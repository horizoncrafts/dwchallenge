FROM ubuntu:latest

ENV ANACONDA_FILE Anaconda3-2019.03-Linux-x86_64.sh
ENV ANACONDA_PATH /opt/anaconda3
ENV CONDA_ENV python36

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH $ANACONDA_PATH/bin:$PATH


RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates git man

RUN wget --quiet https://repo.anaconda.com/archive/$ANACONDA_FILE && chmod +x $ANACONDA_FILE

RUN ./$ANACONDA_FILE -b -p $ANACONDA_PATH && rm $ANACONDA_FILE

RUN ln -s $ANACONDA_PATH/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". $ANACONDA_PATH/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate $CONDA_ENV" >> ~/.bashrc



RUN conda create --name $CONDA_ENV python=3.6

RUN conda install --name $CONDA_ENV -y --quiet anaconda

# additional packages
RUN conda install --name $CONDA_ENV -y --quiet tensorflow keras


WORKDIR /data/notebooks

EXPOSE 8888

#not sure if this changes anything
SHELL ["/bin/bash", "-c"]

#RUN ["conda", "activate", "$CONDA_ENV"]
#CMD ["jupyter", "notebook", "--ip", "0.0.0.0", "--allow-root", "--no-browser"]

# needs a trick to run conda initialization. The reason is, the original .bashrc stops its processing when the $PS1 is empty, hence whetever conda added at the of the file could not run
# eventually, this needs to be converted to entrypoint script
CMD ["/bin/bash", "-c", "source $ANACONDA_PATH/etc/profile.d/conda.sh && conda activate $CONDA_ENV && jupyter notebook --ip 0.0.0.0 --allow-root --no-browser"]