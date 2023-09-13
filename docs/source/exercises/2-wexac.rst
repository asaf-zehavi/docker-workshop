Tutorial #2 - Docker Integrations with Wexac
============================================

In this tutorial we'll learn to integrate dockers with WEXAC - it's REALLY easy.

We'll run the same task with the same docker as the last tutorial, but this time - on WEXAC.

Setup
-----

First of all, we'll setup our workspace. Create a new folder to work from - I created a ``docker-demo`` folder in my
home directory. Now create a bash file with the commands from the previous tutorial::

    humann_databases --download chocophlan DEMO humann_dbs
    humann_databases --download uniref DEMO_diamond humann_dbs
    wget -O demo.sam https://github.com/biobakery/humann/raw/master/examples/demo.sam
    humann --input demo.sam --output demo_sam

I called my file ``demo.sh``.

Running the Job
---------------

This is almost exactly like running any other task on WEXAC, only you need to use the following flags in your ``bsub``
command:

* ``-env LSB_CONTAINER_IMAGE=biobakery/humann:latest``: Specify which docker image to use, WEXAC will pull the docker
  image from a remote repository.
* ``-app nvidia-gpu``: An application that runs Nvidia dockers. Basically, dockers that may also use Nvidia GPUs.
* ``-q gpu-short``: The nvidia-gpu app only runs on GPU machines.
* ``-gpu num=1``: Running in a GPU queue, you need to require GPUs...

**I believe there should be a way to run docker jobs without requiring Nvidia GPUs, but I haven't found it when
searching just now...**

Anyway, open an SSH connection to a WEXAC access server, cd to your new directory, and run a job to run your bash file.
When the job is done - you should have the output files in your directory :)

That's it - it was that easy!
