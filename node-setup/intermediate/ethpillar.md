# EthPillar

## Full Node Setup <a href="#lido-csm-testnet-workflow" id="lido-csm-testnet-workflow"></a>

### Video guide <a href="#video-guide" id="video-guide"></a>

{% embed url="https://youtu.be/aZLPACj2oPI" %}

{% hint style="warning" %}
For Testnet setups, replace all Holesky options with Hoodi
{% endhint %}

### Download EthPillar

Go to the [Coincashew website](https://www.coincashew.com/coins/overview-eth/ethpillar) and copy the latest 1-line installation command and paste it into your terminal.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/coincashew/EthPillar/main/install.sh)"
```

Then, type + enter `ethpillar` and follow along the prompts in the terminal UI (TUI) to:

1. Sync an execution client and a Consensus + Validator Client
2. <mark style="color:red;">**\[For Testnet only]**</mark> `Yes` for **generate validator keys.** Generate validator keys to participate in the Lido CSM
   * Choose how many validator keys to generate and set the password for the key
   * Save your 24-word mnemonic
3. <mark style="color:green;">**\[For Mainnet]**</mark> `No` for **generate validator keys.** Generate your validator keys using a secure process ([key-generation-for-mainnet](../../generating-validator-keys/key-generation-for-mainnet/ "mention")) before resuming the steps below.&#x20;
4. Verify the Fee Recipient and withdrawal address on the [CSM Operator Portal](https://operatorportal.lido.fi/modules/community-staking-module)
5. Import the generated validator keys onto your validator client

{% tabs %}
{% tab title="Withdrawal Address" %}
* **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
* **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)
{% endtab %}

{% tab title="Fee Recipient Address" %}
* **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
* **Hoodi:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
It is highly recommended to use a [secure key generation workflow](../../generating-validator-keys/key-generation-for-mainnet/) in a later section for Mainnet
{% endhint %}

Copy the deposit data generated by the command below for uploading onto the Lido CSM Widget.

* **Mainnet:** [https://csm.lido.fi/](https://csm.lido.fi/)
* **Hoodi:** [https://csm.testnet.fi/](https://csm.testnet.fi/)

```
cat ~/staking-deposit-cli/validator_keys2024-08-23-063857/deposit*json
```

#### ETHPillar TUI Navigation <a href="#ethpillar-tui-navigation" id="ethpillar-tui-navigation"></a>

1. `Arrow keys & Tab key`: Cycle options
2. `Space bar`: Select option
3. `Enter`: Confirm option
4. `CTRL+B`, then `D`: Exit split-screen monitoring view
5. `CTRL+C`: Exit individual screen monitoring view
6. `exit` command (type "exit" and `enter` in terminal) : Exit current terminal

## Setup additional CSM validator client only

{% tabs %}
{% tab title="EthPillar CSM VC Additional Plugin" %}
This option allows you to use EthPillar to spin up an additional validator client on top of your existing EthPillar setup with a separate Fee Recipient Address set to the Lido Execution Layer Rewards Vault. You will import your CSM validator keys on this EthPillar validator client.

Run `ethpillar`to activate the Terminal UI.

* Select `Plugins`>>`Lido CSM Validator: Activate an extra validator service. Re-use this node's EL/CL.`

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-13 at 1.03.17 AM.png" alt=""><figcaption></figcaption></figure>

* Enter the Fee Recipient Address as the `Lido Execution Layer Rewards Vault`.
  * **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
  * **Hoodi:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)
* While selecting the **Separate Lido CSM Validator** menu option, generate and import CSM validator keys.
  * **Mainnet:** [`0xB9D7934878B5FB9610B3fE8A5e441e8fad7E293f`](https://etherscan.io/address/0xb9d7934878b5fb9610b3fe8a5e441e8fad7e293f)&#x20;
  * **Hoodi:**  [`0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2`](https://hoodi.etherscan.io/address/0x4473dCDDbf77679A643BdB654dbd86D67F8d32f2)

{% hint style="danger" %}
It is highly recommended to use a [secure key generation workflow](../../generating-validator-keys/key-generation-for-mainnet/) in a later section for Mainnet
{% endhint %}

Generate and import CSM validator keys.

{% content-ref url="../../generating-validator-keys/" %}
[generating-validator-keys](../../generating-validator-keys/)
{% endcontent-ref %}
{% endtab %}

{% tab title="EthPillar CSM VC + Existing Setup" %}
This option allows you to use EthPillar to spin up a separate validator client where you can set a separate Fee Recipient Address on (i.e., Lido Execution Layer Rewards Vault). You will import your CSM validator keys on this EthPillar validator client. You can connect this validator client to your existing beacon node.&#x20;

Run `ethpillar` to active the Terminal UI.

Select `4 - Lido CSM Validator Client Only`.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Enter your consensus client (beacon node) address. **Example:** http://127.0.0.1:5052

Verify the `fee_recipient` address is set to the `Lido Execution Layer Rewards Vault`.

* **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
* **Hoodi:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)

Generate and import CSM validator keys.

{% content-ref url="../../generating-validator-keys/" %}
[generating-validator-keys](../../generating-validator-keys/)
{% endcontent-ref %}
{% endtab %}
{% endtabs %}
