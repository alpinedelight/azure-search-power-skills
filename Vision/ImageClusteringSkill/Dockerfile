FROM tensorflow/tensorflow

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
COPY requirements.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
    && rm -rf /tmp/pip-tmp

RUN apt-get update
RUN apt-get install 'libsm6'\
    'libgl1-mesa-glx'\
    'libxext6'  -y

#RUN mkdir -p /usr/src/mlops TOBDELETED
#RUN mkdir -p /usr/src/mlops/common TOBDELETED
RUN mkdir -p /usr/src/ml
RUN mkdir -p /usr/src/ml/extractors
RUN mkdir -p /usr/src/ml/similarity
RUN mkdir -p /usr/src/ml/models
RUN mkdir -p /usr/src/ml/utils
RUN mkdir -p /usr/src/api
RUN mkdir -p /usr/src/api/common
RUN mkdir -p /usr/src/api/extractor
RUN mkdir -p /usr/src/api/models

WORKDIR /usr/src/api

#COPY mlops/__init__.py /usr/src/  TOBDELETED
#COPY mlops/__init__.py /usr/src/mlops/  TOBDELETED
#COPY mlops/common /usr/src/mlops/common  TOBDELETED
#COPY mlops/__init__.py /usr/src/mlops/common  TOBDELETED
COPY ml/extractors /usr/src/ml/extractors
COPY ml/models /usr/src/ml/models
COPY ml/similarity /usr/src/ml/similarity
COPY ml/utils /usr/src/ml/utils
COPY custom-skills-deployment/models /usr/src/api/models/
COPY custom-skills-deployment/extractor/ /usr/src/api/extractor/
COPY custom-skills-deployment/app.py /usr/src/api/

EXPOSE 5000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "5000"]