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

Copy Files to & From the Container
----------------------------------
