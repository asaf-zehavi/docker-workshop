Tutorial #3 - Creating our own Docker Images
============================================

In this tutorial we'll learn to create our own custom docker images.

Sometimes, there isn't a Docker image out there that fits out needs well enough, and we need to make our own.
Usually, it's best to stat with an existing docker image which is as close to your needs as available.

For this tutorial, we'll try to run a demo of
`PyTorch-BigGraph <https://github.com/facebookresearch/PyTorch-BigGraph>`_ - a library that Or and I use in our project.

Freezing a Container
--------------------

For this tutorial we'll start with the ``pytorch/pytorch`` image that already has pytorch installed.
In order to run PyTorch-BigGraph we'll need to download the package and install it.

Let's start by running the base image as shown in :ref:`tut1`. Now, proceed to running the everything you need to save
in your new docker image. In this case, I prepared the commands for you::

    apt update
    apt install -y curl g++ unzip
    curl -o PyTorch-BigGraph-main.zip https://codeload.github.com/facebookresearch/PyTorch-BigGraph/zip/a11ff0eb644b7e4cb569067c280112b47f40ef62
    unzip PyTorch-BigGraph-main.zip
    rm PyTorch-BigGraph-main.zip
    PBG_INSTALL_CPP=1 pip install PyTorch-BigGraph-a11ff0eb644b7e4cb569067c280112b47f40ef62/
    rm -rf PyTorch-BigGraph-a11ff0eb644b7e4cb569067c280112b47f40ef62/

Now that we've made all the preparations we want to save the changes as an image so we don't have to do that again.
For that, we'll use the ``docker commit`` command. This command takes the current state of a container and "freezes"
it - saving it as an image. So - you should run a command similar to this::

    docker commit <container-identifier> pytorch-biggraph:1.0

After running this - look and see that the image was created.

Now, let's make sure everything went correctly and run a demo run of PyTorch-BigGraph (you don't have to wait for it to
finish, if it starts running - you can move on)::

    torchbiggraph_example_fb15k

Using a Dockerfile
------------------

Committing a container to an image is a workable solution for sure, but it has some drawbacks.
After committing the image you won't know exactly what you did, and what the changes were - so if you'll have to change
something - it'll be a mess. You'll either have to run it, try to understand what you did last time and fix it, or
you'll have to start over. Continually editing the image like this has the potential to make a mess of your image and
leave unintentional changes that can make for some hard-to-fix bugs.

That's why we have a better solution - dockerfiles!

Uploading to the Repository
---------------------------

Running on WEXAC
----------------
