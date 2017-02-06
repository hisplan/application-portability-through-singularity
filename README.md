# Application Protability through Singularity

This was presented by Jaeyoung Chun on Feb 3, 2017. The presentation covers the following topics and the PPT file can be found [here](./presentation.pptx).

- Goals
- Virtualization
- Docker vs. Singularity at 10,000 ft.
- Creating Image
- Running Container
- Physical Size of Image File
- Memory Usage at Runtime
- Data Access Issues

## Examples

Here are some of the examples you can try out.

### Virtual Machines

Most of the examples here requires Singularity to be installed on your machine. The following virtual machines comes pre-built with Singularity. But, you need to have Vagrant on your machine to programatically manage virtual machines and environments.

- [Singularity on CentOS](https://github.com/hisplan/vagrant-centos-singularity)
- [Singularity on Ubuntu](https://github.com/hisplan/vagrant-ubuntu-singularity)

### Running Containers

- [Running samtools by creating a container image from a Singularity image definition file](https://github.com/hisplan/singularity-samtools)
- [Running samtools by creating a container image from a Docker image definition file](https://github.com/hisplan/docker-samtools)

### File Sharing

Two primary methods are provided to share files on the host with the container.

#### By Replacing User's Home Directory:

```bash
$ singularity shell --home /home/chunj/tmp-home samtool.img
```

#### By Using Bind Points

```bash
$ singularity shell --bind /ifs/data:/ifs/data samtools.img
```

This only works when the following two conditions are met:

1. The system administrator has enabled user control of binds (via `user bind control = yes`) in `singularity.conf`.
2. Either
    - the system administrator has enabled the use of file system overlay (via `enable overlay = yes`) in `singularity.conf`)
    
    or

    - the bind point (`/ifs/data` in this case) already exist within the container.

