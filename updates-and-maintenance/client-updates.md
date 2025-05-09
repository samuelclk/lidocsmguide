# Client Updates

## Dappnode

If there are updates available to your clients, they'll appear on the right-hand side of your Dappnode Dashboard:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Click on the package and then on the "Update" botton and follow the instructions for the update. It should install automatically after checking parameters are correct.

You'll be prompted to enable automatic updates for all your packages. It is recommended to update manually as certain client versions conflict with one another. This way, you have full control over which client versions to run for your setup.&#x20;

## EthPillar

Run `ethpillar`. Navigate to each client used and select **"update to latest release"**

## Stereum

If there's updates available to your clients they'll appear on the right-hand side of the Note tab:

<figure><img src="../.gitbook/assets/image copia.png" alt=""><figcaption></figcaption></figure>

Click on the package you wish to update, and then confirm the installation.

## Sedge

If you want to update your clients, first update the `.env` file and change the following lines:

```
EC_IMAGE_VERSION=<client:version>
CC_IMAGE_VERSION=<client:version>
VL_IMAGE_VERSION=<client:version>
```

Run `sedge down` to remove all services, and `sedge run` to run them back up and apply changes to the `.env` file.

## Eth Docker

Run the following commands.

```
ethd down
ethd update
ethd up
```

## Systemd

{% hint style="warning" %}
This sub-section applies to your validator client and Mev-boost client. Replace the "ALL\_CAPS" portion of the following commands with the actual file names.
{% endhint %}

### Stop your client

```
sudo systemctl stop CLIENT.service
```

### Download the latest version

{% hint style="info" %}
**Releases Page:**

* Nimbus: [https://github.com/status-im/nimbus-eth2/releases](https://github.com/status-im/nimbus-eth2/releases)
* Lighthouse: [https://github.com/sigp/lighthouse/releases](https://github.com/sigp/lighthouse/releases)
* Prysm: [https://github.com/OffchainLabs/prysm/releases](https://github.com/OffchainLabs/prysm/releases)
* Lodestar: [https://github.com/ChainSafe/lodestar/releases](https://github.com/ChainSafe/lodestar/releases)
* Teku: [https://github.com/ConsenSys/teku/releases](https://github.com/ConsenSys/teku/releases)
* Mev-boost: [https://github.com/flashbots/mev-boost/releases](https://github.com/flashbots/mev-boost/releases/)
{% endhint %}

Download the latest version of the validator client you are using.

```
curl -LO DOWNLOAD_URL
```

Download the corresponding checksum file.

```
curl -LO CHECKSUM_URL
```

Print the contents of the checksum file.

```
cat CHECKSUM_FILE 
```

Run the checksum verification process to ensure that the files have not been tampered with during download.

```
echo "CHECKSUM DOWNLOADED_CLIENT_FILE_NAME" | sha256sum --check
```

_**Expected output:** Verify the output of the checksum verification._

```
nimbus_validator_client: OK
```

{% hint style="info" %}
Each downloadable file comes with its checksum. Replace the actual checksum and URL of the download link in the code block above.

{% hint style="info" %}
Make sure to choose the amd64 version. Right click on the linked text and select "copy link address" to get the URL of the download link to `curl`.
{% endhint %}
{% endhint %}

If the checksum is verified, extract the validator client binaries into the `(/usr/local/bin)` directory.&#x20;

```bash
tar xvf DOWNLOADED_CLIENT_FILE_NAME
sudo cp LATEST_CLIENT_BINARIES /usr/local/bin
```

Then, clean up the duplicated copies.

```
cd
rm -r ALL_DOWNLOADED_FILES
```

### Restart the validator client

```bash
sudo systemctl start CLIENT.service
sudo systemctl status CLIENT.service
```

Monitor journal logs using

```bash
sudo journalctl -fu CLIENT.service -o cat | ccze -A
```
