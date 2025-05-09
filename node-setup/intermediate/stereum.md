# Stereum

**Stereum** is an open-source toolkit that simplifies setting up and managing Ethereum nodes, supporting solo staking and integrations like Lido’s Community Staking Module (CSM) described here.

It provides an intuitive UI and automation tools, making node deployment and maintenance more accessible for validators.

## Full Node Setup <a href="#lido-csm-testnet-workflow" id="lido-csm-testnet-workflow"></a>

{% hint style="info" %}
To use Stereum your machine must be running Ubuntu. You can follow the official installation guide [here](https://ubuntu.com/tutorials/install-ubuntu-desktop).
{% endhint %}

### Video Guide

{% embed url="https://youtu.be/v5k1nlDajyI?si=wAM35LSC_Wk7I7RQ" %}

### Configure Passwordless Sudo

Stereum requires passwordless `sudo` access to function properly. Follow these steps to configure it:

1.  Log into your server and run the following command to edit the `visudo` file:

    ```
    sudo visudo
    ```
2.  Add the following line under `includedir /etc/sudoers.d` (replace `<username>`with your actual username):

    ```
    <username> ALL=(ALL) NOPASSWD: ALL
    ```
3. Restart your session or log out and back in to apply the changes.
4. Verify your passwordless sudo setup by running `sudo -l`. If no password is requested, it's configured correctly and you are ready to use Stereum.

### Download the Stereum Launcher

Head to [stereum.net](https://stereum.net/) and download the launcher for your current operative system. We're using MacOS in this guide.

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

### Configure the Stereum Launcher to run Lido CSM

Once installed, fill the login information for your server. Note that you can save the information for multiple servers in the launcher for easier access.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

At login, you will be asked to select between three different installation methods:

* Import a configuration from a previous Stereum setup
* Do a custom installation
* One-click installation

We'll go with the one-click installation

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-03-18 a la(s) 20.58.41.png" alt=""><figcaption></figcaption></figure>

Now, we will select the network and CSM as the use case. We recommend trying the setup on a testnet first if this is your first time running an Ethereum node!

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-03-18 a la(s) 20.59.12 (1).png" alt=""><figcaption></figcaption></figure>

After choosing the use case you will be able to see what services will be installed, and select the execution, consensus and validator clients you want to run on your setup.

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-03-18 a la(s) 20.59.33.png" alt=""><figcaption></figcaption></figure>

On the following screens you will select the relays for MEV Boost and how you prefer your nodes to sync. By default Stereum selects all relays [vetted by Lido](https://enchanted-direction-844.notion.site/6d369eb33f664487800b0dedfe32171e?v=8e5d1f1276b0493caea8a2aa1517ed65), but you can pick and choose based on your preference. For syncing your consensus client we recommend using Checkpoint Sync with any of the sources in the dropdown menu.

After confirming your setup you're ready to go! Stereum will install all the services automatically.

### Check your Setup and upload the Validator Keys

After Stereum is done installing everything you'll have access to a view of your server in the launcher. Let's verify  that all the services were installed and configured correctly.

Start by opening the Setup. There you should see the following services:

* Execution, consensus and validator clients
* Flashbots MEV Boost
* Lido Keys API & Validator Ejector
* Prometheus, Grafana, CSM Monitoring and Kubo IPFS

<figure><img src="../../.gitbook/assets/image copia (4).png" alt=""><figcaption></figcaption></figure>

Check the logs of every client and confirm that they started syncing. After this make sure that the validator client has the Fee Recipient set to Lido's Execution Layer Rewards Vault with the respective addresses:

* **Mainnet:** [`0x388C818CA8B9251b393131C08a736A67ccB19297`](https://etherscan.io/address/0x388C818CA8B9251b393131C08a736A67ccB19297)
* **Hoodi:** [`0x9b108015fe433F173696Af3Aa0CF7CDb3E104258`](https://hoodi.etherscan.io/address/0x9b108015fe433F173696Af3Aa0CF7CDb3E104258)

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-03-18 a la(s) 21.23.11.png" alt=""><figcaption></figcaption></figure>

If all these check out, you are good to go!&#x20;

## Generate Validator Keys

We can proceed to generate validator keys according to this section: [Generating Validator Keys](../../generating-validator-keys/). Remember to double check that you configured them with the correct Withdrawal Address.

## Importing Validator Keys

Head to the Staking tab in the Stereum Launcher, and drag-&-drop the Keystores.&#x20;

1. Select the Validator Client configured with the Lido Execution Layer Rewards Vault as the Fee Recipient Address.&#x20;
2. Enter the password and click on the checkmark.&#x20;
3. After a few seconds your keys will be imported and your Staking tab should look like this:

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Now you're ready to upload the deposit data in the Lido CSM UI:

{% content-ref url="../../lido-csm-widget/" %}
[lido-csm-widget](../../lido-csm-widget/)
{% endcontent-ref %}

***

You can read more about Stereum in their [official documentation](https://stereum-dev.github.io/ethereum-node-web-docs/docs/intro).

