FROM postgres:9.4

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg 9.1' > /etc/apt/sources.list.d/postgres-9.1.list

RUN apt-get update && apt-get install -y --no-install-recommends \
		postgresql-9.1=9.1.24-1.pgdg80+1 \
		postgresql-contrib-9.1=9.1.24-1.pgdg80+1 \
	&& rm -rf /var/lib/apt/lists/*

ENV PGBINOLD /usr/lib/postgresql/9.1/bin
ENV PGBINNEW /usr/lib/postgresql/9.4/bin

ENV PGDATAOLD /var/lib/postgresql/9.1/data
ENV PGDATANEW /var/lib/postgresql/9.4/data

RUN mkdir -p "$PGDATAOLD" "$PGDATANEW" \
	&& chown -R postgres:postgres /var/lib/postgresql

WORKDIR /var/lib/postgresql

COPY docker-upgrade /usr/local/bin/

ENTRYPOINT ["docker-upgrade"]

# recommended: --link
CMD ["pg_upgrade"]
