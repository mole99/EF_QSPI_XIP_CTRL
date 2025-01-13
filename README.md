# EF_QSPI_XIP_CTRL

A QSPI XiP Flash COntroller with a parameterized Direct-Mapped Cache.
## The wrapped IP


 The IP comes with an AHBL Wrapper

#### Wrapped IP System Integration

```verilog
EF_QSPI_XIP_CTRL_APB INST (
	`TB_AHBL_SLAVE_CONN,
	.sck(sck)
	.ce_n(ce_n)
	.dout(dout)
	.din(din)
	.douten(douten)
);
```
> **_NOTE:_** `TB_APB_SLAVE_CONN is a convenient macro provided by [BusWrap](https://github.com/efabless/BusWrap/tree/main).
#### Wrappers with DFT support
Wrappers in the directory ``/hdl/rtl/bus_wrappers/DFT`` have an extra input port ``sc_testmode`` to disable the clock gate whenever the scan chain testmode is enabled.

## Implementation example  

The following table is the result for implementing the EF_QSPI_XIP_CTRL IP with different wrappers using Sky130 PDK and [OpenLane2](https://github.com/efabless/openlane2) flow.
|Module | Number of cells | Max. freq |
|---|---|---|
|EF_QSPI_XIP_CTRL|1973| 250 |
|EF_QSPI_XIP_CTRL_AHBL|1973|250|
## The Programmer's Interface


### Registers

|Name|Offset|Reset Value|Access Mode|Description|
|---|---|---|---|---|

### Clock Gating
The IP includes a clock gating feature that allows selective activation and deactivation of the clock using the ``GCLK`` register. This capability is implemented through the ``ef_util_gating_cell`` module, which is part of the common modules library, [ef_util_lib.v](https://github.com/efabless/EF_IP_UTIL/blob/main/hdl/ef_util_lib.v). By default, the clock gating is disabled. To enable behavioral implmentation clock gating, only for simulation purposes, you should define the ``CLKG_GENERIC`` macro. Alternatively, define the ``CLKG_SKY130_HD`` macro if you wish to use the SKY130 HD library clock gating cell, ``sky130_fd_sc_hd__dlclkp_4``.

**Note:** If you choose the [OpenLane2](https://github.com/efabless/openlane2) flow for implementation and would like to enable the clock gating feature, you need to add ``CLKG_SKY130_HD`` macro to the ``VERILOG_DEFINES`` configuration variable. Update OpenLane2 YAML configuration file as follows: 
```
VERILOG_DEFINES:
- CLKG_SKY130_HD
```

### The Interface 

<img src="docs/_static/EF_QSPI_XIP_CTRL.svg" width="600"/>

#### Module Parameters 

|Parameter|Description|Default Value|
|---|---|---|
|NUM_LINES|The cache number of lines.|16|
|LINE_SIZE|The cache line size in bytes.|32|
|RESET_CYCLES|The number of cycles needed for the s/w reset command; reset time = (RESET_CYCLES + 1) * 2 /(HCLK frequency).|999|

#### Ports 

|Port|Direction|Width|Description|
|---|---|---|---|
|sck|output|1|SPI serial clock|
|ce_n|output|1|SPI chip select (Active Low).|
|dout|output|4|Flash controller SPI data out.|
|din|input|4|Flash controller SPI data in.|
|douten|output|4|Flash controller data out enable (Active Low)|
## Firmware Drivers:
Firmware drivers for EF_QSPI_XIP_CTRL can be found in the [fw](https://github.com/efabless/EF_QSPI_XIP_CTRL/tree/main/fw) directory. EF_QSPI_XIP_CTRL driver documentation  is available [here](https://github.com/efabless/EF_QSPI_XIP_CTRL/blob/main/fw/README.md).
You can also find an example C application using the EF_QSPI_XIP_CTRL drivers [here]().
## Installation:
You can install the IP either by cloning this repository or by using [IPM](https://github.com/efabless/IPM).
##### 1. Using [IPM](https://github.com/efabless/IPM):
- [Optional] If you do not have IPM installed, follow the installation guide [here](https://github.com/efabless/IPM/blob/main/README.md)
- After installing IPM, execute the following command ```ipm install EF_QSPI_XIP_CTRL```.
> **Note:** This method is recommended as it automatically installs [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) as a dependency.
##### 2. Cloning this repo: 
- Clone [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) repository, which includes the required modules from the common modules library, [ef_util_lib.v](https://github.com/efabless/EF_IP_UTIL/blob/main/hdl/ef_util_lib.v).
```git clone https://github.com/efabless/EF_IP_UTIL.git```
- Clone the IP repository
```git clone github.com/efabless/EF_QSPI_XIP_CTRL```
