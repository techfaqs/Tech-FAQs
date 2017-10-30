## What is Docker?

Docker is a tool that allows developers, sys-admins etc to easily deploy
their applications in a sandbox (called containers) to run on the host 
operating system i.e. Linux. 
The key benefit of Docker is that it allows users to package an application
with all of its dependencies into a standardized unit for software development.
Unlike virtual machines, containers do not have the high overhead and hence 
enable more efficient usage of the underlying system and resources.

## What are containers?

The industry standard today is to use Virtual Machines (VMs) to run 
software applications.VMs run applications inside a guest Operating System,
which runs on virtual hardware powered by the server’s host OS.

VMs are great at providing full process isolation for applications:
there are very few ways a problem in the host operating system can affect
the software running in the guest operating system, and vice-versa.
But this isolation comes at great cost — the computational overhead 
spent virtualizing hardware for a guest OS to use is substantial.

Containers take a different approach: by leveraging the low-level 
mechanics of the host operating system, containers provide most of
the isolation of virtual machines at a fraction of the computing power.

## Docker Terminology

**Images** - The blueprints of our application which form the basis of containers.
In the demo above, we used the `docker pull` command to download the busybox image.
**Containers** - Created from Docker images and run the actual application.
We create a container using `docker run` which we did using the busybox image that we
downloaded. A list of running containers can be seen using the `docker ps` command.
**Docker Daemon** - The background service running on the host that manages building,
running and distributing Docker containers. The daemon is the process that runs 
in the operating system to which clients talk to.
**Docker Client** - The command line tool that allows the user to interact with the
daemon. More generally, there can be other forms of clients too - such as Kitematic
which provide a GUI to the users.
**Docker Hub** - A registry of Docker images. You can think of the registry as a 
directory of all available Docker images. If required, one can host their own
Docker registries and can use them for pulling images.


#### Reference:

- [Docker Container](https://docker-curriculum.com/)
