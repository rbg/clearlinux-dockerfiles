# Clear Linux* OS `gonum` container image

<!-- Required -->
## What is this image?

`clearlinux/gonum` is a Docker image with `gonum` running on top of the
[official clearlinux base image](https://hub.docker.com/_/clearlinux). User
can deploy gonum apps on top of `clearlinux/gonum` container, and get better
performance via newlib interface which call clearlinux avx512 optimized CBLAS. 

<!-- application introduction -->
> [Gonum](https://gonum.org/) Gonum is a set of numeric libraries for the Go programming language.
> It contains libraries for matrices, statistics, optimization

For other Clear Linux* OS
based container images, see: https://hub.docker.com/u/clearlinux

## Why use a clearlinux based image?

<!-- CL introduction -->
> [Clear Linux* OS](https://clearlinux.org/) is an open source, rolling release
> Linux distribution optimized for performance and security, from the Cloud to
> the Edge, designed for customization, and manageability.

Clear Linux* OS based container images use:
* Optimized libraries that are compiled with latest compiler versions and
  flags.
* Software packages that follow upstream source closely and update frequently.
* An aggressive security model and best practices for CVE patching.
* A multi-staged build approach to keep a reduced container image size.
* The same container syntax as the official images to make getting started
  easy. 

To learn more about Clear Linux* OS, visit: https://clearlinux.org.

<!-- Required -->
## Deployment:

### Deploy with Docker
The easiest way to get started with this image is by simply pulling it from
Docker Hub. 

1. Pull the image from Docker Hub: 
    ```
    docker pull clearlinux/gonum
    ```

2. Start a container using the examples below:
    ```
    docker run --rm clearlinux/gonum
    ```
	or specified app
    ```
    docker run -it --rm -v "$PWD/test":/app -w /app clearlinux/gonum /bin/bash -c "go mod init app;go test -bench ."
    ```
    For gonum app development, use newlib interface for blas can bring significant performance gain over default blas
    ```
	import (
		"gonum.org/v1/gonum/blas/gonum"
		"gonum.org/v1/netlib/blas/netlib"
		"gonum.org/v1/gonum/blas/blas64"
		...
	)

	func BenchmarkCBlas64(b *testing.B) {
		blas64.Use(netlib.Implementation{})
		...
	}
    ```

<!-- Required -->
## Build and modify:

The Dockerfiles for all Clear Linux* OS based container images are available at
https://github.com/clearlinux/dockerfiles. These can be used to build and
modify the container images.

1. Clone the clearlinux/dockerfiles repository.
    ```
    git clone https://github.com/clearlinux/dockerfiles.git
    ```

2. Change to the directory of the application:
    ```
    cd gonum/
    ```

3. Build the container image:
    ```
    docker build -t clearlinux/gonum .
    ```

4. Please refer to [create custom application container image](https://docs.01.org/clearlinux/latest/guides/maintenance/container-image-modify.html) on how to customize your container image with specific debug capabilities, such as: make, git.

   Refer to the Docker documentation for [default build arguments](https://docs.docker.com/engine/reference/builder/#arg).
   Additionally:
   
   - `swupd_args` - specifies arguments to pass to the Clear Linux* OS software
     manager. See the [swupd man pages](https://github.com/clearlinux/swupd-client/blob/master/docs/swupd.1.rst#options)
     for more information.

<!-- Required -->
## Licenses

All licenses for the Clear Linux* Project and distributed software can be found
at https://clearlinux.org/terms-and-policies
