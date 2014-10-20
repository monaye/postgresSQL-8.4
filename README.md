dockerfiles-centos-postrgresql
=============================

CentOS 6 dockerfile for PostgreSQL 8.4

Setup
-----

To build the image

    # docker build --rm -t <yourname>/postgresql .


Starting PostgreSQL
--------------------

    docker run --name=postgresql84 -d -p 5432:5432 <yourname>/postgresql


Creating a database at launch
-----------------------------

You can create a postgresql superuser at launch, by specifying 'POSTGRESQL_USER',
'POSTGRESQL__PASS' and 'POSTGRESQL_DB' variables. For all the above variables,
a default value of 'docker' is used if not specified.

    docker run --name postgresql84 -d -p 5432:5432 \
    -e 'POSTGRESQL_USER=<db_username>' \
    -e 'POSTGRESQL_PASS=<password>' \
    -e 'POSTGRESQL_DB=<db_name>' \
    <yourname>/postgresql

To connect to the database with the user created above:

    psql -U <db_username> -h $(docker inspect --format {{.NetworkSettings.IPAddress}} postgresql84)
