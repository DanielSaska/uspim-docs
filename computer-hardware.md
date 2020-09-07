# Computer Hardware

The computer specifications necessary for optimal function and acquisition of the setup are highly dependent on the acquisition requirements. For large field of view and high acquisition speeds, the acquisition produces large datasets, making the process highly storage-dependent. State-of-the-art acquisition cameras are able to reach 4 megapixel resolution at 100 Hz and 16 bit depth, producing a theoretical throughput of 838.9 MB/s. This poses a write speed requirement higher than that which can be satisfied by a regular SATA3 storage interface which is limited to a theoretical maximum of 600 MB/s. It is therefore highly recommended to utilize a faster storage solution, such as fast PCI-based solid state disk (SSD) storage (e.g. Intel Optane 905p) or hardware SSD RAID. The acquisition is not highly CPU dependent and neither µSPIM Toolset nor MicroManager take a significant advantage in parallel processing. A state-of-the-art consumer line 4- or 6-core CPU is sufficient for optimal performance. Due to the continuous high data throughput, it is recommended to use a secondary computer for stimulation and/or other intensive tasks to avoid potential performance issues caused by the multiple tasks competing for computational resources or ensuring that this is not the case when a single machine is used.

µSPIM Toolset relies on a number of microscope components controlled by an analogue signal including galvanometer mirrors, software laser shutters, camera trigger and the piezoelectric stage. These control signals are produced by National Instrument DAC adapter. While µSPIM Toolset allows for incomplete configurations e.g. single light path with unmodulated laser and single sheet-generating scanning mirror, to support the full functionality, the National Instruments DAC card must support at least 8 analogue outputs with no need for analogue or digital inputs as the control is fully feed-forward and does not require any feedback from the hardware.

## Example Computer Hardware Setup
| Computer Parts   | Component                                                                                |
|------------------|------------------------------------------------------------------------------------------|
| CPU              | Intel Xeon Gold 5122                                                                     |
| RAM              | 128GB (2x64GB) DDR4 ECC LR Memory                                                        |
| Motherboard      | Supermicro X11DPL-i                                                                      |
| GPU              | NVIDIA Quatro P620                                                                       |
| Storage          | Samsung PM883 960GB SATA (general storage) <br/> Samsung 970 EVO 2TB M.2 (acquisition storage) |
| Frame Grabber    | Firebird Camera Link (2xCLM-2PE8) (Active Silicon)                                       |
| DAC card         | PCIe-6738 (National Instruments)                                                         |
| Operating System | Windows 10 Education 64-bit                                                              |
