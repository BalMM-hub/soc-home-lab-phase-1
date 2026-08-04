# Splunk Enterprise Installation (Host Machine)

[← Back to project overview](README.md)

With the endpoint in place, the next step was standing up the SIEM that would receive and analyze its logs. Splunk Enterprise was downloaded and installed directly on the host machine rather than inside a VM, so that it could act as a stable, always-available collection point regardless of what was happening inside the lab's virtual machines. During installation, administrator credentials were created for the instance, and after setup completed, a login to the Splunk web interface was used to confirm the installation had succeeded and the platform was ready to receive data.

![Downloading Splunk Enterprise](figure05_splunk_download.png)
*Downloading Splunk Enterprise on the host machine*

![Splunk setup wizard](figure06_splunk_wizard.png)
*Splunk Enterprise setup wizard*

![Splunk installation in progress](figure07_splunk_install.png)
*Splunk Enterprise installation in progress*

![Creating admin credentials](figure08_splunk_credentials.png)
*Creating administrator credentials during setup*

![Splunk sign-in page](figure09_splunk_signin.png)
*Splunk Enterprise sign-in page*

![Splunk home page](figure10_splunk_homepage.png)
*Splunk Enterprise home page, confirming the installation completed successfully*

---

Next: [Splunk Universal Forwarder Installation & Configuration →](Splunk%20Universal%20Forwarder%20Installation%20and%20Configuration.md)
