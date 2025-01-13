SIM-RTL:
	iverilog EF_QSPI_XIP_CTRL_AHBL_tb.v ../../hdl/rtl/EF_QSPI_XIP_CTRL.v ../../hdl/rtl/DMC.v ../../hdl/rtl/bus_wrappers/EF_QSPI_XIP_CTRL_AHBL.v ../vip/sst26wf080b.v
	./a.out

SIM-GL:
	iverilog -s EF_QSPI_XIP_CACHE_AHBL_tb EF_QSPI_XIP_CACHE_AHBL_tb.v ../vip/sst26wf080b.v ../../hdl/gl/sky130/EF_QSPI_XIP_CACHE_AHBL.v ../../util/tech/sky130/sky130_hd.v
	./a.out

