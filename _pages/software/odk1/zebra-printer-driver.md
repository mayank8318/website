---
title: ODK 1 Zebra Printer Driver
date: 2010-11-09T21:14:19+00:00
author: Yaw Anokwa
layout: page

permalink: /software/odk1/sensors/zebra-printer-driver/
sidenav: software
---

<p>Printing is only possible on devices running Android 3.1 or higher.</p>

<p>Printing is available beginning with ODK Collect 1.3; see the&nbsp;<a href="/1_0_tools/usage_documentation/widget_type_examples/#printing_widgets">Printing Widget</a>&nbsp;section of the Examples page for how to create a form that uses the printer widget and how labels are formatted.</p>

<p>The ODK Zebra Printer Driver has been tested with the MZ220 and MZ320 printers. See the Zebra Technologies&nbsp;<a href="https://www.zebra.com/us/en/products-services/printers/printer-type/mobile/mz-series.html">website</a>&nbsp;for information on that printer.</p>

<h1>Installation</h1>

<ol>
	<li><span style="color:#FF0000">These instructions assume you have already installed ODK Collect 1.3 (or higher) and</span><br />
	<a href="/1_0_tools/sensors">ODK Sensors</a>&nbsp;<span style="color:#FF0000">on your device.</span></li>
	<li><span style="color:#FF0000">Please read all the instructions and notes before beginning.</span></li>
</ol>

<h3>Downloading from Google Play</h3>

<ol>
	<li>From your device's application drawer, choose the Play Store.</li>
	<li>Search for "ODK" choose "ODK Zebra Printer Driver" from "Open Data Kit".</li>
	<li>Select that result and click the Install button. Click OK after viewing the security settings.</li>
</ol>

<h3>Downloading from Web</h3>

<ol>
	<li>From your device's application drawer, choose Settings, then Applications. Make sure Unknown sources is checked.</li>
	<li>Return to the application drawer and choose Browser. Navigate to <a href="/1_0_tools/download">the downloads page</a> and download "ODK Zebra Printer Driver vN.N...apk"</li>
	<li>In the download window, you will see "ODK Zebra Printer Driver vN.N...apk". Select it to download the file. On older devices, the APK will automatically install after you approve the security settings. On newer devices, you must go to the download list, rename the file to restore the .apk extension (the extension will have been renamed to .man during the download process), then click on it to install it.</li>
</ol>

<h1>Configuring the Zebra MZ Series Printer</h1>

<p>The general steps are as follows. For clarifications, please refer to the documentation on the Zebra Technologies website.</p>

<ol>
	<li>Download and install the 'Zebra Setup Utilities' for the MZ Series printers (these utilities include all the necessary printer drivers).</li>
	<li>Connect the MZ series printer to your computer via USB cable and install the printer driver for it on your computer.</li>
	<li>Open the 'Zebra Setup Utilities' tool</li>
	<li>Select your printer.</li>
	<li>Click on the 'Configure Printer Connectivity' button</li>
	<li>Select 'Bluetooth' and advance to the 'Bluetooth settings' screen.</li>
	<li>Set the 'Friendly name' and 'Authentication pin' of your printer.</li>
	<li>Complete the configuration and exit the tool</li>
</ol>

<p>Your Android device will not be able to 'pair' with your printer until it has been given an Authentication PIN; you will need to remember the Friendly name, as it will be how the printer is identified during the configuration process. The MZ series printers do not come with a pre-configured PIN value. If not specified, the friendly name will be the model number of the printer (MZ220 or MZ320). For the following documentation, the 'Authentication PIN' was set to 1234 and the 'Friendly name' was set to HMBPrinter</p>

<h1>Configuring the ODK Zebra Printer Driver</h1>

<p>There are many steps in this process. Many of them are on Android system settings screens to establish communications between your Android device and the printer. Once that is accomplished, there are only a few ODK-specific configuration setting for the driver itself.</p>

