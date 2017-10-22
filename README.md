**Current build:** fred1475

**Note:** work in progress, port access doesnt work yet

If present, use the `fred1475` tag instead of `latest` or `master`

This is an **unofficial** docker image for Freenet.

The binaries used are from the official Freenet releases. You can verify that
they are trustworthy by checking the sha256 of each and comparing it to the official
release files.

Usage
=====

Just pull the image by tag:

    docker pull infincia/docker-freenet

Then download the docker-compose.yml file found in the github repo, edit it
to set the port and volume configuration the way you want it, then run it:

    docker-compose -f docker-compose.yml up -d

Alternatively you can run the image directly:

    docker run --name freenet -v $HOME/freenet/data:/data -v $HOME/freenet/config:/conf -p 127.0.0.1:8888:8888 -p 127.0.0.1:9481:9481 infincia/docker-freenet

Afterward Freenet should be running, and you should be able to access fproxy on port
8888, either on the local machine or by connecting to it through an ssh tunnel:

    ssh -L 8888:127.0.0.1:8888 -N user@dockerhost

By default Freenet is only accessible from localhost. This can be overwritten in
the `freenet.ini` or via the environment variable `allowedhosts`:

    docker run --env allowedhosts=192.168.0.0/24 ...

If you use docker-compose, see the example in the attached `docker-compose.yml`.


Details
=====

This image ships a set of Freenet binaries inside the image and properly separates
them from user data, so that the image can be torn down and updated without risk
of losing your configuration or identities (fms etc).

This image does not use the java wrapper and has Freenet auto-update disabled in favor
of updating through Docker.

It is recommended that you continue to use it that way rather than turning on auto-update,
as there will be runtime changes that the Docker image will account for that may not be
handled otherwise.
