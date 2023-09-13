Tutorial #1 - Using an Existing Docker Image
============================================

In this tutorial we'll learn to pull a Docker image to our machine, to run it interactively & to copy files to and from
the container.

For this tutorial, we'll use `HUMAnN <https://github.com/biobakery/humann/>`_ as an example. HUMAnN is "a method for
efficiently and accurately profiling the abundance of microbial metabolic pathways and other molecular functions from
metagenomic or metatranscriptomic sequencing data". We will run it on some demo data they provide.

Pull a Docker Image
-------------------
First of all, we'll need to get the docker image we want to use. For this we'll use an image BioBakery published for
HUMAnN. You could search for it yourself in the `Docker Hub <https://hub.docker.com/search?q=>`_, or you can just click
on this direct link for now: https://hub.docker.com/r/biobakery/humann.

Now, we need to pull it to your machine. Pulling a Docker image is the act of downloading it from a remote repository to
your computer. We will do it using the ``docker pull`` command in our shell.

Search the dockerhub page above for the proper command, and run it in your shell (Powershell on Windows, bash on Linux,
etc.).

Now, let's make sure this actually worked. Go to the docker desktop program and open the ``images`` tab. Make sure you
see the new image there. Alternatively, you can check the same thing through the command line, try running ``docker
image ls``.

You can see the docker image is identified by 3 different identifiers:

* The image name. in this case: ``biobakery/humann``
* The version tag. in this case: ``latest`` - meaning you downloaded the latest version of the docker image (this is the
  default). It is also common to download specific versions - for instance I recently downloaded the ``ubuntu:22.04``
  docker which contains the version of ubuntu that came out in April 2022.
* The image ID - in this case: ``7e9cf87a635c``. This is a part of the image's checksum. Both images and containers have
  such ID's, and every command can take this ID as input, as well as the name & version.

Run it Interactively
--------------------

Now, we want to use the docker image we downloaded to create a docker container and run our commands in it. The easiest
way would be using the ``run`` command. This command takes a given docker image, creates a container from it ,and runs
the container with your parameters. In this case, we want to run the container interactively. In order to do that - run
the following command::

    docker run --interactive --tty <docker identifier>

Use one of the identifiers discussed in the previous section. Alternatively, you can use the shorthand version::

    docker run -it <docker identifier>

Now, the prompt of your shell should change - all the commands you run from here on out will run within the newly
created docker container. Try it if you like.

Next, lets have a look at our new container. Open the "Docker Desktop" application, and check the ``containers`` tab -
you should see your new container there. You could also open another terminal and run one of these commands to get the
same information: ``docker ps`` or ``docker container ls``.

Finally, let's get down to business and run HUMAnN. Open the terminal you've run the ``docker run`` in, or open a new
terminal to this container using the Docker Desktop GUI. In this terminal, run the following commands::

    humann_databases --download chocophlan DEMO humann_dbs
    humann_databases --download uniref DEMO_diamond humann_dbs
    wget https://github.com/biobakery/humann/raw/master/examples/demo.sam
    humann --input demo.sam --output demo_sam

These commands download some demo databases for HUMAnN and a demo input file. The final line runs HUMAnN on the input
file. If you've done everything correctly - the commands should run without a hitch.

Copy Files to & From the Container
----------------------------------
