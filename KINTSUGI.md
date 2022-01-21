# Getting up and running on Kintsugi testnet

- Create a throwaway ETH address in metamask, and export its secret key. This address **must** not be used for transactions outside
  Kintsugi testnet, it has to be considered compromised once used here.
- Fund this address with 32.13 Kintsugi ETH using the FaucETH at https://kintsugi.themerge.dev/ three times.
- On your Linux machine, install docker
  - If you already have docker installed, skip this step
  - Otherwise, run `sudo apt update && sudo apt -y install docker.io docker-compose`
  - Make your user part of the docker group: `sudo usermod -aG docker MYUSERNAME` and then `newgrp docker`
- Clone this tool and get into the `merge` branch
  - `git clone https://github.com/eth2-educators/eth-docker.git merge-test && cd merge-test && git fetch origin merge && git checkout merge`
- Configure the clients you wish to run
  - `./ethd config`
- Deposit for one key and generate the keystore files
  - `docker-compose run --rm generate-keys` 
- Start the stack:
  - `./ethd up`
- Look at logs and see consensus and execution client synchronizing, and the validator client validating:
  - `./ethd logs -f consensus`
  - `./ethd logs -f execution`
  - `./ethd logs -f validator` - for those clients that have a separate validator client, like Lighthouse
- Observe your validator at https://beaconchain.kintsugi.themerge.dev , by entering its public key or the ETH address you funded it from
- If you want to try a different combo, first `./ethd terminate` so the chain data gets deleted, then just `./ethd config`, choose your clients, 
  **wait 15 minutes**, and `./ethd up`. No need to generate keys again. The 15 minute wait is there to avoid slashing.

Note: Not all consensus/execution client combinations have been tested. Please join us on ethstaker Discord to discuss the results of your experimentation!
And above all, have fun!

Your generated keys are in `./kintsugi-secrets`
