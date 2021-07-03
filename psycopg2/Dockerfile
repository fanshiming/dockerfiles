
FROM postgres:12.7 as pone
WORKDIR /opt/myapp/lib/
RUN  cp -d /usr/lib/x86_64-linux-gnu/libpq.so.5 /opt/myapp/lib/
RUN  cp    /usr/lib/x86_64-linux-gnu/libpq.so.5.13 /opt/myapp/lib/
RUN  ldd /usr/lib/x86_64-linux-gnu/libpq.so.5 | awk '{print $3}' | \
         xargs -L 1 -i cp {}  /opt/myapp/lib/

FROM  python:"3.8.10-slim-buster" as ptwo
WORKDIR /opt/myapp
COPY  --from=pone /lib /lib
COPY  --from=pone /usr/lib /usr/lib
RUN	  ldconfig \   
	  && PATH=$PATH:/usr/lib/postgresql/12/bin \
      && export PATH \
      && apt-get update \
      && apt-get -y install gcc \
          && apt-get -y install libpq-dev \
          && pip install --no-cache-dir psycopg2==2.9.1