<ol>
	<li>
	<ol>
		<li>Click on the 'ODK Zebra Printer' to launch the printer driver. This screen should appear:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s0_zebra_print_screen.png" style="height:493px; width:320px" /></li>
		<li>Click on the 'Print' button. Since no printer has been configured, this screen should appear:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s1_install_printer.png" style="height:493px; width:320px" /></li>
		<li>Click 'OK'. This ODK Sensors configuration screen should appear:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s2_choose_connectivity.png" style="height:494px; width:320px" /></li>
		<li>Click 'Add Bluetooth Device'. This screen should appear:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s3_b4_scan.png" style="height:492px; width:320px" /></li>
		<li>Click 'Device Scan'. This alert may appear (if Bluetooth is not yet enabled under Android's Settings / Wireless &amp; network settings):<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s4_os_enable_bt.png" style="height:493px; width:320px" /><br />
		If it does, click 'Yes'. The list of devices will then populate:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s5_device_list.png" style="height:492px; width:320px" /></li>
		<li>The first time a Bluetooth device has been encountered, before Android has 'paired' with it, it will appear as a cryptic hexadecimal value on this screen (e.g., '00:03:7A:4D:C8:FA'). Click on this cryptic entry. This alert with then appear:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s6_confirm_pairing.png" style="height:494px; width:320px" /></li>
		<li>Click 'Yes'. An Android settings configuration screen will be presented:<br />
		<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s7_os_bt_devices.png" style="height:491px; width:320px" /></li>
	</ol>
	</li>
</ol>

<p>The list under 'AVAILABLE DEVICES' should populate (if not, click on the 'SEARCH FOR DEVICES' button at the bottom of the screen). This list no longer reports the cryptic hexadecimal value from the preceding screen. Instead, it presents the 'Friendly name' for the devices it finds. In this case, we gave our MZ220 a 'Friendly name' of HMBPrinter in the earlier section. Click on that device. The following screen will be presented:<br />
<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s8_bt_pin_entry.png" style="height:494px; width:320px" /></p>

<ul>
	<li>Enter the 'Authentication PIN' from the earlier section (e.g., 1234). The printer should now be successfully paired with your Android. This is indicated by the device moving up into the 'PAIRED DEVICES' section on this screen:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/s9_os_bt_paired.png" style="height:494px; width:320px" /></li>
	<li>Click the back button to exit the Android configuration settings. This returns us to the ODK Sensors configuration screen with the cryptic hexadecimal value for the device:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/sa_sensor_list.png" style="height:493px; width:320px" /></li>
	<li>You can either click on that hexadecimal value, or hit 'Device Scan' (which should cause the hexadecimal value to change to the Friendly name) and click on your printer. This selection dialog should appear:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/sb_choose_printer_driver.png" style="height:491px; width:320px" /></li>
	<li>Select 'Zebra MZ Series Printer' and click 'Select'. The underlying screen should refresh with a check beside the printer indicating that it has been configured with the driver:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/sc_sensor_configured.png" style="height:493px; width:320px" /></li>
	<li>Click the back button to exit the ODK Sensors configuration screen. You are now back to the ODK Zebra Printer Driver screen:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/sd_ready_to_print.png" style="height:493px; width:320px" /></li>
	<li>Click 'Exit print screen' to exit the app.</li>
</ul>

<p>&nbsp;</p>

<p>You have completed the configuration of the printer.</p>

<h1>Using the ODK Zebra Printer</h1>

<p>The usage sequence for the printer from ODK Collect is as follows:</p>

<ol>
	<li>From within ODK Collect, navigate to the print widget. e.g.,<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/collect_printer.png" style="height:480px; width:320px" /></li>
	<li>Click on the 'Initiate Printing' button. This will launch the ODK Zebra Printer app:<br />
	<img alt="" src="/sites/opendatakit-dev.cs.washington.edu/files/images/se_enabled_for_printing.png" style="height:493px; width:320px" /></li>
	<li>At this point, make sure the printer is turned on (green light is illuminated).</li>
	<li>Click on 'Print'. After some time, the blue 'working' light of the printer should illuminate, and then it should print.</li>
	<li>Once printing is complete, click on 'Exit print screen' or click the back button to exit back to ODK Collect.</li>
</ol>

<p>If there is a problem printing, or if you need multiple printouts of the same data, you should be able to hit 'Print' to retry or repeat the printing of the label.</p>

<p>In some cases, particularly if you are changing between configured printers, or needed to set up a new printer, you may need to exit back to ODK Collect and click 'Initiate Printing' to successfully print the label.</p>
