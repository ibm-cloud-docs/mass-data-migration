---

copyright:
  years: 2017, 2020, 2021
lastupdated: "2021-03-25"

keywords: set up device, connect device, cable device

subcollection: mass-data-migration

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:preview: .preview}
{:term: .term}

# Connecting the device
{: #connect-device}

{{site.data.keyword.mdms_full}} devices arrive pre-configured and ready to connect to your network.
{: shortdesc}

Before you power on the {{site.data.keyword.mdms_short}} device:

- Ensure that the Mass Data Migration device is at room temperature.
- Ensure that there is no condensation on the device.
- Verify that you received the cables that correspond with your [device model](/docs/mass-data-migration?topic=mass-data-migration-device-overview) by reviewing the inventory list that is located under the transport case lid.
- To avoid inadvertent damage to the device, keep the device in its portable case while the device is in use.

## Step 1. Power on the device
{: #power-on-device}

After you position the device, use the supplied power cord to power on the device.

1. Retrieve the power cord that is located under the transport case lid.
2. Attach the power cord to the inlet on the device, and then connect the plug to a power socket.
3. Set the **Mains Switch** to **On**.
4. Power on the device by using the **System On / Off** button.

   When a System ID value displays on the _System Control Display_ screen, the device is powered on and ready for the next step.

## Step 2. Connect the device
{: #connect-device-to-network}

To connect the device to your network, you need to configure two Ethernet connections. The first connection is for managing the device through a browser, and the second connection is for moving data across the same subnet where the source data is located.

Configure Ethernet connectivity for your device depending on the [{{site.data.keyword.mdms_short}} device model](/docs/mass-data-migration?topic=mass-data-migration-device-overview#mass-data-migration-device-models) that you receive. 

### Connecting the RJ45 model
{: #set-up-RJ45-model}

The RJ45 device model natively supports Ethernet connectivity by using RJ45 connectors.

To learn about setting up a RJ45 / SFP+ device model, see [Connecting the RJ45 / SFP+ model](#set-up-SFP+-model).
{: note}

<a href="https://{DomainName}/docs/api/content/mass-data-migration/images/mdms-device-rj45.svg">
  <img src="images/mdms-device-rj45.svg" alt="Top-down view of the Mass Data Migration device">
</a>

You can use the supplied CAT6A Ethernet cables to connect your storage system to the RJ45 network ports on the device. If you need to enable SFP+ copper support, use the supplied adapters. The adapters are compatible with all switch manufacturers. You can find the adapters in a pocket on the underside of the shipping container lid.

The following table shows how the physical ports on the device map to the ports that are displayed in the UI.

| Device port | Ethernet type  |  Description |
| --- | --- | --- | --- |
| Eth1 | 1Gb | The Eth1 port is used to manage the device and make the web-based UI available outside the data subnet. You can view the gateway information by using the _System Control Display_ screen after the device is powered on. |
| Eth3 | 10Gb | The Eth3 port is used to transfer data from your storage system onto the {{site.data.keyword.mdms_short}} device. The connection must either be on the same subnet as the source data or directly connected to the server. |
{: caption="Table 2. Describes how {{site.data.keyword.mdms_short}} device ports map to the UI display." caption-side="top"}

To connect the RJ45 device model to your network:

1. Retrieve the CAT6A cable from the transport case lid.
2. Connect the CAT6A cable to the Eth3 (`10GbE-B`) port on the device.
3. Connect the CAT6A cable to the SFP+ adapter.
4. Connect the CAT6A cable to your 10Gb Ethernet switch.
5. Open a web browser, and navigate to the following URL.

   ```
   https://<your_Eth3_IP_address>
   ```
   {: codeblock}

   Replace `<your_Eth3_IP_address>` with the IP address that is configured for the Eth3 network port. To view the IP address, check the _System Control Display_ screen on the device.
6. Optional: If you can't reach the IP address, connect the CAT6A cable to the Eth1 (`1GbE-B`) port on the device and try again by navigating to the following URL.
   
   ```
   https://<your_Eth1_IP_address>
   ```
   {: codeblock}

   Replace `<your_Eth1_IP_address>` with the IP address that is configured for the Eth1 network port. To view the IP address, check the _System Control Display_ screen on the device.

   If you need to modify the IP settings for Eth3 or Eth1, see [Reviewing your network settings](#review-network-settings).
   {: tip}

### Connecting the RJ45 / SFP+ model
{: #set-up-SFP+-model}

The RJ45 / SFP+ device model natively supports both RJ45 and SFP+ copper connections. 

To learn about setting up a RJ45 device model that doesn't include SFP+ connections, see [Connecting the RJ45 model](#set-up-RJ45-model).
{: note}

<a href="https://{DomainName}/docs/api/content/mass-data-migration/images/mdms-device-sfp.svg">
  <img src="images/mdms-device-sfp.svg" alt="Top-down view of the Mass Data Migration device">
</a>

You can use the supplied CAT6A and SFP+ cables to connect your storage system to the network ports on the device. 
The following table shows how the physical ports on the device map to the ports that are displayed in the UI.

| Device port | Ethernet type  |  Description |
| --- | --- | --- | --- |
| Eth5 | 10Gb (SFP+) | The Eth5 port is used to transfer data from your storage system onto the {{site.data.keyword.mdms_short}}. This port can also be used to manage the device. The port runs only at 10GbE speed. |
| Eth2 | 10Gb | The Eth2 port is used to manage the device and make the web-based UI available outside the data subnet. This port can also be used for data transfer. The connection must either be on the same subnet as the source data or directly connected to the server. The port can run at speeds of either 1Gb or 10Gb. |
{: caption="Table 3. Describes how {{site.data.keyword.mdms_short}} device ports map to the UI display." caption-side="top"}

To connect the RJ45 / SFP+ device model to your network:

1. Retrieve the SFP+ copper cable from the transport case lid.
2. Connect the SFP+ cable to the Eth5 (`10GbE (5)`) port on the device.
3. Connect the SFP+ cable to your 10Gb Ethernet switch.
4. Open a web browser, and navigate to the following URL.

   ```
   https://<your_Eth5_IP_address>
   ```
   {: codeblock}

   Replace `<your_Eth5_IP_address>` with the IP address that is configured for the Eth5 network port. To view the IP address, check the _System Control Display_ screen on the device.
5. Optional: If you can't reach the IP address, connect the SFP+ cable to the Eth2 (`10GbE-B` or `1GbE-B`) port on the device and try again by navigating to the following URL.
   
   ```
   https://<your_Eth2_IP_address>
   ```
   {: codeblock}

   Replace `<your_Eth2_IP_address>` with the IP address that is configured for the Eth2 network port. To view the IP address, check the _System Control Display_ screen on the device.

   If you need to alter any IP settings for Eth3 or Eth1, see the [Reviewing your network settings](/docs/mass-data-migration?topic=mass-data-migration-ip-settings).
   {: tip}

## Next steps
{: #set-up-device-next-steps}

- Interact with the device by [running the web-based UI](/docs/mass-data-migration?topic=mass-data-migration-access-ui).
- To prepare for the data copy process, start by [unlocking the storage pool on the device](/docs/mass-data-migration?topic=mass-data-migration-unlock-storage-pool).
