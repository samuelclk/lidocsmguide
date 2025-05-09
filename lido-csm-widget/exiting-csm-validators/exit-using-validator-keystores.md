# Exit using validator keystores

## Dappnode

To exit validators in Dappnode open the Web3signer UI by going to the package and then clicking the UI link. After that select the validators you wish to exit, and click exit at the top right.

Follow the instructions and type "I want to exit", followed by `Exit`.

<figure><img src="../../.gitbook/assets/image copia (3).png" alt=""><figcaption></figcaption></figure>

## EthPillar

Step 1: Navigate to EthPillar > Validator > Generate Voluntary Exit Message

Step 2: Broadcast Voluntary Exit Message

## Stereum

Navigate to the "Staking" tab, and click on the green "Withdrawal & Exit Individual Keys" of the keys you want to exit. Alternatively click on the "Withdrawal & Exit All Keys" button at the right to exit all keys in the validator client.

You will be asked to confirm that you want to exit. Check the box and click "Withdraw & Exit".

<figure><img src="../../.gitbook/assets/image copia (1).png" alt=""><figcaption></figcaption></figure>

## Sedge

Sedge currently does not have a built-in validator exit feature.

To exit your validators:

```
# Go to the sedge-data folder
cd ~/sedge-data/

# Run the command
docker compose -it exec validator <client-command>
```

## Eth Docker

You can exit your validators using the keymanager API. To do so:

* Get a list of your keys with `./ethd keys list`
* Sign an exit message with `./ethd keys sign-exit <0xpubkey>`

This signed message is valid for the life of your validator; you do not have to use it right away (you could, for example, keep it for your heirs).

As and when you want to submit a voluntary exit you can:

