# Png-to-from-Verilog
Python3 scripts to convert Png images to Verilog and MIF files (and the other way around)

[**Png2ROM.py**](https://github.com/abbati-simone/Png-to-from-Verilog/blob/master/src/Png2ROM.py) create a Verilog or MIF file (Memory initialization file) from a PNG image without alpha channel (and 8 bit per color).
[**ROM2Png.py**](https://github.com/abbati-simone/Png-to-from-Verilog/blob/master/src/ROM2Png.py) create a PNG image (without alpha) from Verilog file (starting from MIF file is not implemented).

Both scripts needs Python3 *png* and *getopt* packages.

[**run_conversion.sh**](https://github.com/abbati-simone/Png-to-from-Verilog/blob/master/src/run_conversion.sh) is a shell script with many examples for included images

Png2ROM.py example
------------------
Create a MIF file from blocks_rom.png with 4 bit red, 4 bit green, 4 bit blue
```bash
$./src/Png2ROM.py -i doc/png/blocks_rom.png -o doc/mif/blocks_rom.mif -f quartus -b 444
```
Output *blocks_rom.mif* (partial preview):
```
WIDTH = 12;
DEPTH = 2048;
ADDRESS_RADIX = HEX;
DATA_RADIX = BIN;
CONTENT BEGIN
0: 011011011110;
1: 000000000000;
2: 000000000000;
3: 000000000000;
4: 000000000000;
5: 000000000000;
6: 000000000000;
7: 000000000000;
8: 000000000000;
9: 000000000000;
a: 000000000000;
b: 000000000000;
c: 000000000000;
d: 000000000000;
e: 000000000000;
f: 011011011110;
10: 000000000000;
11: 000000000000;
...............
```

Create a Verilog (the *case* portion) file from blocks_rom.png with 4 bit red, 4 bit green, 4 bit blue
```bash
$./src/Png2ROM.py -i doc/png/blocks_rom.png -o doc/verilog/blocks_rom.v -f verilog -b 444
```
Output *blocks_rom.v* (partial preview):
```
//.....
11'b00000000000: color_data = 12'b011011011110;
11'b00000000001: color_data = 12'b000000000000;
11'b00000000010: color_data = 12'b000000000000;
11'b00000000011: color_data = 12'b000000000000;
11'b00000000100: color_data = 12'b000000000000;
11'b00000000101: color_data = 12'b000000000000;
11'b00000000110: color_data = 12'b000000000000;
11'b00000000111: color_data = 12'b000000000000;
11'b00000001000: color_data = 12'b000000000000;
11'b00000001001: color_data = 12'b000000000000;
11'b00000001010: color_data = 12'b000000000000;
11'b00000001011: color_data = 12'b000000000000;
11'b00000001100: color_data = 12'b000000000000;
11'b00000001101: color_data = 12'b000000000000;
11'b00000001110: color_data = 12'b000000000000;
11'b00000001111: color_data = 12'b011011011110;
11'b00000010000: color_data = 12'b000000000000;
11'b00000010001: color_data = 12'b000000000000;
...............
//.....
```

ROM2Png.py example
------------------
Create a PNG file from Verilog file (containing only the *case* portion) with 4 bit red, 4 bit green, 4 bit blue, 16 pixel width, 80 pixel height (without alpha)
```bash
$./src/ROM2Png.py -i doc/verilog/blocks_rom.v -o doc/png/blocks_rom.png -f verilog -b 444 -x 16 -y 80
```
Output *blocks_rom.png*:
![Extracted image from Verilog file](https://github.com/abbati-simone/Png-to-from-Verilog/blob/master/doc/png/blocks_rom.png "Extracted image from Verilog file")

These scripts have been used on this project https://github.com/abbati-simone/Yoshis-Nightmare-Altera


