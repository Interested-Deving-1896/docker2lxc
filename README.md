[update-readmes]   Mode: rewrite — migrating to template structure...
# docker2lxc

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/docker2lxc)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/docker2lxc.git
cd docker2lxc
```

## Usage


Always run the tool from the machine where you need the LXC template.

Depending on whether or not Docker is installed on the machine where you need the LXC template, you will want to use the tool in one of two ways, as explained below.

### Use 1: Docker is available on the machine where the template is needed

In this case, use:

```bash
docker2lxc "$image:$tag" $tarball
```

In the same way you would use:

```bash
docker pull "$image:$tag"
```

#### Use 1: Example

```bash
docker2lxc timescale/timescaledb-ha:pg17 pgvector-pgai-template
```

This will cause the template to be saved as `pgvector-pgai-template.tar.gz` in the same directory. Note that ending the last argument with `.tar.gz` is optional, and will be added to the name of the tarball archive anyway.

#### Use 1: Debugging

To debug an incomplete call to the tool, set the environment variable named `DEBUG` to `1` or `true` before calling `docker2lxc`:

```bash
DEBUG=1 docker2lxc "$image:$tag" $tarball
```

#### Use 1: Cleanup

To remove all the Docker images downloaded locally by `docker2lxc` as part of this usage scenario, use the following command:

```bash
docker image rm --force $(docker image ls -q --filter 'reference=*/?*:docker2lxc')
```

Note that this will only remove images that were pulled by `docker2lxc`.

### Use 2: Docker is not available on the machine where the template is needed

In this case, first set up an SSH access to another machine that has Docker (i.e. `$hostwithdocker`) and enough disk space, then use

```bash
ssh $hostwithdocker "$(docker2lxc $image:$tag)" > $tarball.tar.gz
```

> [!NOTE]
> In this usage scenario, the `docker2lxc' command is teleported and invoked via SSH on the remote host, with the contents of the tarball being redirected and saved to a file on the machine you are working from (which can also be an SSH-accessible remote server, such as the _Proxmox Virtualization Environment_ or PVE).

> [!TIP]
> This usage scenario is also useful if the machine on which the LXC template is to be placed does not have the resources (such as disk space) to download and convert a large Docker image.

#### Use 2: Example

```bash
ssh hostwithdocker "$(docker2lxc timescale/timescaledb-ha:pg17)" > pgvector-pgai-template.tar.gz
```

This will save the template as `pgvector-pgai-template.tar.gz` in the current directory. Note that in this case you have to add `.tar.gz` to the end of the template filename, since it is only created as a result of output forwarding in the shell.

#### Use 2: Debugging

To troubleshoot an incomplete call to the tool, set the environment variable named `DEBUG` to `1` or `true` before "substituting" the `docker2lxc` command.

This will look something like:

```bash
ssh $hostwithdocker "$(DEBUG=1 docker2lxc $image:$tag)" > $tarball.tar.gz
```

#### Use 2: Cleanup

To remove all the Docker images downloaded by `docker2lxc` on the remote, as part of this usage scenario, use the following command:

```bash
ssh hostwithdocker 'docker image rm --force $(docker image ls -q --filter "reference=*/?*:docker2lxc")'
```

Note that this will only remove images on the remote machine that were pulled by `docker2lxc`.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/docker2lxc`](https://github.com/Interested-Deving-1896/docker2lxc) and mirrored through:

```
Interested-Deving-1896/docker2lxc  ──►  OpenOS-Project-OSP/docker2lxc  ──►  OpenOS-Project-Ecosystem-OOC/docker2lxc
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
<!-- License not detected — add a LICENSE file to this repo. -->
<!-- AI:end:license -->
