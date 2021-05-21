# Upgrading Your Smart Node

Rocket Pool smart nodes are not upgraded automatically, as ethereum client updates **may contain breaking changes** and prevent validators from working.
As such, node operators need to be aware of Rocket Pool smart node updates, and apply them manually. Node operators are encouraged to read the changelogs of the relevant repositories.


<br>

## Upgrading the Smart Node Client


The smart node client can be upgraded simply by downloading a new version of the binary and replacing the existing version with it.
For Linux & MacOS, run either the cURL or wget command depending on which utilities are installed on your system.
You can check with `curl --version` and `wget --version` respectively.

### Linux (64 bit):

With cURL:

    curl -L https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-linux-amd64 --create-dirs -o ~/bin/rocketpool && chmod +x ~/bin/rocketpool

With wget::

    mkdir -p ~/bin && wget https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-linux-amd64 -O ~/bin/rocketpool && chmod +x ~/bin/rocketpool

### MacOS (64 bit):

With cURL:

    curl -L https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-darwin-amd64 -o /usr/local/bin/rocketpool && chmod +x /usr/local/bin/rocketpool

With wget:

    wget https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-darwin-amd64 -O /usr/local/bin/rocketpool && chmod +x /usr/local/bin/rocketpool

### Windows (64 bit):

1. Download the [smart node client](https://github.com/rocket-pool/smartnode-install/releases/latest/download/rocketpool-cli-windows-amd64.exe).
1. Overwrite your existing client executable with it (e.g. `C:\bin\rocketpool.exe`).

<br>

## Upgrading the Smart Node Service

Before upgrading the smart node service, if you have made any customizations to your service configuration files, back them up::

    cp -r ~/.rocketpool ~/.rocketpool.bak

Any changes to these files will be overwritten, so you will need to restore them manually after updating.

Next, pause the service before making changes to it::

    rocketpool service pause

Then, upgrade the service configuration files with::

    rocketpool service install -d

You may optionally specify a version of the Rocket Pool smart node service to use, e.g.::

    rocketpool service install -d -v 0.0.3

Once you've upgraded the service configuration files, restore any customizations you made previously.
Then, start the service back up::

    rocketpool service start


<br>

## Post-Upgrade Tasks

Once you have upgraded the smart node client and/or service, check you are running the correct versions with::

	rocketpool service version

In some cases, you may need to rebuild your validator keystores (e.g. if the Eth 2.0 client you are using has updated wallet functionality).
If in doubt, you can always do this with no risk to your existing validator keys.
Once your Eth 1.0 client has finished re-syncing, rebuild your validator keystores with::

	rocketpool wallet rebuild

You can check to see if your validator keys have been loaded correctly with::

	rocketpool service logs validator

Always ensure that your validator container has loaded the keys for each of your minipools.