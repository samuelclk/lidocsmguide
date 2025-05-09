# Dappnode

**Dappnode** is an open-source node management software with a very abstracted user interface and experience. Perfect for begginners or operators looking for max comfort on their setup.

## Full Node Setup <a href="#lido-csm-testnet-workflow" id="lido-csm-testnet-workflow"></a>

{% hint style="info" %}
Machines purchased from the Dappnode store are plug and play, if you're planning to use Dappnode on a custom-build machine, it must be running Debian. You can follow the official installation guide [here](https://www.debian.org/devel/debian-installer/).
{% endhint %}

### Video Guide

{% embed url="https://youtu.be/n31bSAn2IuM?si=RoLjNML8JArVVtGz" %}

You can also see a full video-guide to install and setup Dappnode and Lido CSM on [Mainnet](https://youtube.com/playlist?list=PLS0yTNR46xvGJP1H09iRFxKK09vrNTqBp\&si=wx75jG1VC6s_nLFM) and [Testnet](https://youtube.com/playlist?list=PLS0yTNR46xvEkuuWuiucxo0ZJ8W3wPpx1\&si=guuiaiEuwYYwEt2X).

{% hint style="warning" %}
For Testnet setups, replace all Holesky options with Hoodi
{% endhint %}

## Installing Dappnode

Dappnode sells plug-and-play machines with everything installed, like this [Lido version](https://dappnode.com/collections/frontpage/products/home-lido).

If you want to run Dappnode on a DYOR machine you can install it by:

* Installing an [ISO](https://docs.dappnode.io/docs/user/install/iso) that automatically installs Debian & Dappnode.
* Installing Debian on your machine and then install Dappnode via a [script](https://docs.dappnode.io/docs/user/install/script).

You'll interact with Dappnode via a web-based UI, and to access it remotely you'll need a VPN. The steps are covered in the video guide below.

* **Tailscale VPN:** We recommend installing Tailscale for easy remote access to your Dappnode interface.

{% embed url="https://www.youtube.com/watch?ab_channel=SamuelChong&index=8&list=PLS0yTNR46xvEkuuWuiucxo0ZJ8W3wPpx1&v=jdLPUo6VK_A" %}

* **Wireguard VPN:** Older alternative remote access method

{% embed url="https://www.youtube.com/watch?ab_channel=Dappnode&v=qB0sMaNpXpU" %}

## Configure Dappnode to run Lido CSM

### Setting up the Full Node

With your VPN activated, open [my.dappnode](http://my.dappnode/) and head to the [Stakers](http://my.dappnode/stakers/ethereum) tab. Select the network you'll run your nodes on (Mainnet or Hoodi), Execution and Consensus clients of your preference, also click on Web3signer and select some of the MEV-Boost relays listed [here](https://operatorportal.lido.fi/existing-operator-portal/ethereum-onboarding/mev-relays).

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Then scroll down and click on `Apply changes`. Wait a few minutes for dappnode to install the packages, you will be able to see the chain syncing on the Dashboard.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Installing the Lido CSM package

1. Go to the [DAppStore](http://my.dappnode/installer/dnp) tab and look for the Lido Csm Mainnet/Hoodi package. Click `GET` and follow the steps to install it.
2. After it's installed, open the Lido Csm package in the [Packages](http://my.dappnode/packages/my) tab and click on the UI.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-17 at 16.01.12.png" alt=""><figcaption></figcaption></figure>

You'll see a user interface equal to the Lido CSM Widget. To make deposits you can follow the [lido-csm-widget](../../lido-csm-widget/ "mention") guide. Additionally, because it runs locally and has access to your setup, the built-in UI in the package has some extra features:

* Upload your Keystores in the UI together with the Deposit Data
* See the status of Execution and Consensus clients from the Dashboard tab
* A Notifications tab to set up a Telegram Bot for important messages

## Update clients

If there's updates available to your clients they'll appear on the right-hand side of the Dashboard:

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

You'll be prompted to enable automatic updates for all your packages, we recommend manually updating to avoid update errors at times when you can't solve them.

***

You can read more about Dappnode in their [official documentation](https://docs.dappnode.io/docs/user/getting-started/choose-your-path).
