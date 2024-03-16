# Makefile
# See https://docs.cocotb.org/en/stable/quickstart.html for more info

# defaults
SIM ?= icarus
TOPLEVEL_LANG ?= verilog
SRC_DIR = $(PWD)/../src
PROJECT_SOURCES = tt_um_joerdsonsilva_top.v $(PWD)/modem.v $(PWD)/bask.v $(PWD)/mult1.v $(PWD)/clk_rdg1.v $(PWD)/rdg1.v $(PWD)/ffd1.v $(PWD)/wave11.v $(PWD)/bfsk.v $(PWD)/clk_rdg2.v $(PWD)/clk_25MHz.v $(PWD)/wave12.v $(PWD)/wave22.v $(PWD)/rdg2.v $(PWD)/ffd2.v $(PWD)/freq_select.v $(PWD)/bpsk.v $(PWD)/clk_rdg3.v $(PWD)/rdg3.v $(PWD)/ffd3.v $(PWD)/wave13.v $(PWD)/wave23.v $(PWD)/control_0.v $(PWD)/demod_bask.v $(PWD)/demod_bfsk.v $(PWD)/wave122.v $(PWD)/mult2.v $(PWD)/integrator2.v $(PWD)/demod_bpsk.v $(PWD)/wave133.v $(PWD)/mult3.v $(PWD)/integrator3.v $(PWD)/control_1.v

ifneq ($(GATES),yes)

# RTL simulation:
SIM_BUILD				= sim_build/rtl
VERILOG_SOURCES += $(addprefix $(SRC_DIR)/,$(PROJECT_SOURCES))
COMPILE_ARGS 		+= -I$(SRC_DIR)

else

# Gate level simulation:
SIM_BUILD				= sim_build/gl
COMPILE_ARGS    += -DGL_TEST
COMPILE_ARGS    += -DFUNCTIONAL
COMPILE_ARGS    += -DUSE_POWER_PINS
COMPILE_ARGS    += -DSIM
COMPILE_ARGS    += -DUNIT_DELAY=\#1
VERILOG_SOURCES += $(PDK_ROOT)/sky130A/libs.ref/sky130_fd_sc_hd/verilog/primitives.v
VERILOG_SOURCES += $(PDK_ROOT)/sky130A/libs.ref/sky130_fd_sc_hd/verilog/sky130_fd_sc_hd.v

# this gets copied in by the GDS action workflow
VERILOG_SOURCES += $(PWD)/gate_level_netlist.v

endif

# Include the testbench sources:
VERILOG_SOURCES += $(PWD)/tb.v 
TOPLEVEL = tb

# MODULE is the basename of the Python test file
MODULE = test

# include cocotb's make rules to take care of the simulator setup
include $(shell cocotb-config --makefiles)/Makefile.sim
