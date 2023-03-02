# Learning Docker

## What is Docker?

It solves "it works on my machine" problem. It allows developers to package their apps into Images that run on Containers to allow apps to reun anywhere, consistently.

Images are created from lightweight configuration files called Dockerfiles. That describe everything the apps needs to run.

As long as a machine can run docker, the app will run the same way on any machine.

### Containers vs Virtual Machines

VM use a hypervisor to create a virtual machine that runs on top of the host machine. They require a lot of space, installation and configuration for the OS. They can run multiple OS and apps at the same time. They cannot interact with their host machine.

Containers run on container runtimes, container runtimes work with OS to allocate hardware, directories, copy files, etc. They are lightweight and can run multiple containers at the same time. They can interact with their host machine. They do not boot up, does not require OS installation and configuration. Take less space. Containers can only run one app at a time. They are not isolated from each other and can interact with their hosts.

### Anatomy of a Container

A container is composed of two things, a linux namespace and a linux control group.

## Namespace

| name   | description                         |
| ------ | ----------------------------------- |
| PID    | Process ID                          |
| UTS    | Hostname and domain name            |
| IPC    | Interprocess communication          |
| MOUNT  | Access to file systems              |
| NET    | Network devices, stacks, ports, etc |
| USERNS | User lists                          |
| CGROUP | Control groups                      |
| TIME   | The ability to change time          |

Docker does not support the TIME namespace.

## Control Group

Limit how much any resource can use.

1. Monitor and restrict CPU usage
2. Monitor and restrict memory consumption
3. Monitor and restrict network and disk bandwidth
4. Assign disk quotas

Docker does not support the disk quota.

## Docker Limitations

-   Natively only runs on Linux
-   Containers images are bound to their parent operating system

## The Docker difference

-   Dockerfiles make configuration and packaging apps and their environments easy.
-   Docker Hub makes sharing images with anyone in the world easy.
-   The Docker CLI makes it easy to start your apps in containers.
