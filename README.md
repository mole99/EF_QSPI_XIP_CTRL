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
Wrappers in the directory ``/hdl/rtl/bus_wrappers/DFT`` have an extra input port ``sc_testmode`` to enable the clock gate whenever the scan chain testmode is enabled.

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
The IP has clock gating feature, enabling the selective activation and deactivation of the clock as required through the ``GCLK`` register. This functionality is implemented through the ``ef_util_gating_cell``, which is part of the the common modules library, [ef_util_lib.v](https://github.com/efabless/EF_IP_UTIL/blob/main/hdl/ef_util_lib.v). By default, the cell operates with a behavioral implementation, but when the ``CLKG_SKY130_HD`` macro is enabled, the ``sky130_fd_sc_hd__dlclkp_4`` clock gating cell is used.
**Note:** If you choose the [OpenLane2](https://github.com/efabless/openlane2) flow for implementation and would like to add the clock gating feature, you need to add ``SKY130`` macro to the ``VERILOG_DEFINES`` configuration variable. Update the YAML configuration file as follows: 
```
VERILOG_DEFINES:
- SKY130
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
You can either clone repo or use [IPM](https://github.com/efabless/IPM) which is an open-source IPs Package Manager
* To clone repo:
```git clone https://github.com/efabless/EF_QSPI_XIP_CTRL```
> **Note:** If you choose this method, you need to clone [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) repository, as it includes required modules from the common modules library, [ef_util_lib.v](https://github.com/efabless/EF_IP_UTIL/blob/main/hdl/ef_util_lib.v)
* To download via IPM , follow installation guides [here](https://github.com/efabless/IPM/blob/main/README.md) then run 
```ipm install EF_QSPI_XIP_CTRL```
> **Note:** This method is recommended as it automatically installs [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) as a dependency.
