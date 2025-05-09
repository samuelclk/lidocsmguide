# Method 2: Configure CSM Fee Recipient on separate validator client

## Set up a separate CSM validator client only

### Download validator client

{% tabs %}
{% tab title="Teku" %}
### Install the dependencies - Java Runtime Environment

```bash
sudo apt-get update
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get -y install openjdk-21-jre libjemalloc-dev
```

### Download Teku

[Download](https://github.com/ConsenSys/teku/releases) the latest version of Teku and run the checksum verification process to ensure that the downloaded file has not been tampered with.

```bash
cd
curl -LO https://artifacts.consensys.net/public/teku/raw/names/teku.tar.gz/versions/24.10.2/teku-24.10.2.tar.gz
echo "1cc76913f3b85987e2a60c9b94c6918d31773ebd3237c5fdf33de366fa259202 teku-24.10.2.tar.gz" | sha256sum --check
```

{% hint style="info" %}
Each downloadable file comes with it's own checksum. Replace the actual checksum and URL of the download link in the code block above.

{% hint style="info" %}
Make sure to choose the amd64 version. Right click on the linked text and select "copy link address" to get the URL of the download link to `curl`.
{% endhint %}
{% endhint %}

_**Expected output:** Verify output of the checksum verification._

```
teku-24.10.2.tar.gz: OK
```

If checksum is verified, extract the files and move them into the `(/usr/local/bin)` directory for neatness and best practice. Then, clean up the duplicated copies.

```bash
tar xvf teku-24.10.2.tar.gz
sudo cp -a teku-24.10.2 /usr/local/bin/teku
rm -r teku*
```
{% endtab %}

{% tab title="Nimbus" %}
### Download Nimbus

[Download](https://github.com/status-im/nimbus-eth2/releases) the latest version of Nimbus, extract the zipped file, and then run the checksum verification process to ensure that the "nimbus\_beacon\_node" and "nimbus\_validator\_client" files have not been tampered with during download.

<pre class="language-bash"><code class="lang-bash">cd
curl -LO https://github.com/status-im/nimbus-eth2/releases/download/v24.9.0/nimbus-eth2_Linux_amd64_24.9.0_f54a0366.tar.gz
<strong>tar xvf nimbus-eth2_Linux_amd64_24.9.0_f54a0366.tar.gz
</strong><strong>cd nimbus-eth2_Linux_amd64_24.9.0_f54a0366/build
</strong><strong>echo "e40ec8fb6ded9a085bf52f7fa4b2e3cb8f63670f4d4c0f8e190f5a3d7e0038230985083b22ed859a1ddbdce230df05ebb182a73cfa8a614b470aa7516111b7d0  nimbus_beacon_node" | sha512sum --check
</strong>echo "35737f59e52fdc47823532b15d372a225779f38887c39664239a2171bc6f24a79633dfbb9257c7715ae640ea9037a3c6352e2e58c53af74a352d745e23d8c74b  nimbus_validator_client" | sha512sum --check
</code></pre>

{% hint style="info" %}
Each downloadable file comes with it's own checksum. Replace the actual checksum and URL of the download link in the code block above.

{% hint style="info" %}
Make sure to choose the amd64 version. Right click on the linked text and select "copy link address" to get the URL of the download link to `curl`.
{% endhint %}
{% endhint %}

_**Expected output:** Verify output of the checksum verification._

```
nimbus_beacon_node: OK
nimbus_validator_client: OK
```

If checksum is verified, extract the consensus client and validator client binaries into the `(/usr/local/bin)` directory (as a best practice). Then, clean up the duplicated copies.

```bash
cd ~/nimbus-eth2_Linux_amd64_24.9.0_f54a0366/build
sudo cp nimbus_beacon_node nimbus_validator_client /usr/local/bin
cd
rm -r nimbus*
```
{% endtab %}

{% tab title="Lodestar" %}
This step is not needed for Lodestar as we will be using Docker to download and run it. Proceed to the next step.
{% endtab %}

{% tab title="Lighthouse" %}
### Download Lighthouse

[Download](https://github.com/sigp/lighthouse/releases) the latest version of Lighthouse and run the checksum verification process to ensure that the downloaded file has not been tampered with.

```bash
cd
curl -LO https://github.com/sigp/lighthouse/releases/download/v5.3.0/lighthouse-v5.3.0-x86_64-unknown-linux-gnu.tar.gz
curl -LO https://github.com/sigp/lighthouse/releases/download/v5.3.0/lighthouse-v5.3.0-x86_64-unknown-linux-gnu.tar.gz.asc
```

Run the checksum verification process.

```sh
gpg --keyserver keyserver.ubuntu.com --recv-keys 15E66D941F697E28F49381F426416DC3F30674B0
gpg --verify lighthouse-v5.3.0-x86_64-unknown-linux-gnu.tar.gz.asc lighthouse-v5.3.0-x86_64-unknown-linux-gnu.tar.gz
```

Verify the release signing key (`--recv-keys`) in the first command above in the releases page [here](https://github.com/sigp/lighthouse/releases).

{% hint style="info" %}
Each downloadable file comes with it's own checksum. Replace the actual checksum and URL of the download link in the code block above.

{% hint style="info" %}
Make sure to choose the amd64 version. Right click on the linked text and select "copy link address" to get the URL of the download link to `curl`.
{% endhint %}
{% endhint %}

_**Expected output:** Verify output of the checksum verification._

```
gpg: Signature made Thu Mar 28 07:30:45 2024 UTC
gpg:                using RSA key 15E66D941F697E28F49381F426416DC3F30674B0
gpg: Good signature from "Sigma Prime <security@sigmaprime.io>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 15E6 6D94 1F69 7E28 F493  81F4 2641 6DC3 F306 74B0
```

If checksum is verified, extract the files and move them into the `(/usr/local/bin)` directory for neatness and best practice. Then, clean up the duplicated copies.

<pre class="language-bash"><code class="lang-bash">tar xvf lighthouse-v5.3.0-x86_64-unknown-linux-gnu.tar.gz
sudo cp lighthouse /usr/local/bin
<strong>rm -r lighthouse*
</strong></code></pre>
{% endtab %}

{% tab title="Prysm" %}
### Download Prysm

[Download](https://github.com/prysmaticlabs/prysm/releases) the latest version of Prysm beacon node (`beacon-chain`) and run the checksum verification process to ensure that the downloaded file has not been tampered with.

```bash
cd
curl -LO https://github.com/prysmaticlabs/prysm/releases/download/v5.1.2/beacon-chain-v5.1.2-linux-amd64
curl -LO https://github.com/prysmaticlabs/prysm/releases/download/v5.1.2/beacon-chain-v5.1.2-linux-amd64.sha256
```

Run the checksum verification process.

```sh
sha256sum --check beacon-chain-v5.1.2-linux-amd64.sha256
```

{% hint style="info" %}
Each downloadable file comes with it's own checksum. Replace the actual checksum and URL of the download link in the code block above.

{% hint style="info" %}
Make sure to choose the amd64 version. Right click on the linked text and select "copy link address" to get the URL of the download link to `curl`.
{% endhint %}
{% endhint %}

_**Expected output:** Verify output of the checksum verification._

```
beacon-chain-v5.1.2-linux-amd64: OK
```

If checksum is verified, extract the files and move them into the `(/usr/local/bin)` directory for neatness and best practice. Then, clean up the duplicated copies.

<pre class="language-bash"><code class="lang-bash">mv beacon-chain-v5.1.2-linux-amd64 prysmbeacon #rename the binary file for easy reference
chmod +x prysmbeacon
<strong>sudo cp prysmbeacon /usr/local/bin
</strong><strong>rm -r prysmbeacon beacon-chain-v5.1.2-linux-amd64.sha256
</strong></code></pre>
{% endtab %}
{% endtabs %}

### Create new CSM user

{% tabs %}
{% tab title="Teku" %}
```sh
sudo useradd --no-create-home --shell /bin/false csm_teku_validator
```
{% endtab %}

{% tab title="Nimbus" %}
```sh
sudo useradd --no-create-home --shell /bin/false csm_nimbus_validator
```
{% endtab %}

{% tab title="Lodestar" %}
```sh
sudo useradd --no-create-home --shell /bin/false csm_lodestar_validator
```
{% endtab %}

{% tab title="Lighthouse" %}
```sh
sudo useradd --no-create-home --shell /bin/false csm_lighthouse_validator
```
{% endtab %}

{% tab title="Prysm" %}
```sh
sudo useradd --no-create-home --shell /bin/false csm_prysm_validator
```
{% endtab %}
{% endtabs %}

By clearly segregating the users and permissions for separate services in your workflow, this will provide additional safeguards against operational mistakes that can lead to slashing via double signing.

### Generate Validator Keys

{% content-ref url="../../../generating-validator-keys/" %}
[generating-validator-keys](../../../generating-validator-keys/)
{% endcontent-ref %}

### Transfer Validator Keys to your Node

#### Prepare your validator keys

Now that we have our validator signing keystore, we will need to place it in our validator node itself so that the node can sign attestations and propose blocks.

Plug in the USB drive with your validator signing keystores into your node device. Once the USB drive is plugged in, we will need to identify it. On the terminal of your node, run:

```
lsblk
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

Look for your USB drive in the output list. It will take a name similar to the screenshot above - i.e. `sdx`.

After you find it, you can proceed to mount your USB drive onto the `/media` folder.

```sh
sudo mount /dev/sda1 /media
```

**Note:** Replace `sda1` with the actual name of your USB drive.

You will now be able to access your USB drive via the terminal by going into the `/media` folder.

Go into your USB drive and copy your validator signing keystore into the HOME directory of your node.

```sh
cd /media/staking-deposit-cli
sudo cp -r validator_keys ~
```

Unmount and eject your USB drive.

```sh
cd
sudo umount /media
```

Now you need to create a **plain text password file** for your validator node to decrypt your validator signing keystores.

First let's print and copy the file name of your validator signing keystore.

```
cd ~/validator_keys
ls
```

With the `validator_signing_keystore_file_name` copied, create the password file.

<pre><code>sudo nano <a data-footnote-ref href="#user-content-fn-1">&#x3C;validator_signing_keystore_file_name></a>.txt
</code></pre>

Type in the password you used when generating your validator keys in the earlier step. Then save and exit the file with `CTRL + O, enter, CTRL + X`.

### Import Validator Keys

Create separate folders, import the CSM validator keys, and set appropriate permissions.

{% tabs %}
{% tab title="Teku" %}
### Prepare the CSM validator keystores

1\) Create 3 new folders to store the validator client data, validator keystore, and the validator keystore password

2\) Copy the validator keystores and it's password file into their respective folders

3\) Change the owner of this folder to the teku user

4\) Restrict permissions on this new folder such that only the owner is able to read, write, and execute files in this folder

```sh
sudo mkdir -p /var/lib/csm_teku_validator/validator_keystores /var/lib/csm_teku_validator/keystore_password
sudo cp ~/validator_keys/<validator_keystore.json> /var/lib/csm_teku_validator/validator_keystores
sudo cp ~/validator_keys/<validator_keystore_password.txt> /var/lib/csm_teku_validator/keystore_password
sudo chown -R csm_teku_validator:csm_teku_validator /var/lib/csm_teku_validator
sudo chmod 700 /var/lib/csm_teku_validator
```

{% hint style="info" %}
**Aside from the file extension, the validator\_keystore\_password file will need to be named identically as the validator signing keystore file (e.g. keystore-m-123.json, keystore-m-123.txt)**
{% endhint %}
{% endtab %}

{% tab title="Nimbus" %}
### Prepare the CSM validator keystores

1\) Create a new folder to store the validator client data, validator keystore, and the validator keystore password

```sh
sudo mkdir -p /var/lib/csm_nimbus_validator
```

2\) Run the validator key import process.

<pre class="language-sh"><code class="lang-sh"><strong>sudo /usr/local/bin/nimbus_beacon_node deposits import --data-dir:/var/lib/csm_nimbus_validator/ ~/validator_keys
</strong></code></pre>

3\) Change the owner of this new folder to the `csm_nimbus_validator` user

4\) Restrict permissions on this new folder such that only the owner is able to read, write, and execute files in this folder

```sh
sudo chown -R csm_nimbus_validator:csm_nimbus_validator /var/lib/csm_nimbus_validator
sudo chmod 700 /var/lib/csm_nimbus_validator
```
{% endtab %}

{% tab title="Lodestar" %}
## Prepare the validator data directory

1\) Create 3 new folders to store the validator client data, validator keystore, and the validator keystore password

2\) Copy the validator keystores and it's password file into their respective folders

3\) Change the owner of these new folders to the `csm_lodestar_validator`user

4\) Restrict permissions on this new folder such that only the owner is able to read, write, and execute files in this folder

5\) Retrieve the UID and GID of the `csm_lodestar_validator` user account to be used in your `docker-compose.yml` file in the next step

<pre class="language-sh"><code class="lang-sh">sudo mkdir -p /var/lib/csm_lodestar_validator/validator_keystores /var/lib/csm_lodestar_validator/keystore_password
<strong>sudo cp ~/validator_keys/&#x3C;validator_keystore.json> /var/lib/csm_lodestar_validator/validator_keystores
</strong>sudo cp ~/validator_keys/&#x3C;validator_keystore_password.txt> /var/lib/csm_lodestar_validator/keystore_password
sudo chown -R csm_lodestar_validator:csm_lodestar_validator /var/lib/csm_lodestar_validator
sudo chmod 700 /var/lib/csm_lodestar_validator
id csm_lodestar_validator
</code></pre>

{% hint style="info" %}
**Aside from the file extension, the validator\_keystore\_password file will need to be named identically as the validator signing keystore file (e.g. keystore-m-123.json, keystore-m-123.txt)**
{% endhint %}

_**Expected output:**_

```
uid=1004(csm_lodestar_validator) gid=1005(csm_lodestar_validator) groups=1005(csm_lodestar_validator)
```

_**New folders created:**_

```
/var/lib/csm_lodestar_validator/
/var/lib/csm_lodestar_validator/validator_keystores
/var/lib/csm_lodestar_validator/keystore_password
```
{% endtab %}

{% tab title="Lighthouse" %}
### Prepare the validator data directory

1\) Create a new folders to store the validator client data, validator keystore, and the validator keystore password

```sh
sudo mkdir -p /var/lib/csm_lighthouse_validator
```

2\) Run the validator key import process.

```sh
sudo lighthouse account validator import --network mainnet --datadir /var/lib/csm_lighthouse_validator --directory=$HOME/staking_deposit-cli*/validator_keys
```

{% hint style="warning" %}
set to `--network hoodi` if running on Testnet.
{% endhint %}

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

3\) Change the owner of this new folder to the `csm_lighthouse_validator` user

4\) Restrict permissions on this new folder such that only the owner is able to read, write, and execute files in this folder

```sh
sudo chown -R csm_lighthouse_validator:csm_lighthouse_validator /var/lib/csm_lighthouse_validator
sudo chmod 700 /var/lib/csm_lighthouse_validator
```
{% endtab %}

{% tab title="Prysm" %}
1\) Create a new folders to store the validator client data, validator keystore, and the validator keystore password

```sh
sudo mkdir -p /var/lib/csm_prysm_validator
```

2\) Run the validator key import process.

```sh
sudo /usr/local/bin/prysmvalidator accounts import --keys-dir=$HOME/validator_keys --wallet-dir=/var/lib/csm_prysm_validator --mainnet
```

{% hint style="warning" %}
set to `--network hoodi` if running on Testnet.
{% endhint %}

**Note:** You will be prompted to accept the terms of use, create a new password for the Prysm wallet, and enter the password of your validator keystore.

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

3\) Create a plain text password file for the Prysm wallet

```sh
sudo nano /var/lib/csm_prysm_validator/password.txt
```

Enter the password you set during the validator keystore import process. Then, save + exit with `CTRL+O`, `ENTER`, `CTRL+C`.

4\) Change the owner of this new folder to the `csm_prysm_validator` user

5\) Restrict permissions on this new folder such that only the owner is able to read, write, and execute files in this folder

```sh
sudo chown -R csm_prysmvalidator:csm_prysmvalidator /var/lib/csm_prysm_validator
sudo chmod 700 /var/lib/csm_prysm_validator
```
{% endtab %}
{% endtabs %}

### Configure the separate VC service

Create a new configuration file for your separate validator client.

{% tabs %}
{% tab title="Teku" %}
Create a systemd configuration file for the Teku Validator Client service to run in the background.

```sh
sudo nano /etc/systemd/system/csm_tekuvalidator.service
```

Paste the configuration parameters below into the file:

```bash
[Unit]
Description=CSM Teku Validator Client
Wants=network-online.target
After=network-online.target
[Service]
User=csm_teku_validator
Group=csm_teku_validator
Type=simple
Restart=always
RestartSec=5
Environment="JAVA_OPTS=-Xmx8g"
Environment="TEKU_OPTS=-XX:-HeapDumpOnOutOfMemoryError"
ExecStart=/usr/local/bin/teku/bin/teku vc \
  --network=<hoodi_or_mainnet> \
  --data-path=/var/lib/csm_teku_validator \
  --validator-keys=/var/lib/csm_teku_validator/validator_keystores:/var/lib/csm_teku_validator/keystore_password \
  --beacon-node-api-endpoint=http://<Internal_IP_address>:5051 \
  --validators-proposer-default-fee-recipient=<hoodi_or_mainnet_fee_recipient_address> \
  --validators-builder-registration-default-enabled=true \
  --validators-graffiti="<your_graffiti>" \
  --metrics-enabled=true \
  --metrics-port=8108 \
  --doppelganger-detection-enabled=true 

[Install]
WantedBy=multi-user.target
```

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`. Understand and review your configuration summary below, and amend if needed.

{% hint style="info" %}
**Important:** Recall that you will have to use designated fee recipient addresses as a CSM operator.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endhint %}
{% endtab %}

{% tab title="Nimbus" %}
Create a systemd configuration file for the Nimbus Validator Client service to run in the background.

```bash
sudo nano /etc/systemd/system/csm_nimbusvalidator.service
```

Paste the configuration parameters below into the file:

```
[Unit]
Description=CSM Nimbus Validator Client
Wants=network-online.target
After=network-online.target

[Service]
User=csm_nimbus_validator
Group=csm_nimbus_validator
Type=simple
Restart=always
RestartSec=5
ExecStart=/usr/local/bin/nimbus_validator_client \
  --data-dir=/var/lib/csm_nimbus_validator \
  --payload-builder=true \
  --beacon-node=http://<Internal_IP_address>:5051 \
  --metrics \
  --metrics-port=8108 \
  --suggested-fee-recipient=<hoodi_or_mainnet_fee_recipient_address> \
  --graffiti="<your_graffiti>" \
  --doppelganger-detection

[Install]
WantedBy=multi-user.target
```

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`. Understand and review your configuration summary below, and amend if needed.

{% hint style="info" %}
**Important:** Recall that you will have to use designated fee recipient addresses as a CSM operator.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endhint %}
{% endtab %}

{% tab title="Lodestar" %}
Create a new folder for the CSM Lodestar validator client.&#x20;

```sh
cd
sudo mkdir csm_lodestar_validator
```

Create a `docker-compose.yml` file in the Lodestar folder.

```sh
cd ~/csm_lodestar_validator
sudo nano docker-compose.yml
```

Paste the following configuration into the `docker-compose.yml` file. **Note:** This is similar to the `systemd` configuration file used in the setup of other clients in this curriculum.

```yaml
services:
  validator_client:
    image: chainsafe/lodestar:latest
    container_name: csm_lodestar_validator
    user: <UID>:<GID> #replace with the actual UID and GID of the csm_lodestar_validator user
    restart: unless-stopped
    volumes:
      - /var/lib/csm_lodestar_validator:/var/lib/csm_lodestar_validator
    command:
      - validator
      - --dataDir
      - /var/lib/csm_lodestar_validator
      - --importKeystores
      - /var/lib/csm_lodestar_validator/validator_keystores
      - --importKeystoresPassword
      - /var/lib/csm_lodestar_validator/keystore_password/<validator_signing_keystore_password_file_name>.txt
      - --network
      - <hoodi_or_mainnet>
      - --beaconNodes
      - http://<Internal_IP_address>:5051
      - --builder
      - --builder.boostFactor
      - 100
      - --suggestedFeeRecipient
      - "<hoodi_or_mainnet_fee_recipient_address>"
      - --doppelgangerProtection
      - --metrics
      - --metrics.port
      - "5064"
      - --graffiti
      - "your_graffiti"
    environment:
      NODE_OPTIONS: --max-old-space-size=2048
    ports:
      - "5064:5064"
```

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`.&#x20;

{% hint style="info" %}
**Important:** Recall that you will have to use designated fee recipient addresses as a CSM operator.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endhint %}
{% endtab %}

{% tab title="Lighthouse" %}
Create a systemd configuration file for the Lighthouse Validator Client service to run in the background.

```bash
sudo nano /etc/systemd/system/csm_lighthousevalidator.service
```

Paste the configuration parameters below into the file:

```
[Unit]
Description=CSM Lighthouse Validator Client (Hoodi)
Wants=network-online.target
After=network-online.target

[Service]
User=csm_lighthouse_validator
Group=csm_lighthouse_validator
Type=simple
Restart=always
RestartSec=5
ExecStart=/usr/local/bin/lighthouse vc \
  --network <hoodi_or_mainnet> \
  --datadir /var/lib/csm_lighthouse_validator \
  --builder-proposals \
  --builder-boost-factor 100 \
  --beacon-nodes http://<Internal_IP_address>:5051 \
  --metrics \
  --metrics-port 8108 \
  --suggested-fee-recipient <hoodi_or_mainnet_fee_recipient_address> \
  --graffiti="<your_graffiti>" \
  --enable-doppelganger-protection

[Install]
WantedBy=multi-user.target
```

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`. Understand and review your configuration summary below, and amend if needed.

{% hint style="info" %}
**Important:** Recall that you will have to use designated fee recipient addresses as a CSM operator.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endhint %}
{% endtab %}

{% tab title="Prysm" %}
Create a systemd configuration file for the Prysm Validator Client service to run in the background.

```bash
sudo nano /etc/systemd/system/csm_prysmvalidator.service
```

Paste the configuration parameters below into the file:

```
[Unit]
Description=CSM Prysm Validator Client (Hoodi)
Wants=network-online.target
After=network-online.target

[Service]
User=csm_prysm_validator
Group=csm_prysm_validator
Type=simple
Restart=always
RestartSec=5
ExecStart=/usr/local/bin/prysmvalidator \
  --accept-terms-of-use \
  --<hoodi_or_mainnet> \
  --datadir=/var/lib/csm_prysm_validator \
  --enable-builder \
  --beacon-rpc-provider=<Internal_IP_address>:4000 \
  --beacon-rpc-gateway-provider=<Internal_IP_address>:5051 \
  --wallet-dir=/var/lib/csm_prysm_validator \
  --wallet-password-file=/var/lib/csm_prysm_validator/password.txt \
  --monitoring-port=8108 \
  --suggested-fee-recipient=<hoodi_or_mainnet_fee_recipient_address> \
  --graffiti="<your_graffiti>" \
  --enable-doppelganger

[Install]
WantedBy=multi-user.target
```

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`. Understand and review your configuration summary below, and amend if needed.

{% hint style="info" %}
**Important:** Recall that you will have to use designated fee recipient addresses as a CSM operator.

* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endhint %}
{% endtab %}
{% endtabs %}

## Start the CSM Validator Client

Create a new configuration file for your separate validator client.

{% tabs %}
{% tab title="Teku" %}
Reload the systemd daemon to register the changes made, start the Teku Validator Client, and check its status to make sure its running.

```bash
sudo systemctl daemon-reload
sudo systemctl start csm_tekuvalidator.service
sudo systemctl status csm_tekuvalidator.service
```

The output should say the Teku Validator Client is **“active (running)”.** Press CTRL-C to exit and the Teku Validator Client will continue to run.

Use the following command to check the logs for any warnings or errors:

```bash
sudo journalctl -fu csm_tekuvalidator -o cat | ccze -A
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (64).png" alt=""><figcaption><p>Example output of the Teku VC running on the Goerli testnet. Look out for Hoodi in your output.</p></figcaption></figure>

Press `CTRL-C` to exit.

If the Teku Validator Client service is running smoothly, we can now enable it to fire up automatically when rebooting the system.

```bash
sudo systemctl enable csm_tekuvalidator
```

**Expected output:**

```
Created symlink /etc/systemd/system/multi-user.target.wants/csm_tekuvalidator.service → /etc/s
```

### Remove duplicates of validator keystores

To prevent configuration mistakes leading to double signing in the future, remove duplicate copies of the validator signing keystores once everything is running smoothly.

```sh
sudo rm -r ~/staking_deposit-cli*/validator_keys
```
{% endtab %}

{% tab title="Nimbus" %}
Reload the systemd daemon to register the changes made, start the Nimbus Validator Client, and check its status to make sure its running.

```bash
sudo systemctl daemon-reload
sudo systemctl start csm_nimbusvalidator.service
sudo systemctl status csm_nimbusvalidator.service
```

The output should say the Nimbus Validator Client is **“active (running)”.** Press CTRL-C to exit and the Nimbus Validator Client will continue to run.

Use the following command to check the logs for any warnings or errors:

```bash
sudo journalctl -fu csm_nimbusvalidator -o cat | ccze -A
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

Press `CTRL-C` to exit.

If the Nimbus Validator Client service is running smoothly, we can now enable it to fire up automatically when rebooting the system.

```bash
sudo systemctl enable csm_nimbusvalidator
```

**Expected output:**

```
Created symlink /etc/systemd/system/multi-user.target.wants/csm_nimbusvalidator.service → /etc/systemd/system/csm_nimbusvalidator.service.
```

### Remove duplicates of validator keystores

To prevent configuration mistakes leading to double signing in the future, remove duplicate copies of the validator signing keystores once everything is running smoothly.

```sh
sudo rm -r ~/staking_deposit-cli*/validator_keys
```
{% endtab %}

{% tab title="Lodestar" %}
1\) Make sure you are in the same folder as the `docker-compose.yml` file you created earlier.

```sh
cd ~/csm_lodestar_validator
```

&#x20;2\) Start the docker container.

```sh
docker compose up -d
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

3\) Make sure there are no error messages by monitoring the logs for a few minutes.

```sh
docker logs csm_lodestar_validator -f
```

<figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

## Remove duplicates of validator keystores

To prevent configuration mistakes leading to double signing in the future, remove duplicate copies of the validator signing keystores once everything is running smoothly.

```sh
sudo rm -r ~/staking_deposit-cli*/validator_keys
```
{% endtab %}

{% tab title="Lighthouse" %}
Reload the systemd daemon to register the changes made, start the Lighthouse Validator Client, and check its status to make sure its running.

```bash
sudo systemctl daemon-reload
sudo systemctl start csm_lighthousevalidator.service
sudo systemctl status csm_lighthousevalidator.service
```

The output should say the Lighthouse Validator Client is **“active (running)”.** Press CTRL-C to exit and the Lighthouse Validator Client will continue to run.

Use the following command to check the logs for any warnings or errors:

```bash
sudo journalctl -fu csm_lighthousevalidator -o cat | ccze -A
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You will see some warnings if your beacon node (consensus client) is not yet synced.
{% endhint %}

Press `CTRL-C` to exit.

If the Lighthouse Validator Client service is running smoothly, we can now enable it to fire up automatically when rebooting the system.

```bash
sudo systemctl enable csm_lighthousevalidator
```

**Expected output:**

```
Created symlink /etc/systemd/system/multi-user.target.wants/csm_lighthousevalidator.service → /etc/systemd/system/csm_lighthousevalidator.service.
```

### Remove duplicates of validator keystores

To prevent configuration mistakes leading to double signing in the future, remove duplicate copies of the validator signing keystores once everything is running smoothly.

```sh
sudo rm -r ~/staking_deposit-cli*/validator_keys
```
{% endtab %}

{% tab title="Prysm" %}
Reload the systemd daemon to register the changes made, start the Prysm Validator Client, and check its status to make sure its running.

```bash
sudo systemctl daemon-reload
sudo systemctl start csm_prysmvalidator.service
sudo systemctl status csm_prysmvalidator.service
```

The output should say the Prysm Validator Client is **“active (running)”.** Press CTRL-C to exit and the Prysm Validator Client will continue to run.

Use the following command to check the logs for any warnings or errors:

```bash
sudo journalctl -fu csm_prysmvalidator -o cat | ccze -A
```

**Expected output:**

<figure><img src="../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You will see some warnings if your beacon node (consensus client) is not yet synced.
{% endhint %}

Press `CTRL-C` to exit.

If the Prysm Validator Client service is running smoothly, we can now enable it to fire up automatically when rebooting the system.

```bash
sudo systemctl enable csm_prysmvalidator
```

**Expected output:**

```
Created symlink /etc/systemd/system/multi-user.target.wants/csm_prysmvalidator.service → /etc/systemd/system/csm_prysmvalidator.service.
```

### Remove duplicates of validator keystores

To prevent configuration mistakes leading to double signing in the future, remove duplicate copies of the validator signing keystores once everything is running smoothly.

```sh
sudo rm -r ~/staking_deposit-cli*/validator_keys
```
{% endtab %}
{% endtabs %}

## Resources

{% tabs %}
{% tab title="Teku" %}
* Releases: [https://github.com/Consensys/teku/releases](https://github.com/Consensys/teku/releases)
* Documentation: [https://docs.teku.consensys.io/introduction](https://docs.teku.consensys.io/introduction)
* Discord: [https://discord.gg/consensys](https://discord.gg/consensys) (Select the Teku channel)
{% endtab %}

{% tab title="Nimbus" %}
* Releases: [https://github.com/status-im/nimbus-eth2/releases](https://github.com/status-im/nimbus-eth2/releases)
* Documentation: [https://nimbus.guide/install.html](https://nimbus.guide/install.html)
* Discord: [https://discord.gg/BWKx5Xta](https://discord.gg/BWKx5Xta)
{% endtab %}

{% tab title="Lodestar" %}
* Git repository: [https://github.com/ChainSafe/lodestar-quickstart.git](https://github.com/ChainSafe/lodestar-quickstart.git)
* Documentation: [https://chainsafe.github.io/lodestar/](https://chainsafe.github.io/lodestar/)
* Discord: [https://discord.gg/7Gdb4nFh](https://discord.gg/7Gdb4nFh)
{% endtab %}

{% tab title="Lighthouse" %}
* Releases: [https://github.com/sigp/lighthouse/releases](https://github.com/sigp/lighthouse/releases)
* Documentation: [https://lighthouse-book.sigmaprime.io/intro.html](https://lighthouse-book.sigmaprime.io/intro.html)
* Discord: [https://discord.com/invite/TX7HKfgJN3](https://discord.com/invite/TX7HKfgJN3)
{% endtab %}

{% tab title="Prysm" %}
* Releases: [https://github.com/prysmaticlabs/prysm/releases](https://github.com/prysmaticlabs/prysm/releases)
* Documentation: [https://docs.prylabs.network/docs/getting-started](https://docs.prylabs.network/docs/getting-started)
* Discord: [https://discord.gg/prysmaticlabs](https://discord.gg/prysmaticlabs)
{% endtab %}
{% endtabs %}

[^1]: 
