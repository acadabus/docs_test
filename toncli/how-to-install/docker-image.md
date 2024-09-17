# Docker image

If you would like to use toncli, the easiest way to get started is by using the Docker image created by the [Trinketer22 contributor](https://github.com/Trinketer22/func\_docker). This image provides all the necessary binaries and dependencies to run toncli, so you can simply pull the image to your local machine and start using it right away.

To use the Docker image, you will need to have Docker installed on your system. Once you have Docker installed, you can pull the Docker image with the following command:

```bash
docker pull trinketer22/func_docker:slim
docker tag trinketer22/func_docker:slim toncli-local
```

Note that docker image supports Mac M1.



Once the image is downloaded, you can start a Docker container using the image with the following command:

```bash
docker run --rm -it -v /path/to/project:/code toncli-local start --name test_project wallet 
```

This will start a new Docker container running toncli, and you will be able to use toncli as if it were installed on your local machine.

Please note that the Docker image provided by Trinketer22 is currently the easiest way to use toncli, as we are still working on a TON repository that will provide binaries for all our packages, including toncli. In the future, we will provide more detailed instructions for installing and using toncli from the TON repository. In the meantime, we hope that the Docker image provided by Trinketer22 will make it easy for you to get started with toncli.

#### Example of how to run toncli using the Docker image provided by Trinketer22:

```bash
docker run --rm -it -v /path/to/project:/code \
-v /path/to/toncli_conf_dir/:/root/.config \
toncli-local update_libs
```

In this example, we are using two volumes to mount directories from the host system into the Docker container. The first volume mounts the `/path/to/project` directory from the host system to the `/code` directory in the container. This is the directory where your TON project files are located. The second volume mounts the `/path/to/toncli_conf_dir/` directory from the host system to the `/root/.config` directory in the container. This is the directory where toncli stores its deployment information, including your private keys to deploy wallet.

When you run this command, you will be prompted to go through the standard toncli initialization dialog. During this process, you will need to provide the absolute paths to the Func, Fift, and lite-client binaries inside the Docker container. These paths are:

* `/usr/local/bin/func`
* `/usr/local/bin/fift`
* `/usr/local/bin/lite-client`

It's important to note that these paths are inside the Docker container, and not on your local system. Once you have provided these paths and completed the initialization process, toncli will create a `toncli` directory in the `/path/to/toncli_conf_dir/` directory on your local system. This directory will contain the `config.ini` file, as well as the `fift-libs`, `func-libs`, and `test-libs` directories. These directories contain the libraries and dependencies that toncli needs to run.

After this, you will be able to use toncli to deploy and interact with TON smart contracts, using the Docker container as your development environment.&#x20;

```
docker run --rm -it \
-v /path/to/project:/code \
-v /path/to/toncli_conf_dir/:/root/.config \
toncli-local deploy --net testnet
```
