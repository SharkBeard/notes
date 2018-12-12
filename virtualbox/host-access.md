# Host Access

In VirtualBox it is possible to have your running virtualbox server accessable by your host machine. This will allow you to test the same site in the guest VM as well as access it from the host's web browser.

## Setup

1. Shut down your VM.
1. Right click VM -> Settings -> Network
1. Click the Adapter 2 tab.
1. Set `attached to` to `Host-only Adapter`
  * You may also need to set `Promiscuous Mode` to `Allow All` under advanced.
1. Make sure it is enabled and click OK.

## Usage

1. Start the VM
  * Make sure both networks are connected
1. Get the local IP address with one of the following commands
  * `$ hostname -I` works in Ubuntu 18.04 LTS
  * `$ iwconfig`
  * `ip`
1. Navigate to that address on your host machine.

## Notes 
* You probably want to add this ip into your hosts file `/etc/hosts` or `C:\Windows\System32\drivers\etc\hosts`
* This IP address is may change, so check that if it breaks.
