PROJ=morse

all: ${PROJ}.bit

%.json: %.v
	yosys -p "synth_ecp5 -json $@" $<

%_out.config: %.json
	nextpnr-ecp5 --json $< --textcfg $@ --um5g-85k --package CSFBGA285 --lpf morse.lpf

%.bit: %_out.config
	ecppack $< $@

prog: ${PROJ}.bit
	tinyprog -p $<

clean:
	rm -f *.bit *.svf *_out.config *.json

.PHONY: clean
.PRECIOUS: ${PROJ}.json ${PROJ}_out.config
