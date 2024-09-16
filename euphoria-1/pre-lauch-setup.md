# Setup genesis validator node

Below are the instructions to generate your genesis transaction.

## Generate genesis transaction (pre-launch only)

1. Download the lastest **Euphoria** pre-release from [aurad repo](https://github.com/aura-nw/aura) and run `make` to build the source.
   Or clone source code from the repo
   ```bash
   git clone https://github.com/aura-nw/aura
   cd aura
   git checkout euphoria
   make install
   mkdir -p ~/.local/bin
   ln -s ~/go/bin/aurad ~/.local/bin/aurad
   ```
   
2. Initialize the  directories and create the local genesis file with the correct
   chain-id

   ```bash
   aurad config chain-id euphoria-1
   aurad init <MONIKER-NAME> --chain-id euphoria-1
   ```

3. Create a local key pair for creating validator

   ```bash
   aurad keys add <key-name> --keyring-backend os
   ```

4. Download the pre-genesis file:

   ```bash
   curl -s https://raw.githubusercontent.com/aura-nw/testnets/main/euphoria-1/pre-genesis.json >~/.aura/config/genesis.json
   ```

5. Create the gentx, replace `<key-name>`:

   The number of bonded tokens must be 3600eaura
   
   ```bash
   aurad add-genesis-account <key-name> 3600000000ueaura --keyring-backend os
   aurad gentx <key-name> 3600000000ueaura [flags] --keyring-backend os --chain-id euphoria-1 --yes
   ```
   
   Flags:
   ```
   --commission-rate                   The initial commission rate percentage (Minimum 5%)
   --commission-max-rate               The maximum commission rate percentage (Permanent once set)
   --commission-max-change-rate        The maximum commission change rate percentage (per day)(Permanent once set)
   --min-self-delegation               The minimum self delegation required on the validator
   --moniker                           The validator's moniker
   --details                           The validator's details
   --website                           The validator's website
   --security-contact                  The validators email address
   --identity                          The validators keybase.io pgp id
   ```
   Example:
   ```bash
   aurad gentx KEY-NAME 3600000000ueaura \
   --commission-rate 0.05 \
   --commission-max-rate 0.1 \
   --commission-max-change-rate 0.01 \
   --min-self-delegation 1 \
   --moniker "YOUR VALIDATOR NAME" \
   --details "YOUR VALIDATOR DETAILS" \
   --website "https://YOURWEBSITE.COM" \
   --security-contact="YOUR@EMAIL.COM" \
   --identity "YOUR KEYBASE.IO PGP ID" \
   --from KEY-NAME \
   --chain-id euphoria-1 \
   --keyring-backend os \
   --yes 
   ```

   If all goes well, you will see a message similar to the following:

   ```bash
   Genesis transaction written to "/home/[user]/.aurad/config/gentx/gentx-******.json"
   ```

## Submit gentx and logo
**NOTE**: Deadline for the submission is **July 11th at 9:00 UTC+7**

1. Fork this repository 

2. Upload your logo (optional) and gentx with format:
   
   ```
   gentx-<validator-name>.json
   <validator-adress>.png
   ```

   Example:
   ```
   gentx-auranode.json
   auravaloper1u09a7hv2r7jmx8ndtrykm0xt3ywcsmvxgtghgt.png
   ```

3. Create a pull request to our main branch
Sample PR: [Link](https://github.com/aura-nw/testnets/pull/4)

### Download finalized genesis and setup your validator

1. Download genesis:

   ```bash
   curl -s <TBA> >~/.aura/config/genesis.json
   ```
2. Setup your nodes and services

   Docs: [Link](https://docs.aura.network/validator/running-a-fullnode)
   ```bash
   [Unit]
   Description=Aura Validator
   After=network.target

   [Service]
   Group=aura
   User=aura
   WorkingDirectory=/home/aura
   #ExecStartPre=+/home/aura/.local/bin/pre-checks-aurad.sh
   ExecStart=/home/aura/.local/bin/aurad start
   #ExecStartPost=+/home/aura/.local/bin/post-checks-aurad.sh
   #Sockets=/dev/shm/aura/trpc.socket
   Restart=on-failure
   RestartSec=3
   LimitNOFILE=30000
   ## The Options below are advanced, configure at your own risk ##
   ## Feel free to @ me in discord (Erialos The Silver Fox) if you ##
   ## need help and want to know more ##
   #Set Nice below 0 to give higher process priorety
   #Nice=-10
   # Set allowed CPU's to include 4 but keep CPU Affinity to 2
   # target set CPU's.  Both lists should contain the same cpus
   #IE:  CPUAffinity=0,1,4,7
   #AllowedCPUs=
   #CPUAffinity=
   # Set Out Of Memory Killer to kill process under high memory
   # Pressure and release and re-allowcate
   # This can have an adverse effect of restarting the process too much.
   # Values are -1000 through 1000.  Negative values will seek to use OOM Killer
   # less and values closer to 1000 will result in more process resetarts to
   # free up memory.  I have a script that does something bettter
   #OOMScoreAdjust=800
   # IO Scheduling to realtime and high priority with first in first out
   #IOSchedulingClass=realtime
   # values 0 - 7
   #IOSchedulingPriority=1  
   #CPUSchedulingPolicy=fifo
   # Set long timeout to wait and not kill if daemon is running up memory
   # to complete a task
   #TimeoutSec=500
   # Set Memory Limits
   #MemoryHigh=3300M
   #MemoryMin=800M

   [Install]
   WantedBy=multi-user.target
   ```
      And if you use sockets like me, I recommend putting them in shared memory.  You will need to edit your `/etc/fstab`, add a shared memory entry. It doesn't need to be large.  10M is fine.
   
   Pre-checks
   ```bash
   #!/bin/bash

   #Output to console
   #set -x

   if [ -e /dev/shm/aura/trpc.socket ]; then
       rm /dev/shm/aura/*.socket
   fi

   #Create shared memory directory and give bze and www-data permissions

   if [ ! -e /dev/shm/aura ]; then
       mkdir /dev/shm/aura
   fi

   setfacl -d -R -m u::rwX,g::rwX,o::- /dev/shm/aura
   chmod -R 2774 /dev/shm/aura/
   chown -h -R aura:www-data /dev/shm/aura

   exit 0

   ```
   
   Post-Checks
   ```bash
   #!/bin/bash
   #set -x

   until [ -S /dev/shm/aura/trpc.socket ]
   do
       sleep 1
   done

   setfacl -d -R -m u::rwX,g::rwX,o::- /dev/shm/aura
   chmod -R 2774 /dev/shm/aura/
   chown -h -R aura:www-data /dev/shm/aura

   exit 0

   ```

   
3. Start the service and wait until the genesis time
