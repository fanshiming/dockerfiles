
FROM postgres:12.7 as pone
FROM  python:"3.8.10-slim-buster" as ptwo
WORKDIR /opt/myapp
COPY  --from=pone /lib /lib
COPY  --from=pone /usr/lib /usr/lib
RUN  ldconfig \   
     && PATH=$PATH:/usr/lib/postgresql/12/bin \
     && export PATH \
     && apt-get update \
     && apt-get -y install gcc \
     && apt-get -y install libpq-dev \
     && pip install psycopg2