* Submit the JSON file to [beaconcha.in](https://beaconcha.in/tools/broadcast)\
  OR
* Use `./ethd keys send-exit` to send all created exits through your own consensus layer client

You can track the status of your voluntary exit request at `https://beaconcha.in/validator/<validator-id>`. There are three steps:

* Your validator becomes 'Exited' (5-6 epochs (\~35 minutes), assuming no [exit queue](https://www.validatorqueue.com/))
* Your validator exit becomes 'Withdrawable' (256 epochs (\~27 hours))
* Your 32 Eth is returned to your withdrawal address (currently a maximum of just under a week, see the 'Withdrawals' tab at `https://beaconcha.in/validator/<validator-id>` for the next scheduled withdraw for your validator)

## Systemd

First we need to find the file path of your validator keystores on your machine.

```sh
sudo find /var/lib -name "keystore*.json"
```

Copy the resulting file path onto a text editor for easy retrieval in the next step.&#x20;

{% tabs %}
{% tab title="Teku" %}
Run the exit command.

```sh
teku voluntary-exit                                \
  --beacon-node-api-endpoint=http://127.0.0.1:5051 \
  --validator-keys=/file/path/to/validator_key.json:/file/path/to/validator_key_password.txt
```

**Replace the following:**

1. `/file/path/to/validator_key.json` with your actual file path pointing to your **validator keystore**
2. `/file/path/to/validator_key_password.txt` with your actual file path pointing to your validator keystore **password**

### **Reference**

{% embed url="https://docs.teku.consensys.io/how-to/voluntarily-exit" %}


{% endtab %}

{% tab title="Nimbus" %}
Run the exit command.

```
/usr/local/bin/build/nimbus_beacon_node deposits exit \
--rest-url http://localhost:5052 --validator=<VALIDATOR_KEYSTORE_PATH>
```

**Replace the following:**

1. `<VALIDATOR_KEYSTORE_PATH>` with your actual file path pointing to your **validator keystore**

You will then be prompted to enter the password of your validator keystore.

### Reference

{% embed url="https://nimbus.guide/voluntary-exit.html" %}
{% endtab %}

{% tab title="Lodestar" %}
List all validator pubkeys and copy the CSM validator pubkeys you want to exit.&#x20;

```
/usr/local/bin/lodestar validator list
```

{% hint style="success" %}
You can check which validator pubkeys are active under your CSM Operator ID in the Lido CSM Widget. It does not matter which CSM validator pubkey as long as you exit the requested number of keys.&#x20;
{% endhint %}

Run the exit command.

```
docker run -it --rm \
  -v /var/lib/csm_lodestar_validator/validator_keystores:/var/lib/csm_lodestar_validator/validator_keystores \
  chainsafe/lodestar:latest \
  validator voluntary-exit \
  --network NETWORK \
  --pubkeys 0xF00
```

**Replace the following if needed:**

1. `/var/lib/csm_lodestar_validator/validator_keystores:/var/lib/csm_lodestar_validator/validator_keystores` with your actual docker volume mapping the folder path pointing to your validator keys
2. `NETWORK` with `holesky` or `mainnet`&#x20;
3. `0xF00` with your actual validator pubkey

You will be promted to enter your validator keystore password.

### Reference

{% embed url="https://chainsafe.github.io/lodestar/run/validator-management/validator-cli/#validator-voluntary-exit" %}
{% endtab %}

{% tab title="Lighthouse" %}
Run the exit command.

```
/usr/local/bin/lighthouse --network NETWORK account validator exit \
--keystore /path/to/keystore --beacon-node http://localhost:5052
```

**Replace the following:**

1. `NETWORK` with `mainnet` or `holesky`&#x20;
2. `/path/to/keystore` with your actual file path pointing to your validator keystore

You will then be prompted to enter the password of your validator keystore and then for the Exit Phrase. **Exit Phrase** = `Exit my validator`&#x20;

**Example output:**

```
Running account manager for Holesky network
validator-dir path: ~/.lighthouse/holesky/validators

Enter the keystore password for validator in 0xabcd

Password is correct

Publishing a voluntary exit for validator 0xabcd

WARNING: WARNING: THIS IS AN IRREVERSIBLE OPERATION



PLEASE VISIT https://lighthouse-book.sigmaprime.io/voluntary-exit.html
TO MAKE SURE YOU UNDERSTAND THE IMPLICATIONS OF A VOLUNTARY EXIT.

Enter the exit phrase from the above URL to confirm the voluntary exit:
Exit my validator

Successfully published voluntary exit for validator 0xabcd
Voluntary exit has been accepted into the beacon chain, but not yet finalized. Finalization may take several minutes or longer. Before finalization there is a low probability that the exit may be reverted.
Current epoch: 29946, Exit epoch: 29951, Withdrawable epoch: 30207
Please keep your validator running till exit epoch
Exit epoch in approximately 1920 secs

```

### Reference:

{% embed url="https://lighthouse-book.sigmaprime.io/voluntary-exit.html" %}
{% endtab %}

{% tab title="Prysm" %}
Download the `prysmctl` binaries from the latest [Prysm releases page](https://github.com/prysmaticlabs/prysm/releases) used for one-off operations such as exiting validator keys.

```
cd
curl -LO https://github.com/prysmaticlabs/prysm/releases/download/v5.3.0/prysmctl-v5.3.0-linux-amd64
curl -LO https://github.com/prysmaticlabs/prysm/releases/download/v5.3.0/prysmctl-v5.3.0-linux-amd64.sha256
```

Run the checksum verification process.

```
sha256sum --check prysmctl-v5.3.0-linux-amd64.sha256
```

_**Expected output:** Verify output of the checksum verification._

```
prysmctl-v5.3.0-linux-amd64: OK
```

Run the exit command.

<pre><code><strong>/usr/local/bin/prysmctl validator exit \
</strong>--wallet-dir=/var/lib/csm_prysm_validator --beacon-rpc-provider=http://localhost:5052 
</code></pre>

**Replace the following if needed:**

1. `/var/lib/csm_prysm_validator` with your actual folder path pointing to your Prysm wallet&#x20;

**Note:** The output from running `sudo find /var/lib -name "keystore*.json"` earlier will not be used for Prysm.

You will then be prompted to enter the password of your Prysm wallet and your validator keystore.

### Reference

{% embed url="https://docs.prylabs.network/docs/wallet/exiting-a-validator" %}


{% endtab %}
{% endtabs %}

