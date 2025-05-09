# 🖥️ Advanced: Local Grafana Dashboard

## Setup

### Dappnode

* Check if the Dappnode Monitoring Service (DMS) Package is already installed under **Packages**. Else, install it from the Dappstore.&#x20;
* Access your Dappnode interface, go to the DMS Package, and open up the DMS dashboard.&#x20;
* [Video guide](https://www.youtube.com/watch?v=uhEiLQ4sRHo\&ab_channel=SamuelChong)

### EthPillar

Run ethpillar. Then navigate to `21. Toolbox` >> `2. Monitoring: Observe Ethereum Metrics. Explore Dashboards` >> `Install`

### Stereum

You'll find a button too open Grafana at the top of the launcher screen. Click there and Stereum will open the local instance in your browser.

<figure><img src="../.gitbook/assets/Stereum ETH Home Staking Curriculum copy (1).png" alt=""><figcaption></figcaption></figure>

### Sedge

**Sedge** deploys validators using Docker Compose and includes optional support for Grafana and Prometheus.

* If you enabled monitoring during setup, Prometheus and Grafana containers should be running
* You can edit your `docker-compose.yaml` or `.env` file to adjust data retention or expose metrics

### Eth Docker

No additional steps required.

### Systemd (Validator Client add-on only)

Edit the `prometheus.yml` configuration file.

```sh
sudo nano /etc/prometheus/prometheus.yml
```

According to your selected validator client, append the following block to your existing configuration.

{% tabs %}
{% tab title="Teku" %}
```
  - job_name: "csm_teku_validator"
    scrape_timeout: 10s
    metrics_path: /metrics
    scheme: http
    static_configs:
      - targets: ["localhost:8108"]
```
{% endtab %}

{% tab title="Nimbus" %}
```
  - job_name: 'csm_nimbus_validator'
    metrics_path: /metrics
    static_configs:
      - targets: ['localhost:8108']
```
{% endtab %}

{% tab title="Lodestar" %}
```
  - job_name: 'csm_lodestar_validator'
    metrics_path: /metrics
    static_configs:
      - targets: ['localhost:5064']
```
{% endtab %}

{% tab title="Lighthouse" %}
```
  - job_name: 'csm_lighthouse_validator'
    metrics_path: /metrics
    static_configs:
      - targets: ['localhost:8108']
```
{% endtab %}

{% tab title="Prysm" %}
```
  - job_name: 'csm_prysm_validator'
    metrics_path: /metrics  
    static_configs:
      - targets: ['localhost:8108']
```
{% endtab %}
{% endtabs %}

Once you're done, save with `Ctrl+O` and `Enter`, then exit with `Ctrl+X`.

Reload the systemd daemon to register the changes made, start Prometheus, and check its status to make sure it's running.

```bash
sudo systemctl daemon-reload
sudo systemctl start prometheus.service
sudo systemctl status prometheus.service
```

Monitor the logs for any warnings or errors:

```bash
sudo journalctl -fu prometheus -o cat | ccze -A
```

#### Configure Grafana Dashboard

* Refer to [Accessing your Grafana Dashboard](advanced-local-grafana-dashboard.md#accessing-your-grafana-dashboard) below for access instructions
* Select `Data Sources` and click on `Add data source` , then choose **Prometheus** and enter [**http://localhost:9090**](http://localhost:9090) for the URL
* Setup dashboards - On the left menu bar, click on **Dashboards >> Import**
  * **Teku:** Enter the dashboard ID - `16737`
  * **Nimbus:** Paste the JSON text from the options below
    * [Nimbus Github](https://raw.githubusercontent.com/status-im/nimbus-eth2/stable/grafana/beacon_nodes_Grafana_dashboard.json)
    * [Metanull](https://github.com/metanull-operator/eth2-grafana/blob/master/nimbus/eth2-grafana-nimbus-dashboard.json)
  * **Lodestar:** Paste the JSON text from [here](https://raw.githubusercontent.com/ChainSafe/lodestar/stable/dashboards/lodestar_summary.json)
  * **Lighthouse**: Paste the JSON text from [here](https://raw.githubusercontent.com/sigp/lighthouse-metrics/master/dashboards/Summary.json)
  * **Prysm:** Paste the JSON text from [here](https://raw.githubusercontent.com/GuillaumeMiralles/prysm-grafana-dashboard/master/less_10_validators.json)
* If using the same validator client as your existing solo staking setup, select the `csm_"VALIDATOR"_client` from the JOB selection drop-down menu on the Grafana dashboard of your existing validator client.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-19 at 3.17.03 PM (2).png" alt=""><figcaption></figcaption></figure>

## Accessing your Grafana Dashboard

To access your Grafana dashboard,&#x20;

* **From home:** Connect your laptop to the same WiFi network as your node, then navigate to `http://INTERNAL_IP:3000` on your web browser
* **Outside of home:**&#x20;
  * Create an SSH tunnel by running `ssh -L 3000:INTERNAL_IP:3000 USERNAME@EXTERNAL_IP -p PORT -i PATH_TO_SSH_KEY -v` then navigate to `http://127.0.0.1:3000` on your browser
  * [Install and setup Tailscale VPN](../useful-tools/advanced-networking.md#vpn) on both your node and your laptop. Then navigate to `http://TAILSCALE_ASSIGNED_IP:3000` on your browser

The default login is `admin / admin` and you will be prompted to change your password during your first login.

Dashboards for Consensus clients, Execution clients, and validator performance are included
