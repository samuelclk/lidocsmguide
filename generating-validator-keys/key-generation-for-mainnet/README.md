# 🚀 Key Generation for Mainnet

## Important

* It is highly recommended that you perform this step using an air-gapped machine - i.e. a device that has never connected to the public internet before. We will describe a few methods below.
* If this is not available, turn off all internet and wireless connection (e.g. Ethernet, WiFi, Bluetooth) before proceeding with the key generation step
* In both cases above, make sure you are in a safe environment (e.g. home or office) with a trusted WiFi network for building the validator key generation tool from source. Make sure to also physically block all camera devices - e.g. laptop cameras, Webcams, people standing behind you during this process

## Creating an air-gapped machine

1. The least technical way is to buy a cheap single board computer like the Raspberry Pi from official distributors for less than S$100 SGD
2. **"OS-on-a-stick":** For more technical workarounds, we can flash a new USB drive with TailsOS and run a completely fresh OS from this USB drive itself. This system will be completely isolated from your host device (e.g. working laptop) and the described method below will not store any files after you remove the USB drive

#### _**We will cover Method 2 in this guide.**_&#x20;

## What you will need

1. 2 new and empty USB drives
2. A paper notebook and a pencil (Pens are not recommended)
3. _**100% FOCUS**_

## Download the validator keystore generation file

{% tabs %}
{% tab title="Wagyu Keygen" %}
This is the easiest GUI-based method of generating your validator keystores, deposit data, and recovery seed (mnemonic).

Download the Linux executable file onto your working laptop here: [https://wagyu.gg/](https://wagyu.gg/)

Load the Linux executable file of Wagyu Keygen into a new and empty USB drive.
{% endtab %}

{% tab title="Executable binaries" %}
### Downloading the executable binary file

Download the latest version of the Ethereum validator deposit key generation binary file **on your working laptop** [here](https://github.com/ethereum/staking-deposit-cli/releases) and verify the checksum of the downloaded zipped file.

```sh
cd
curl -LO https://github.com/ethereum/staking-deposit-cli/releases/download/v2.7.0/staking_deposit-cli-fdab65d-linux-amd64.tar.gz
echo "ac3151843d681c92ae75567a88fbe0e040d53c21368cc1ed1a8c3d9fb29f2a3a staking_deposit-cli-fdab65d-linux-amd64.tar.gz" | sha256sum --check
```

**Expected output:**

```
staking_deposit-cli-fdab65d-linux-amd64.tar.gz: OK
```

After the checksum verification, move the zipped file into a new and empty USB drive.
{% endtab %}

{% tab title="Build from source" %}
\*No action needed at this step.
{% endtab %}
{% endtabs %}

## Flash and install OS

1\) Download latest TailsOS [here](https://tails.net/install/download/) and follow the respective instructions to verify the checksums of the downloaded file.

2\) Download an ISO flasher (e.g. [BalenaEtcher](https://etcher.balena.io/)) and flash another new and empty USB drive with your preferred OS. Refer to the sub-section if needed.

{% content-ref url="tailsos-on-usb-as-air-gapped-machine.md" %}
[tailsos-on-usb-as-air-gapped-machine.md](tailsos-on-usb-as-air-gapped-machine.md)
{% endcontent-ref %}

3\) Once your USB drive is flashed with your preferred OS, plug it into your working device and reboot the device to go into the boot menu. Depending on your system, you might need to hold `F2`, `F10`, `F12`, or `ESC` during the rebooting process to bring up the boot menu.

{% hint style="info" %}
You will need to connect your node device to a keyboard and monitor for the installation process
{% endhint %}

<details>

<summary>For an extensive list of laptop models, refer to the links below:</summary>

1\) Non-Apple/Mac models:

[https://techofide.com/blogs/boot-menu-option-keys-for-all-computers-and-laptops-updated-list-2021-techofide/#:\~:text=The%20keys%20that%20are%20generally,of%20the%20computers%20or%20motherboards.](https://techofide.com/blogs/boot-menu-option-keys-for-all-computers-and-laptops-updated-list-2021-techofide/)

2\) Apple/Mac

[https://support.apple.com/en-sg/102603](https://support.apple.com/en-sg/102603)

</details>

4\) Once you see the boot menu, select the option to boot up from your USB drive instead of your usual storage volume and you should see a screen similar to the following. **Note:** You should see "Tails" instead of Ubuntu.

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

5\) Select `*Try or Install Tails`&#x20;

6\) Click on the **"+"** button and add an admin password, then **"Start Tails".** This is required so that you can run the following commands using sudo.

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Wagyu Keygen" %}
## Generate your validator signing keys

### \*BEFORE PROCEEDING TO THE NEXT STEP

1. #### TURN OFF YOUR ETHERNET, WIFI, AND BLUETOOTH ACCESS&#x20;
2. #### PHYSICALLY COVER ALL CAMERA DEVICES - e.g. PHONES, WEBCAMS, LAPTOP CAMERAS, PEOPLE STANDING BEHIND YOU

