SIM-RTL:
	iverilog EF_QSPI_XIP_CTRL_ahbl_tb.v ../../hdl/rtl/EF_QSPI_XIP_CTRL.v ../../hdl/rtl/DMC.v ../../hdl/rtl/bus_wrappers/EF_QSPI_XIP_CTRL_ahbl.v ../vip/sst26wf080b.v
	./a.out

SIM-GL:
	iverilog -s EF_QSPI_XIP_CACHE_ahbl_tb EF_QSPI_XIP_CACHE_ahbl_tb.v ../vip/sst26wf080b.v ../../hdl/gl/sky130/EF_QSPI_XIP_CACHE_ahbl.v ../../util/tech/sky130/sky130_hd.v
	./a.out

