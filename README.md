# zabbix-GPU-temperature
see how to monitor Nvidia GPUs temperature with zabbix on ubuntu.

run this command to make your drivers up-to-date : 

``$ sudo ubuntu-drivers autoinstall ``

``$ sudo reboot``

Then clone this repository.

After that go ahead and uncomment **UserParameter**=0 and set it to 1 in zabbix_agentd.conf :

``$ sudo nano /etc/zabbix/zabbix_agentd.conf`` 

Add the content of **nvidiaGPUTemp.conf** below it.

Exit nano editor using ``CTRL+x``;

Restart zabbix-agent service ``$ sudo systemctl restart zabbix-agent``

Then open your web browser and go to your zabbix server which in my case is localhost.
> if you don't have zabbix6 installed fallow [this](https://citizix.com/how-to-install-and-configure-zabbix-server-6-on-ubuntu-20-04/) tutorial

From the left modules select **Configuration > Templates**. on the top-right tap on import then on Browse and select **Template nvidiaGPUTemp.xml** and click on import.

Now in the same module select Hosts then click items on the host you want it to be.

On the top-left click on Create item. then fill out the form and type nvidiaGPUTemp in "KEY" input. Set a NAME, Set ***Units*** to °C , ***Update interval*** to 10s and ***Type of information*** to Numeric(float), then add.

Eventually, after a few minutes go ahead and check it on **Monitoring > Host > yourHost**. hit and choose latest data now you can finally see it.

Inspired by [this](https://github.com/B1T0/zabbix-basic-cpu-temperature.git) guy :)
