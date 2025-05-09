# 🔧 Setting the Fee Recipient for CSM Validators

When running validators via Lido Community Staking Module (CSM), it is **mandatory** to set the fee recipient to the **Lido Execution Layer Rewards Vault**:

* **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
* **Hoodi testnet:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)

{% hint style="warning" %}
For **Hoodi Testnet** users:

Use [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258) instead of [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297) in the guides below.
{% endhint %}

Failure to do so may result in [MEV stealing penalties](https://docs.lido.fi/staking-modules/csm/guides/mev-stealing), including:

* A **penalty** equal to the stolen execution layer rewards plus a fixed fine
* Your **bond being locked** until the full penalty amount is returned

This guide shows you how to correctly set the fee recipient on various platforms. It does not cover how to set up or run a validator node from scratch.

{% hint style="success" %}
You can verify the fee recipient address on the [Lido Deployed Contracts](https://docs.lido.fi/deployed-contracts/) page.
{% endhint %}

## Dappnode[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#dappnode) <a href="#dappnode" id="dappnode"></a>

Dappnode sets the fee recipient through the **Staking Brain** in the Web3Signer package, either during key import or by editing existing validator keys.

#### Set fee recipient when importing new validator keys[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#set-fee-recipient-when-importing-new-validator-keys) <a href="#set-fee-recipient-when-importing-new-validator-keys" id="set-fee-recipient-when-importing-new-validator-keys"></a>

**Step 1:** In the side panel, go to **“Stakers”**, then select the **Web3Signer** package and click **“Upload Keystores”** to open the **Staking Brain**.

**Step 2:** Enable **“Use same tag for every file”**, and in the **“Staking Protocol”** dropdown, select **“Lido”**. This automatically sets the fee recipient to:

`0x388C818CA8B9251b393131C08a736A67ccB19297`

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Click **“Submit Keystores”** to complete the import.

***

#### Change fee recipient on existing validator keys[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#change-fee-recipient-on-existing-validator-keys) <a href="#change-fee-recipient-on-existing-validator-keys" id="change-fee-recipient-on-existing-validator-keys"></a>

**Step 1:** In the side panel, go to **“Stakers”**, then select the **Web3Signer** package and click **“Upload Keystores”**.

**Step 2:** Review the **Fee Recipient** field for each validator key. If it's incorrect or missing, click the **edit** icon.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Set the fee recipient to: `0x388C818CA8B9251b393131C08a736A67ccB19297`

**Step 4:** Click **“Submit Keystores”** to apply the changes.

warning

Known issue with Nimbus on Dappnode

Several users have [reported](https://research.lido.fi/t/proposed-blocks-with-wrong-fee-recipient-due-to-dappnode-nimbus-bug/9057) that when running **Nimbus** with Dappnode, the fee recipient set in the **Staking Brain** (Web3Signer) is not applied. Instead, the fee recipient set on the **consensus layer node** is used, which can result in MEV stealing, when it is not set to the Lido Execution Layer Rewards Vault.

This issue has been acknowledged by the Dappnode team but has not been confirmed as resolved.

We do not recommend running Nimbus with Dappnode for Lido CSM validators until the issue is conclusively fixed. Consider switching to another consensus client if you’re currently running Nimbus.

## Eth-Docker[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#eth-docker) <a href="#eth-docker" id="eth-docker"></a>

### Set on validator key level

With ETH Docker running (i.e., `ethd up`), run&#x20;

```
./ethd keys list
```

then

```
./ethd keys set-recipient 0xPUBKEY 0xADDRESS 
```

set `0xPUBKEY` with the public key of the key you wish to set a separate fee recipient for, and `0xADDRESS` to the CSM Fee Recipient Address.

* **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
* **Hoodi:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)

### Set on validator and consensus client level

If you're using [Eth-Docker](https://ethdocker.com/) (typically located in `~/eth-docker`), follow these steps to check or set the correct **fee recipient**.

#### Step 1: Edit the `.env` file[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-1-edit-the-env-file) <a href="#step-1-edit-the-env-file" id="step-1-edit-the-env-file"></a>

Open the `.env` file in your Eth-Docker directory:

```
cd ~/eth-docker
nano .env
```

Make sure the following line is present and correctly set:

`FEE_RECIPIENT=0x388C818CA8B9251b393131C08a736A67ccB19297`

important

If the line already exists with a different value, update it to match the correct Lido address.

#### Step 2: Save and exit[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-2-save-and-exit) <a href="#step-2-save-and-exit" id="step-2-save-and-exit"></a>

Save the file and exit your editor (in nano: press `CTRL+O`, `ENTER`, then `CTRL+X`).

#### Step 3: Apply the configuration[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-3-apply-the-configuration) <a href="#step-3-apply-the-configuration" id="step-3-apply-the-configuration"></a>

Run the update command to regenerate and restart the services with the new configuration:

```
./ethd update
./ethd up
```

If the address was already correct, you can keep Eth-Docker running without restarting.

## Sedge[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#sedge) <a href="#sedge" id="sedge"></a>

If you're using [Sedge](https://docs.sedge.nethermind.io/) to manage your validator stack, follow these steps to check or set the correct **fee recipient**.

#### Step 1: Navigate to the `sedge-data` folder[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-1-navigate-to-the-sedge-data-folder) <a href="#step-1-navigate-to-the-sedge-data-folder" id="step-1-navigate-to-the-sedge-data-folder"></a>

```
cd <your-sedge-folder>/sedge-data
```

#### Step 2: Edit the `.env` file[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-2-edit-the-env-file) <a href="#step-2-edit-the-env-file" id="step-2-edit-the-env-file"></a>

```
nano .env
```

Ensure this line exists and is set correctly:

`FEE_RECIPIENT=0x388C818CA8B9251b393131C08a736A67ccB19297`

important

If the line already exists with a different value, update it to match the correct Lido address.

#### Step 3: Save and exit[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-3-save-and-exit) <a href="#step-3-save-and-exit" id="step-3-save-and-exit"></a>

Save the file and exit your editor (in nano: press `CTRL+O`, `ENTER`, then `CTRL+X`).

#### Step 4: Restart Sedge[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-4-restart-sedge) <a href="#step-4-restart-sedge" id="step-4-restart-sedge"></a>

If you made any changes, restart Sedge:

```
./sedge down
./sedge run
```

If the address was already correct, you can keep Sedge running without restarting.

## Stereum[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#stereum) <a href="#stereum" id="stereum"></a>

If you're using [Stereum](https://stereum.net/) to manage your Ethereum node and validators, follow these steps to verify or update the **fee recipient** address.

#### Step 1: Open your Node Page[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-1-open-your-node-page) <a href="#step-1-open-your-node-page" id="step-1-open-your-node-page"></a>

Access the node management interface in Stereum.

#### Step 2: Go to the Validator Client Settings[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-2-go-to-the-validator-client-settings) <a href="#step-2-go-to-the-validator-client-settings" id="step-2-go-to-the-validator-client-settings"></a>

In the interface, locate your validator client and click the **settings icon**.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

#### Step 3: Locate "Default Fee Recipient"[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-3-locate-default-fee-recipient) <a href="#step-3-locate-default-fee-recipient" id="step-3-locate-default-fee-recipient"></a>

Find the field labeled **"Default Fee Recipient"**.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

#### Step 4: Verify or update the address[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-4-verify-or-update-the-address) <a href="#step-4-verify-or-update-the-address" id="step-4-verify-or-update-the-address"></a>

Make sure it is set to: `0x388C818CA8B9251b393131C08a736A67ccB19297`

If the address is missing or incorrect, enter the correct one.

#### Step 5: Confirm and restart[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-5-confirm-and-restart) <a href="#step-5-confirm-and-restart" id="step-5-confirm-and-restart"></a>

Click **"Confirm & Restart"** to save your changes and restart the validator client.

important

Stereum sets the Lido fee recipient automatically, but you should still manually verify it is correct before restarting your node.

## SSV Network[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#ssv-network) <a href="#ssv-network" id="ssv-network"></a>

If you're running CSM validators using [SSV](https://ssv.network/), make sure your **Fee Recipient Address** is set correctly in the SSV dApp.

#### Step 1: Open the SSV dApp[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-1-open-the-ssv-dapp) <a href="#step-1-open-the-ssv-dapp" id="step-1-open-the-ssv-dapp"></a>

Navigate to the [SSV dApp](https://app.ssv.network/) and log in with the wallet that registered your validator cluster.

#### Step 2: Open the fee recipient settings[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-2-open-the-fee-recipient-settings) <a href="#step-2-open-the-fee-recipient-settings" id="step-2-open-the-fee-recipient-settings"></a>

Click on **"Fee Address"** in the top right corner of the screen.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

#### Step 3: Set the correct fee recipient address[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-3-set-the-correct-fee-recipient-address) <a href="#step-3-set-the-correct-fee-recipient-address" id="step-3-set-the-correct-fee-recipient-address"></a>

In the **"Fee Recipient Address"** field, enter: `0x388C818CA8B9251b393131C08a736A67ccB19297`

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

If the field is empty or shows a different address, update it and click **"Update"** to initiate the transaction.

caution

The fee recipient address is set **per wallet**, not per cluster!\
If you're running validators with SSV for other protocols in parallel, you must use a **separate wallet** to set a different fee recipient.

## Obol[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#obol) <a href="#obol" id="obol"></a>

In [Obol](https://obol.org/) DVT setups, the **fee recipient** is configured by the cluster leader during cluster creation.

#### Fee recipient setup options[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#fee-recipient-setup-options) <a href="#fee-recipient-setup-options" id="fee-recipient-setup-options"></a>

* **Using the** [**Obol DV Launchpad**](https://launchpad.obol.org/)**:**\
  If you select **"Lido CSM"** under withdrawal configuration, the fee recipient is automatically set to: `0x388C818CA8B9251b393131C08a736A67ccB19297`

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

* **Using the CLI:**\
  You must manually set the correct fee recipient address when creating the cluster definition file.

caution

Before finalizing the cluster creation, **double-check** that the fee recipient is correctly set. Once the cluster is created, **you cannot change the fee recipient**.\
If the wrong address was set, the only solution is to exit your validators and create a **new cluster** with the correct fee recipient address.

## Systemd[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#systemd) <a href="#systemd" id="systemd"></a>

#### Step 1: Open your validator client’s systemd service file.[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-1-open-your-validator-clients-systemd-service-file) <a href="#step-1-open-your-validator-clients-systemd-service-file" id="step-1-open-your-validator-clients-systemd-service-file"></a>

Typically located in `/etc/systemd/system/`

#### Step 2: Update the service file with the appropriate flag and address:[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-2-update-the-service-file-with-the-appropriate-flag-and-address) <a href="#step-2-update-the-service-file-with-the-appropriate-flag-and-address" id="step-2-update-the-service-file-with-the-appropriate-flag-and-address"></a>

[**Lighthouse**](https://lighthouse-book.sigmaprime.io/validator_fee_recipient.html)[**​**](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#lighthouse)

```
ExecStart=/usr/local/bin/lighthouse vc \
  --suggested-fee-recipient=0x388C818CA8B9251b393131C08a736A67ccB19297 \
  [other flags...]
```

[**Prysm**](https://www.offchainlabs.com/prysm/docs/execution-node/fee-recipient/)[**​**](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#prysm)

```
ExecStart=/usr/local/bin/validator \
  --suggested-fee-recipient=0x388C818CA8B9251b393131C08a736A67ccB19297 \
  [other flags...]
```

[**Teku**](https://docs.teku.consensys.io/how-to/configure/builder-network#example-builder-configurations)[**​**](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#teku)

```
ExecStart=/usr/local/bin/teku/bin/teku validator-client \
  --validators-proposer-default-fee-recipient=0x388C818CA8B9251b393131C08a736A67ccB19297 \
  [other flags...]
```

[**Nimbus**](https://nimbus.guide/suggested-fee-recipient.html)[**​**](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#nimbus)

```
ExecStart=/usr/local/bin/nimbus_validator_client \
  --suggested-fee-recipient=0x388C818CA8B9251b393131C08a736A67ccB19297 \
  [other flags...]
```

[**Lodestar**](https://chainsafe.github.io/lodestar/run/validator-management/vc-configuration#configuring-the-fee-recipient-address)[**​**](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#lodestar)

```
ExecStart=/usr/bin/lodestar validator \
  --suggestedFeeRecipient=0x388C818CA8B9251b393131C08a736A67ccB19297 \
  [other flags...]
```

#### Step 3: Reload and restart the service[​](https://docs.lido.fi/staking-modules/csm/guides/fee-recipient/#step-3-reload-and-restart-the-service) <a href="#step-3-reload-and-restart-the-service" id="step-3-reload-and-restart-the-service"></a>

```
sudo systemctl daemon-reload
sudo systemctl restart <your-validator-service>
```
