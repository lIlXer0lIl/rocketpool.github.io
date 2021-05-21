## Getting Started

### Supported Operating Systems

The smart node client is supported on Linux, MacOS and Windows. **Note that a smart node cannot be run locally on Windows at this stage; the Windows client can only be used to manage a remote server**.

The smart node service is supported on AMD64 architecture and all Unix platforms, with automatic OS dependency installation for Ubuntu, Debian, CentOS and Fedora. OS dependencies (docker engine and docker-compose) must be installed manually on all other Unix platforms.

Support for additional architectures (e.g. ARM) and operating systems will be added incrementally, after successful testing of the existing version.

Note that a node operator must have root access to their node in order to install and run the smart node service.

### Hardware Requirements

The Rocketpool smart node stack will manage an ETH1 node, an ETH2 node and the integration into the Rocketpool network. Depending on your specific ETH1 and ETH2 nodes your hardware usage may vary slightly. We recommend letting the setup script pick random ETH clients to support ecosystem client diversity.

When staking on mainnet, we recommend at least 16GB of memory and 500GB of hard disk space in order to run. Note that **an SSD is required**, as the ETH clients rely on high I/O.

For a detailed overwiev of hardware usage and syncing times per client type, the [eth2-docker]( https://eth2-docker.net/docs/Usage/ResourceUsage ) project has up-to-date statistics.

To see what setups Rocketpool community users are using, please refer to [the Rocketpool hardware guide]( /guides/node/hardware.html ).


### Binary Installation

Firstly, install the smart node client locally. For Linux & MacOS, run either the cURL or wget command depending on which utilities are installed on your system. You can check with `curl --version` and `wget --version` respectively.

#### Linux (64 bit)

With cURL:
``` shell 
curl -L https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-linux-amd64 --create-dirs -o ~/bin/rocketpool && chmod +x ~/bin/rocketpool
```

With wget:
``` shell 
mkdir -p ~/bin && wget https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-linux-amd64 -O ~/bin/rocketpool && chmod +x ~/bin/rocketpool
```

#### MacOS (64 bit):

With cURL:

``` shell
curl -L https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-darwin-amd64 -o /usr/local/bin/rocketpool && chmod +x /usr/local/bin/rocketpool
```

With wget:
``` shell
wget https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-darwin-amd64 -O /usr/local/bin/rocketpool && chmod +x /usr/local/bin/rocketpool
```

#### Windows (64 bit):

1. Download the [smart node client](https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-windows-amd64.exe).
1. Move it to the desired location on your system (e.g. `C:\bin\rocketpool.exe`).
1. Open the command prompt and run it via its full path (e.g. `C:\bin\rocketpool.exe`).

### Service Installation

Secondly, install the smart node service either locally or on a remote server. To install locally, simply run `rocketpool service install`. To install remotely, provide flags for the remote host address, username, and SSH identity file, e.g.:
``` shell
rocketpool --host example.com --user username --key /path/to/identity.pem service install
```

If automatic dependency installation is not supported on your platform (or if you would prefer to install OS dependencies yourself), use the `-d` option to skip this step (e.g. `rocketpool service install -d`). Then, manually install [docker engine](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/).

The following installation options are available:

- `-r`: Verbose mode (print all output from the installation process)
- `-d`: Skip automatic installation of OS dependencies
- `-n`: Specify a network to run the smart node on (default: medalla)
- `-v`: Specify a version of the smart node service package files to use (default: latest)

Once the smart node service has been installed, you may need to start a new shell session if working locally. This is required for updated user permissions to take effect (for interacting with docker engine).


### Service Configuration

Once the smart node service is installed, it must be configured before use. Simply run `rocketpool service config` and follow the prompts to select which Eth 1.0 and Eth 2.0 clients to run in the smart node stack.

You may use [Infura](https://infura.io/) rather than run a full Eth 1.0 client if desired. If you do, you will need to create an account and set up a new project to obtain a project ID. Note that Infura will limit requests after a certain threshold, so uptime is not guaranteed.

By default, the smart node will select a random Eth 2.0 client to run, in order to increase network client diversity. You may, however, select a specific client to run if you prefer.