Load the USB drive containing the Linux executable file of `Wagyu Keygen` onto the newly booted _**"OS-on-a-USB".**_

Move the `Wagyu Keygen` file into the Desktop of your _**"OS-on-a-USB"**_ and run it (double-click).

Follow the instructions on the `Wagyu Keygen` GUI to:

1. Create a new secret recovery phrase
2. Select the network (e.g., Mainnet, Holesky)
3. Write down your secret recovery phrase
4. Type in your secret recovery phrase manually to confirm you have written it down correctly
5. Choose how many validator keys you want to generate
6. Encrypt your validator keystores with a strong password
7. **\[IMPORTANT]** Set your withdrawal address to the `Lido Withdrawal Vault`
   * **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)
   * **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
8. Confirm password for validator keystores
9. Choose the folder to store the validator keystores and deposit data file that will be generated (choose the Desktop folder here)

{% hint style="danger" %}
Do not set your withdrawal address to the `Lido Withdrawal Vault` if you are generating validator keys for non-CSM use.
{% endhint %}

**There will be 2 files generated.**&#x20;

1. A `keystore-m_<timestamp>.json` file: This is your validator signing keystore that your validator node will use to sign attestations. Keep this file extremely secure.
2. A `deposit_data-<timestamp>.json`: This is the file that links your ETH deposit to your validator. You will only use this once, during the deposit process.

Store both files on a new USB drive by copying the entire staking-deposit-cli folder into it.&#x20;

Restart your host device (e.g. working laptop) and remove the OS-on-a-stick. There will not be any persistent memory stored on it.
{% endtab %}

{% tab title="Executable binaries" %}
Load the USB drive containing the `keystore generation zipped file` onto the newly booted _**"OS-on-a-USB".**_

Copy the `keystore generation zipped file` into the Desktop of your _**"OS-on-a-USB".**_

Press `ALT+T`, then extract the contents of the zipped file and change directory into the extracted folder.

```sh
cd Desktop
tar xvf staking_deposit-cli-fdab65d-linux-amd64.tar.gz
cd staking_deposit-cli-fdab65d-linux-amd64
```

## Generate your validator signing keys

### \*BEFORE PROCEEDING TO THE NEXT STEP

1. #### TURN OFF YOUR ETHERNET, WIFI, AND BLUETOOTH ACCESS&#x20;
2. #### PHYSICALLY COVER ALL CAMERA DEVICES - e.g. PHONES, WEBCAMS, LAPTOP CAMERAS, PEOPLE STANDING BEHIND YOU

Run the following command to generate your validator keys. Replace `<number>` with the number of validators you want to set up and `<YourWithdrawalAddress>` with the actual withdrawal address depending on your setup choice.

```
./deposit new-mnemonic --num_validators <number> --chain <network> --eth1_withdrawal_address <YourWithdrawalAaddress>
```

Set your withdrawal address to the `Lido Withdrawal Vault`.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)

{% hint style="danger" %}
Do not set your withdrawal address to the `Lido Withdrawal Vault` if you are generating validator keys for non-CSM use.
{% endhint %}

You will be prompted to key in the following. Select accordingly.

1. Choose your language (for the session)
2. Confirm your execution address (your withdrawal address)
3. Choose the language of your mnemonic word list (seed phrase)
4. Create a password to encrypt your validator signing keystores
5. Confirm password created in step 4

**Expected output:**

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Next, your mnemonic word list will be generated. Write it down on a piece of paper or notebook  -\***Never store this online or on any device that is connected to the internet**.

&#x20;**Expected output:**

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Press any key once you have written your mnemonic down and the tool will prompt you to key in your mnemonic in the same order to verify that you have recorded it correctly.

If you typed in your mnemonic correctly, you will be greeted by an ASCII art of a Rhino!

**Expected output:**

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

**There will be 2 files generated.**&#x20;

1. A `keystore-m_<timestamp>.json` file: This is your validator signing keystore that your validator node will use to sign attestations. Keep this file extremely secure.
2. A `deposit_data-<timestamp>.json`: This is the file that links your ETH deposit to your validator. You will only use this once, during the deposit process.

Store both files on a new USB drive by copying the entire staking-deposit-cli folder into it.&#x20;

Restart your host device (e.g. working laptop) and remove the OS-on-a-stick. There will not be any persistent memory stored on it.
{% endtab %}

{% tab title="Build from source" %}
## Building the validator key generation tool from source

Connect your _**OS-on-a-USB**_ to a trusted WiFi network and fire up the Linux terminal using `Ctrl + Alt + T` .

