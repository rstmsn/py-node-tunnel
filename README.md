# py-node-tunnel
Personal servers such as Umbrel offer Bitcoin users a quick and easy way to self host a Bitcoin & Lightning Network Node.
At present, Umbrel does not allow it's Bitcoin Core instance to accept incoming connections over clearnet. All connections must take place over Tor.
This has both security and privacy benefits, however, it presents a challenge for some users who wish to connect apps with no existing proxy/Tor support to their Umbrel Bitcoin Core node.

A good example is hardware wallet manufacturer Ledger's desktop software 'Ledger Live'.
Ledger Live allows a user to connect and use their own Bitcoin Core node to validate transactions, verify wallet balances, etc. This is a much more secure approach than using Ledger's own surveillance node.

py-node-tunnel provides a solution to this problem, until such times as native proxy/Tor support is added.

When launched, py-node-tunnel runs an instance of Tor on the users local machine, as well as a python based tunnel script.
The tunnel script opens a port on the local machine, and proceeds to listen for incoming connections.
When a connection is initiated, py-node-tunnel routes the requests over Tor, to the desired target Bitcoin node.

## Requirements

Docker

## Setup

To get setup, download or clone this repository to a folder on your local machine.

## Configuration

To setup py-node-tunnel, edit docker-compose.yaml and update the following lines with your Umbrel's Bitcoin Core Tor hostname & port:

```yaml
tunnel:
	entrypoint:
    	- --connect-host=umbrelbitcoincorerpchostname.onion
		- --connect-port=8332
```
By default, py-node-tunnel will listen for incoming connections on the local machine on port 8332. To change this, edit the following line in docker-compose.yaml:

```yaml
tunnel:
	entrypoint:
		- --listen-port=8332
```

## Launching py-node-tunnel

To launch py-node-tunnel, cd to the py-node-tunnel and run:
`docker-compose up -d`

## Using py-node-tunnel
When using an application that can connect to a Bitcoin Core node, but does not support  proxys/Tor, simply connect to localhost:8332 instead, and your connection will be routed over Tor to the target Bitcoin Core node. 

#### Credits
Thanks to WangYihang for the python tunnel gist:
https://gist.github.com/WangYihang/e7d36b744557e4673d2157499f6c6b5e

**Bitcoin Tips:**
3JHxvvUz4RQHMVYRgdQFfiSmoKfH99U2UZ 