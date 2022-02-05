# Use the official image as a parent image.
FROM python:3.10.2-slim-buster

RUN apt-get update && apt-get install -y git supervisor pkg-config python-numpy libicu-dev python3-pip
RUN /usr/local/bin/python3 -m pip install --upgrade pip
# Set the working directory.
WORKDIR /usr/src/nlpserver
COPY . .

# Install dependencies
RUN apt-get install -y python3-numpy libicu-dev python3-icu
RUN pip3 install Cython
RUN cd /tmp/ && git clone https://github.com/aboSamoor/pycld2
RUN cd /tmp/pycld2 && python3 setup.py install
#RUN cd /tmp/ && git clone https://github.com/aboSamoor/polyglot
#RUN cd /tmp/polyglot && python3 setup.py install
RUN python3 -m pip install -r requirements.txt


# Download language models
RUN polyglot download LANG:en; python3 -m spacy download en; polyglot download embeddings2.en; polyglot download ner2.en; python3 -m spacy download en_core_web_sm

RUN polyglot download LANG:de && \
    python3 -m spacy download de && \
    polyglot download LANG:fr && \
    python3 -m spacy download fr && \
    polyglot download LANG:es && \
    python3 -m spacy download es && \
    polyglot download embeddings2.de && \
    polyglot download embeddings2.fr && \
    polyglot download embeddings2.es && \
    polyglot download ner2.de && \
    polyglot download ner2.fr && \
    polyglot download ner2.es  && \
    python3 -m spacy download de_core_news_sm  && \
    python3 -m spacy download fr_core_news_sm  && \
    python3 -m spacy download es_core_news_sm

# Set supervisor config
COPY docker/nlpserver.conf /etc/supervisor/conf.d
COPY docker/entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
 
EXPOSE 6400