Install system dependencies - `pip3` & `virtualenv`. _**Note:** Remove the `sudo` prefix for each line if your system returns an error._

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt install python3-venv python3-pip
sudo apt install python3-virtualenv
sudo apt-get install git
```

Create a python virtual environment to run the tool under:

```bash
virtualenv venv
source venv/bin/activate
```

Download the git repository of the tool by running. Reference and verify the URL of the git repository [here](https://github.com/ethereum/staking-deposit-cli).

```bash
git clone -b master --single-branch https://github.com/ethereum/staking-deposit-cli.git
```

Install the dependency packages for running the tool:

```bash
python3 setup.py install
pip3 install -r requirements.txt
```

**Expected output:** You should see some progress bars after a few seconds.

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

### \*BEFORE PROCEEDING TO THE NEXT STEP

1. #### TURN OFF YOUR ETHERNET, WIFI, AND BLUETOOTH ACCESS&#x20;
2. #### PHYSICALLY COVER ALL CAMERA DEVICES - e.g. PHONES, WEBCAMS, LAPTOP CAMERAS, PEOPLE STANDING BEHIND YOU

## Generate your validator signing keys

Run the following command to generate your validator keys. Replace `<number>` with the number of validators you want to set up and `<YourWithdrawalAddress>` with the actual withdrawal address depending on your setup choice.

```bash
python3 ./staking_deposit/deposit.py new-mnemonic --num_validators <number> --chain holesky --eth1_withdrawal_address <YourWithdrawalAddress>
```

Set your withdrawal address to the `Lido Withdrawal Vault`.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)

{% hint style="danger" %}
Do not set your withdrawal address to the `Lido Withdrawal Vault` if you are generating validator keys for non-CSM use.
{% endhint %}

You will be prompted to key in the following. Select accordingly.

1. Choose your language (for the session)
2. Confirm your execution address (your withdrawal address)
3. Choose the language of your mnemonic word list (seed phrase)
4. Create a password to encrypt your validator signing keystores
5. Confirm password created in step 4

**Expected output:**

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Next, your mnemonic word list will be generated. Write it down on a piece of paper or notebook  -\***Never store this online or on any device that is connected to the internet**.

&#x20;**Expected output:**

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Press any key once you have written your mnemonic down and the tool will prompt you to key in your mnemonic in the same order to verify that you have recorded it correctly.

If you typed in your mnemonic correctly, you will be greeted by an ASCII art of a Rhino!

**Expected output:**

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

**There will be 2 files generated.**&#x20;

1. A `keystore-m_<timestamp>.json` file: This is your validator signing keystore that your validator node will use to sign attestations. Keep this file extremely secure.
2. A `deposit_data-<timestamp>.json`: This is the file that links your ETH deposit to your validator. You will only use this once, during the deposit process.

Store both files on a new USB drive by copying the entire staking-deposit-cli folder into it.&#x20;

Restart your host device (e.g. working laptop) and remove the OS-on-a-stick. There will not be any persistent memory stored on it.
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Store your 24-word mnemonic securely.

* **Mainnet:** Write it down physically on a notebook and store that securely. <mark style="color:red;">**Do not store any digital copies of this.**</mark>
* **Testnet:** Fine to store this digitally.
{% endhint %}

## Import Validator Key to your Node

{% hint style="success" %}
This sub-section is also covered in the Node Setup section. Skip this if you have already imported your validator keys previously.
{% endhint %}

{% tabs %}
{% tab title="Dappnode" %}
Go to the Dappnode UI and navigate to the `Stakers` > `Ethereum` menu. Your Web3Signer will have a link saying `Upload Keystores` . If it doesn’t, make sure that you have waited enough time for all the packages to be installed (around 5 minutes) and refresh the page.

Then click on the `Import Keystores` button on the lower part of the Web3Signer UI.

Here browse for the keystore file(s) you generated in the previous step and enter them along with the password you chose to secure your keystores.

* Upload the keystores and tag them with "Lido".
* The fee recipient will be automatically set to `0x388C818CA8B9251b393131C08a736A67ccB19297` for Mainnet. **It is not editable.**

You are now ready to upload your deposit data file onto the Lido CSM Widget

{% content-ref url="../../lido-csm-widget/upload-remove-view-validator-keys.md" %}
[upload-remove-view-validator-keys.md](../../lido-csm-widget/upload-remove-view-validator-keys.md)
{% endcontent-ref %}
{% endtab %}

{% tab title="EthPillar" %}
First, locate the absolute file path to your validator key.&#x20;

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

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Sedge" %}
WIP
{% endtab %}

{% tab title="Eth Docker" %}
### Import validator keys

Move your validator keys into the `/eth-docker/.eth/validator_keys` folder of your validator node. _**Testnet users that generated your validator keys using Eth Docker directly can skip this step.**_

```
sudo cp FILE_PATH_TO_VALIDATOR_KEY ~/eth-docker/.eth/validator_keys
```

Change the user permissions of the folder containing your validator keys.

```sh
sudo chown -R $USER:$USER ~/eth-docker/.eth/validator_keys
```

Next, import the generated validator keys onto your validator client

```
ethd keys import
```
{% endtab %}

{% tab title="Systemd" %}
Refer to the segments `Transfer Validator Keys to your Node` >> `Import Validator Keys` of the following page.

{% content-ref url="../../node-setup/advanced/systemd/method-2-configure-csm-fee-recipient-on-separate-validator-client.md" %}
[method-2-configure-csm-fee-recipient-on-separate-validator-client.md](../../node-setup/advanced/systemd/method-2-configure-csm-fee-recipient-on-separate-validator-client.md)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}
