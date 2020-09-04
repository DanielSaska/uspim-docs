# Computer Software
# Hardware Drivers
Ensure that all of the used microscope hardware is connected and conifgured properly. For correct operation, you may need to install additional propriatery software or drivers which can generally be found on the manufacturer's website.

National Instruments drivers can be downloaded from the NI website ([https://www.ni.com/en-gb/support/downloads/drivers.html](https://www.ni.com/en-gb/support/downloads/drivers.html)). It is possible to confirm the drivers are installed properly by running NI MAX and identifying the installed NI DAC card ([https://knowledge.ni.com/KnowledgeArticleDetails?id=kA00Z000000P9tuSAC&l=en-GB](https://knowledge.ni.com/KnowledgeArticleDetails?id=kA00Z000000P9tuSAC&l=en-GB)).

# μSPIM Control Server
Download up-to-date version of the control server from releases section of the [uspim-ctrl](https://github.com/DanielSaska/uspim-ctrl/releases) GitHub repository. Alternatively, see [Compiling from Source](/compiling.md) for instructions about how to build the plugin from source. 

## μSPIM Control Server Configuration
Upon first execution, `cfg.json` configuration file is created in the same directory. This file contains all configuration needed for correct interaciton with the National Instruments DAC card. By default, first device is used:
```json
{
	"dev": "Dev1",

	"xMirror1Channel": "AO0",
	"xMirror2Channel": "AO1",
	"laser1Channel": "AO2",
	"laser2Channel": "AO3",
	"zMirror1Channel": "AO4",
	"zMirror2Channel": "AO5",
	"pifocChannel": "AO6",
	"shutterChannel": "AO7",

	"counterSource": "Ctr0InternalOutput",
	"triggerSource": "PFI0",
	"counterChannel": "Ctr0",
	"clockSignalChannel": "Ctr1",
	"clockSignalTerminal": "PFI1"
}
```
If there is multiple NI cards installed in the machine, it may be appropriate to modify the `"dev"` value to the number of the analog output card you wish to use. NI MAX software installed with the NI drivers can be used to identify the NI devices. The analog output channels used can be modified where appropriate, as can the internal trigger/clock sources. Some devices have different capabilities on different channels/sources so it is advisable to use the user manual for your device prior to making any modifications.

# MicroManager
Download Micro-Manager 1.4 from the website ([https://micro-manager.org/wiki/Download_Micro-Manager_Latest_Release](https://micro-manager.org/wiki/Download_Micro-Manager_Latest_Release)). Follow the setup wizard, no special configuration should be required at this stage.

## MicroManager Configuration

**Configure Startup** To start μSPIM Plugin automatically whenever MicroManager is launched, copy `config/MMStartup.bsh` from the [uspim-mm](https://github.com/DanielSaska/uspim-mm/tree/master/config) repository to the directory where MicroManager is installed. In the same directory, modify `ImageJ.cfg`, changing `-Xmx2000m` to 80-90% of the total RAM available, e.g. if your acquisition machine has 64GB, set the java parameter to `-Xmx50000m` to allow allocation of up to 50GB of RAM to MicroManager. This setting will vary greatly, based on application and whether you intend to run other memory-intensive tasks during acquisition on the same machine. It is also possible to modify this parameter through the ImageJ window when MicroManage is launched in `Edit -> Options -> Memory & Threads... -> Maximum memory`.

**Increase Sequence Buffer Size** Launch MicroManager and select a blank configuration if you do not already have one. In the MicroManager window select `Tools -> Options` and increase the Sequence Buffer Size. By default, this 250MB and we found 5000MB to be more than sufficient. Again, this setting will depend on the inended use of the setup. Where fast acquisitions of high-resolution images are required, larger buffer size should be used. Generally 1-5GB should be sufficient for vast majority of applications, as long as the disk write speed is adequate to the acquisition settings. If the machine is unable to keep up with offloading the data to the disk drive, larger buffer is necessary. If you are running into issues with the acquisition stopping prematurely with "Circular buffer overflowed" error, larger buffer may be necessary.

**Configuring Microscope Hardware** Make sure all microscope hardware parts are connected and turned on and launch MicroManager. Select a blank configuration file when MicroManager starts. Under `Tools` select `Hardware Configuration Wizard...`. Keep `Create new configuration` checked and press Next. Configuration here will depend on the parts used. For our setup with ORCA-Flash camera, Omicron LuxX lasers and Thorlabs SC10 shutters, we selected `HamamatsuHam_DCAM`, `Omicron` and `ThorlabsSC10`, adding them to the Installed Device section. For devices such as some mechanical shutters and lasers connected through the COM interface (either directly through COM port or USB interface), it is important to select the correct COM number and BaudRate. On successful configuration, the status should be `OK` for all installed devices. If you have multiple devices of the same kind e.g. lasers or mechanical shutters, it is possible to add them all by adding multiple of the same device, selecting appropriate COM ports that they are connected on. In case of multiple shuttears, you can use a virtual device to control all of them at the same time by adding `Utilities -> Multi Shutter` device. When all devices are configured, press Next. Select your camera and shutter (or combined shutter/cameras). The rest of the configuration can be skipped but ensure you save your configuration in the last step of the wizard. You will then be able to select the configuration file every time you start up MicroManager.

**Configuration setting groups** For both conveniencne of operation and consistant results when using μSPIM for acquisition, it is highly recomended to set up a number of groups and presets for hardware settings. This can be done directly in the main MicroManager window.

Group *CameraTrigger* with presets 'Internal' and 'External' should modify all hardware settings such that the camera triggering is set to be internal and external, respectively.

Group *ScanMode* with presets 'Normal' and any other required should control the scan mode e.g. for 'Normal' it should be Area acquisition, other modes could include rolling shutter, for eexample.
Group *VisibleLaserFront* with presets 'On' and 'Off' should enable and disable the laser in an analogue/digital shuttering mode. 'Front' and 'Side' may be bit misleading as the two VisibleLaser groups refer to the first and second laser.

Group *VisibleLaserSide* - see *VisibleLaserFront*

Group *System* with *Startup* preset should contain all settings that are modified by the groups above or the user. It will be applied automatically on startup of MicroManager and should reset all values to their default state.

!> Note that while configuring the groups is entirely optional, it will be necessary to always set the laser to external triggering mode before acquisition. Whether this is done manually by the user in the device configuration or automatically through the presence of appropriate groups is entirely up to the user.

# μSPIM MicroManager Plugin
Download up-to-date version of the plugin from releases section of the [uspim-mm](https://github.com/DanielSaska/uspim-mm/releases) GitHub repository and copy it to the `mmplugins` subdirectory of the directory where MicroManager is installed. Alternatively, see [Compiling from Source](/compiling.md) for instructions about how to build the plugin from source.

## μSPIM Plugin Configuration
Please see [Calibration](/calibration.md) section regarding calibration. Note the values for each mirror/laser and input them on the *Configuration* tab and save the configuration if you wish to make the settings permanent.

