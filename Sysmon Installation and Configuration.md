# Splunk Universal Forwarder Installation & Configuration

[← Back to project overview](README.md)

## Installing the Forwarder

For Splunk Enterprise to receive anything from the Windows VM, an agent needed to be running on that VM whose job is to read local log data and ship it off to the indexer. That agent is the Splunk Universal Forwarder. It was downloaded and installed inside the Windows 10 VM, and during setup, "on-premises Splunk Enterprise instance" was selected as the deployment type, since this lab does not use Splunk Cloud.

![Downloading Universal Forwarder](images/figure11_forwarder_download.png)
*Downloading the Splunk Universal Forwarder*

![Forwarder installation in progress](images/figure12_forwarder_install.png)
*Universal Forwarder installation in progress*

![Forwarder setup](images/figure13_forwarder_setup.png)
*Universal Forwarder setup — license agreement and instance type*

## Configuring Log Forwarding

Installing the Forwarder alone does not create a working pipeline — both ends need to agree on where data is going and where it is expected to arrive. On the Windows VM side, the Universal Forwarder was configured with the host machine's IP address (`192.168.23.1`) and port `9997` as its receiving destination. On the Splunk Enterprise side, the platform was configured under Forwarding and Receiving to listen for incoming forwarder connections on that same port. Both sides of this configuration have to match for data to flow, which is why they are documented together here.

![Forwarder receiving config](images/figure14_forwarder_config.png)
*Universal Forwarder configured with the receiving server address and port*

![Splunk configured to receive](images/figure15_splunk_receiving.png)
*Splunk Enterprise configured to receive data on port 9997*

## Confirming the Forwarder Connection

Configuration alone does not guarantee a working connection, so this was verified directly rather than assumed. From the Windows VM's command line, the forward-server status was checked, which confirmed an active forward to `192.168.23.1:9997`. This was then cross-checked from the Splunk Enterprise side by searching Splunk's own internal logs (`index=_internal sourcetype=splunkd`), which returned thousands of events — proof that the Forwarder was not just configured correctly on paper, but actually exchanging data with Splunk Enterprise in real time.

![CLI confirmation of active forward](images/figure16_forwarder_confirm_vm.png)
*Command-line confirmation of an active forward from the Windows VM*

![Splunk search confirming forwarder activity](images/figure17_forwarder_confirm_splunk.png)
*Splunk Enterprise search confirming forwarder activity (index=_internal sourcetype=splunkd)*

---

Next: [Sysmon Installation & Configuration →](Sysmon%20Installation%20and%20Configuration.md)
