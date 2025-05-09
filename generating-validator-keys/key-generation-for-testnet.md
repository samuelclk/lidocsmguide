# 🧪 Key Generation for Testnet

{% hint style="warning" %}
This guide is for testnet setups only. Please follow the Mainnet guide to securely generate keys.
{% endhint %}

## Generating Keys

{% tabs %}
{% tab title="EthPillar" %}
### **Generating Keys**

#### **Method 1**

You will be prompted to generate validator keys during the initial setup process. Select `Yes` and follow the terminal UI to generate your validator keys

#### Method 2

If you selected `No` during the initial setup, you can navigate to the keystore generation step by running `ethpillar` and then selecting:&#x20;

* `Validator Client` >> `Generate / Import Validator Keys` >> `Generate new validator keys`, then follow the instructions to complete the remaining steps
{% endtab %}

{% tab title="Eth Docker" %}
### **Generating Keys**

#### **Method 1**

You will be prompted to generate validator keys during the initial setup process. Select `Yes` and follow the terminal UI to generate your validator keys

#### Method 2

If you selected `No` during the initial setup, can run the following to generate your validator keys.

```sh
cd ~/eth-docker
./ethd cmd run --rm deposit-cli-new --execution_address YOURHARDWAREWALLETADDRESS --uid $(id -u)
```

The created files will be in the directory `eth-docker/.eth/validator_keys`
{% endtab %}

{% tab title="All Others" %}
## Wagyu Keygen: Dappnode, Systemd, Stereum

The [Wagyu Keygen](https://github.com/stake-house/wagyu-key-gen) tool features a GUI to make the process easier.

Go to [wagyu.gg](https://wagyu.gg/) and install the tool. Follow the instructions on the `Wagyu Keygen` GUI to:

1. Create a new secret recovery phrase
2. Select the network (e.g., Mainnet, Holesky)
3. Write down your secret recovery phrase
4. Type in your secret recovery phrase manually to confirm you have written it down correctly
5. Choose how many validator keys you want to generate
6. Encrypt your validator keystores with a strong password
7. **\[IMPORTANT]** Set your withdrawal address to the `Lido Withdrawal Vault`
   * **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
8. Confirm password for validator keystores
9. Choose the folder to store the validator keystores and deposit data file that will be generated (choose the Desktop folder here)

**There will be 2 files generated.**&#x20;

1. A `keystore-m_<timestamp>.json` file: This is your validator signing keystore that your validator node will use to sign attestations. Keep this file extremely secure.
2. A `deposit_data-<timestamp>.json`: This is the file that links your ETH deposit to your validator. You will only use this once, during the deposit process.
{% endtab %}
{% endtabs %}

## Importing Keys

{% hint style="success" %}
This sub-section is also covered in the Node Setup section. Skip this if you have already imported your validator keys previously.
{% endhint %}

{% tabs %}
{% tab title="Dappnode" %}
Go to the Dappnode UI and navigate to the `Stakers` >> `Hoodi` menu. Your Web3Signer will have a link saying `Upload Keystores` . If it doesn’t, make sure that you have waited enough time for all the packages to be installed (around 5 minutes) and refresh the page.

Then click on the `Import Keystores` button on the lower part of the Web3Signer UI.

Here browse for the keystore file(s) you generated in the previous step and enter them along with the password you chose to secure your keystores.

* Upload the keystores and tag them with "Lido".
* The fee recipient will be automatically set to `0x9b108015fe433F173696Af3Aa0CF7CDb3E104258` for Hoodi. **It is not editable.**

You are now ready to upload your deposit data file onto the Lido CSM Widget

{% content-ref url="../lido-csm-widget/upload-remove-view-validator-keys.md" %}
[upload-remove-view-validator-keys.md](../lido-csm-widget/upload-remove-view-validator-keys.md)
{% endcontent-ref %}
{% endtab %}

{% tab title="EthPillar" %}
#### **Method 1**

If you generated validator keys during the initial setup process, you will be prompted to import them during the final step. Select `yes` and follow the instructions to complete the remaining steps

#### Method 2

If you generated your validator keys separate from the initial setup, you will first need to locate the absolute file path to your validator key.&#x20;

```
cat $(find /var/lib -name "keystore*.json" 2>/dev/null)
```

Copy the output file path.

```
ethpillar
```

Then, navigate to the keystore generation step by selecting: `Validator Client` >> `Generate / Import Validator Keys` >> `Import validator keys from offline key generation or backup` and paste the absolute file path to your validator key in the field provided.

Follow the instructions to complete the remaining steps.
{% endtab %}

{% tab title="Stereum" %}
## Importing Validator Keys

Head to the Staking tab in the Stereum Launcher, and drag-&-drop the Keystores.&#x20;

1. Select the Validator Client configured with the Lido Execution Layer Rewards Vault as the Fee Recipient Address.&#x20;
2. Enter the password and click on the checkmark.&#x20;
3. After a few seconds your keys will be imported and your Staking tab should look like this:

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Sedge" %}
WIP
{% endtab %}

{% tab title="Eth Docker" %}
Next, import the generated validator keys onto your validator client

```sh
ethd keys import
```
{% endtab %}

{% tab title="Systemd" %}
\
Refer to the segments `Transfer Validator Keys to your Node` >> `Import Validator Keys` of the following page.

{% content-ref url="../node-setup/advanced/systemd/method-2-configure-csm-fee-recipient-on-separate-validator-client.md" %}
[method-2-configure-csm-fee-recipient-on-separate-validator-client.md](../node-setup/advanced/systemd/method-2-configure-csm-fee-recipient-on-separate-validator-client.md)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}
