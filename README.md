# EF_QSPI_XIP_CTRL
Quad I/O SPI Flash memory controller with support for:
- AHB lite interface
- Execute in Place (XiP)
- Nx16 Direct-Mapped Cache (default: N=32).

Intended to be used with SoCs that have no on-chip flash memory. 


## Performance
The following data is obtained using Sky130 HD library
| Configuration | # of Cells (K) | Delay (ns) | I<sub>dyn</sub> (mA/MHz) | I<sub>s</sub> (nA) | 
|---------------|----------------|------------|--------------------------|--------------------|
| 16x16 | 7.2 | 12 | 0.0625 | 20 |
| 32x16 | 14.3 | 17  | 0.126 | 39.5 |


AHB-Lite Quad I/O SPI Flash memory controller with direct mapped cache and support for XiP.
## The wrapped IP


 The IP comes with an AHBL Wrapper

### Wrapped IP System Integration

```verilog
EF_QSPI_XIP_CTRL_AHBL INST (
        .HCLK(CLK), 
        .HRESETn(RESETn), 
        .HADDR(HADDR), 
        .HWRITE(HWRITE), 
        .HSEL(HSEL), 
        .HTRANS(HTRANS), 
        .HWDATA(HWDATA),
        .HRDATA(HRDATA), 
        .HREADY(HREADY),
        .HREADYOUT(HREADYOUT),
        .sck(sck),
        .ce_n(ce_n),
        .din(din),
        .dout(dout),
        .douten(douten)
);
```

## Implementation example  

The following table is the result for implementing the EF_QSPI_XIP_CTRL IP with different wrappers using Sky130 PDK and [OpenLane2](https://github.com/efabless/openlane2) flow.
|Module | Number of cells | Max. freq |
|---|---|---|
|EF_QSPI_XIP_CTRL|534| 384 MHz |
|EF_QSPI_XIP_CTRL_AHBL|13024|40 MHz|

### The Interface 
<img src="docs/EF_QSPI_XIP_CTRL.svg" width="600"/>

#### Ports 

|Port|Direction|Width|Description|
|---|---|---|---|
|sck|output|1|spi serial clock|
|ce_n|output|1|slave select signal|
|din|input|4|spi data in|
|dout|output|4|spi data out|
|douten|output|4|spi data out enable|

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
```git clone https://github.com/efabless/EF_QSPI_XIP_CTRL.git```

## Todo:
 - [ ] support for WB bus
 - [ ] Support cache configurations other than 16 bytes per line
