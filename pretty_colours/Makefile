###############################################################################
#                                                                             #
# Copyright 2016 myStorm Copyright and related                                #
# rights are licensed under the Solderpad Hardware License, Version 0.51      #
# (the “License”); you may not use this file except in compliance with        #
# the License. You may obtain a copy of the License at                        #
# http://solderpad.org/licenses/SHL-0.51. Unless required by applicable       #
# law or agreed to in writing, software, hardware and materials               #
# distributed under this License is distributed on an “AS IS” BASIS,          #
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or             #
# implied. See the License for the specific language governing                #
# permissions and limitations under the License.                              #
#                                                                             #
###############################################################################

# Default name of serial adaptor if none is provided by the user
#SERIAL := /dev/cu.usbmodem1421 # For macOS (maybe)
SERIAL := /dev/ttyACM0 # The default for linux (usually)

chip.bin: chip.v count.v blackice.pcf
	yosys -q -p "synth_ice40 -blif chip.blif" chip.v count.v
	arachne-pnr -d 8k -P tq144:4k -p blackice.pcf chip.blif -o chip.txt
	icepack chip.txt chip.bin

.PHONY: upload
upload:
#	stty -f $(SERIAL) raw & cat chip.bin >$(SERIAL) # for macOS
		stty -F $(SERIAL) raw & cat chip.bin >$(SERIAL) # for linux

.PHONY: clean
clean:
	$(RM) -f chip.blif chip.txt chip.ex chip.bin
