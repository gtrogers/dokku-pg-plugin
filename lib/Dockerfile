# forked from https://gist.github.com/jpetazzo/5494158

FROM	ubuntu:trusty

# prevent apt from starting postgres right after the installation
RUN	echo "#!/bin/sh\nexit 101" > /usr/sbin/policy-rc.d; chmod +x /usr/sbin/policy-rc.d

# add postres repo
RUN apt-get update && LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y -q wget 
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - "https://www.postgresql.org/media/keys/ACCC4CF8.asc" | sudo apt-key add -

RUN apt-get update && LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y -q postgresql-9.4 postgresql-contrib-9.4
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get clean

# allow autostart again
RUN	rm /usr/sbin/policy-rc.d

ADD	. /usr/bin
RUN	chmod +x /usr/bin/start_pgsql.sh
RUN echo 'host all all 0.0.0.0/0 md5' >> /etc/postgresql/9.4/main/pg_hba.conf
RUN sed -i -e"s/var\/lib/opt/g" /etc/postgresql/9.4/main/postgresql.conf
