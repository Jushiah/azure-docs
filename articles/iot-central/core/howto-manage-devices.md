---
title: Manage the devices in your Azure IoT Central application | Microsoft Docs
description: Learn how to manage devices in your Azure IoT Central application. Learn how to manage individual devices and do bulk import and exports of the devices in your application.
author: dominicbetts
ms.author: dobett
ms.date: 10/08/2020
ms.topic: how-to
ms.service: iot-central
services: iot-central
manager: peterpr
ms.custom: contperf-fy21q2

# Operator
---

# Manage devices in your Azure IoT Central application

This article describes how you manage devices in your Azure IoT Central application. You can:

- Use the **Devices** page to view, add, and delete devices connected to your Azure IoT Central application.
- Import and export devices in bulk.
- Maintain an up-to-date inventory of your devices.
- Keep your device metadata up to date by changing the values stored in the device properties from your views.
- Control the behavior of your devices by updating a setting on a specific device from your views.

To learn how to manage custom groups of devices, see [Tutorial: Use device groups to analyze device telemetry](tutorial-use-device-groups.md).

## View your devices

To view an individual device:

1. Choose **Devices** on the left pane. Here you see a list of all devices and of your device templates.

1. Choose a device template.

1. In the right-hand pane of the **Devices** page, you see a list of devices created from that device template. Choose an individual device to see the device details page for that device:

    ![Device Details Page](./media/howto-manage-devices/device-list.png)

## Add a device

To add a device to your Azure IoT Central application:

1. Choose **Devices** on the left pane.

1. Choose the device template from which you want to create a device.

1. Choose + **New**.

1. Turn the **Simulated** toggle to **On** or **Off**. A real device is for a physical device that you connect to your Azure IoT Central application. A simulated device has sample data generated for you by Azure IoT Central.

1. Select **Create**.

1. This device now appears in your device list for this template. Select the device to see the device details page that contains all views for the device.

## Import devices

To connect large number of devices to your application, you can bulk import devices from a CSV file. You can find an example CSV file in the [Azure Samples repository](https://github.com/Azure-Samples/iot-central-docs-samples/tree/master/bulk-upload-devices). The CSV file should include the following column headers:

| Column | Description 
| - | - | 
| IOTC_DEVICEID | The device ID is a unique identified this device will use to connect. The device ID can contain letters, numbers, and the `-` character without any spaces. |
| IOTC_DEVICENAME | Optional. The device name is a friendly name that will be displayed throughout the application. If not specified, this will be the same as the device ID.   |



To bulk-register devices in your application:

1. Choose **Devices** on the left pane.

1. On the left panel, choose the device template for which you want to bulk create the devices.

    > [!NOTE]
    > If you don't have a device template yet then you can import devices under **All devices** and register them without a template. After devices have been imported, you can then migrate them to a template.

1. Select **Import**.

    ![Import Action](./media/howto-manage-devices/bulk-import-1.png)


1. Select the CSV file that has the list of Device IDs to be imported.

1. Device import starts once the file has been uploaded. You can track the import status in the Device Operations panel. This panel appears automatically after the import starts or you can access it through the bell icon in the top right-hand corner.

1. Once the import completes, a success message is shown in the Device Operations panel.

    ![Import Success](./media/howto-manage-devices/bulk-import-2.png)

If the device import operation fails, you see an error message on the Device Operations panel. A log file capturing all the errors is generated that you can download.

## Migrate devices to a template

If you register devices by starting the import under **All devices**, then the devices are created without any device template association. Devices must be associated with a template to explore the data and other details about the device. Follow these steps to associate devices with a template:

1. Choose **Devices** on the left pane.

1. On the left panel, choose **All devices**:

    ![Unassociated Devices](./media/howto-manage-devices/unassociated-devices-1.png)

1. Use the filter on the grid to determine if the value in the **Device Template** column is **Unassociated** for any of your devices.

1. Select the devices you want to associate with a template:

1. Select **Migrate**:

    ![Associate Devices](./media/howto-manage-devices/unassociated-devices-2.png)

1. Choose the template from the list of available templates and select **Migrate**.

1. The selected devices are associated with the device template you chose.

## Export devices

To connect a real device to IoT Central, you need its connection string. You can export device details in bulk to get the information you need to create device connection strings. The export process creates a CSV file with the device identity, device name, and keys for all the selected devices.

To bulk export devices from your application:

1. Choose **Devices** on the left pane.

1. On the left pane, choose the device template from which you want to export the devices.

1. Select the devices that you want to export and then select the **Export** action.

    ![Export](./media/howto-manage-devices/export-1.png)

1. The export process starts. You can track the status using the Device Operations panel.

1. When the export completes, a success message is shown along with a link to download the generated file.

1. Select the **Download File** link to download the file to a local folder on the disk.

    ![Export Success](./media/howto-manage-devices/export-2.png)

1. The exported CSV file contains the following columns: device ID, device name, device keys, and X509 certificate thumbprints:

    * IOTC_DEVICEID
    * IOTC_DEVICENAME
    * IOTC_SASKEY_PRIMARY
    * IOTC_SASKEY_SECONDARY
    * IOTC_X509THUMBPRINT_PRIMARY
    * IOTC_X509THUMBPRINT_SECONDARY

For more information about connection strings and connecting real devices to your IoT Central application, see [Device connectivity in Azure IoT Central](concepts-get-connected.md).

## Delete a device

To delete either a real or simulated device from your Azure IoT Central application:

1. Choose **Devices** on the left pane.

1. Choose the device template of the device you want to delete.

1. Use the filter tools to filter and search for your devices. Check the box next to the devices to delete.

1. Choose **Delete**. You can track the status of this deletion in your Device Operations panel.

## Change a property

Cloud properties are the device metadata associated with the device, such as city and serial number. Cloud properties only exist in the IoT Central application and aren't synchronized to your devices. Writable properties control the behavior of a device and let you set the state of a device remotely, for example by setting the target temperature of a thermostat device.  Device properties are set by the device and are read-only within IoT Central. You can view and update properties on the **Device Details** views for your device.

1. Choose **Devices** on the left pane.

1. Choose the device template of the device whose properties you want to change and select the target device.

1. Choose the view that contains properties for your device, this view enables you to input values and select **Save** at the top of the page. Here you see the properties your device has and their current values. Cloud properties and writable properties have editable fields, while device properties are read-only. For writable properties, you can see their sync status at the bottom of the field. 

1. Modify the properties to the values you need. You can modify multiple properties at a time and update them all at the same time.

1. Choose **Save**. If you saved writable properties, the values are sent to your device. When the device confirms the change for the writable property, the status returns back to **synced**. If you saved a cloud property, the value is updated.

## Next steps

Now that you've learned how to manage devices in your Azure IoT Central application, the suggested next step is to learn how to[Configure rules](howto-configure-rules.md) for your devices.
