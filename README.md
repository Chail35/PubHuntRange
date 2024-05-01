# PubHunt
_Hunt for Bitcoin public keys._

## It searches random compressed public keys for given hash160.

#
# The idea to do this

This is only useful for Bitcoin [puzzle transaction](https://www.blockchain.com/btc/tx/08389f34c98c606322740c0be6a7125d9860bb8d5cb182c02f98461e5fa6cd15).

Modified to Search for the public key within a given range.

For the puzzles, ```66```, ```67```, ```68```, ```69```, ```71``` or ```72``` and some more, there are no public keys are available, so if we can able to find public keys for those addresses, then [Pollard Kangaroo](https://github.com/JeanLucPons/Kangaroo) algorithm can be used to solve those puzzles.

That's it, cheers 🍺 

# Usage

This is GPU only, no CPU support. 

```
./PubHunt -h
PubHunt [-check] [-h] [-v]
        [-gi GPU ids: 0,1...] [-gx gridsize: g0x,g0y,g1x,g1y, ...]
        [-o outputfile] [-sr startRange] [-er endRange] [inputFile]

 -v                       : Print version
 -gi gpuId1,gpuId2,...    : List of GPU(s) to use, default is 0
 -gx g1x,g1y,g2x,g2y, ... : Specify GPU(s) kernel gridsize, default is 8*(MP number),128
 -o outputfile            : Output results to the specified file
 -sr startRange           : Start of the key range to search
 -er endRange             : End of the key range to search
 -l                       : List cuda enabled devices
 -check                   : Check Int calculations
 inputFile                : List of the hash160, one per line in hex format (text mode)
```

For example:
```
./PubHunt -sr 2000000000000000 -er 3fffffffffffffff -o KeyFound.txt -gi 0 -gx 8192,1024 hash160.txt

PubHunt v1.00

DEVICE       : GPU
GPU IDS      : 0
GPU GRIDSIZE : 8192x1024
NUM HASH160  : 1
OUTPUT FILE  : KeyFound.txt
KEY RANGE    : 0x2000000000000000 - 0x3fffffffffffffff
GPU          : GPU #0 NVIDIA GeForce RTX 4070 (46x0 cores) Grid(8192x1024)

[00:00:14] [GPU: 2681.56 MH/s] [T: 37,547,409,408 (36 bit)] [F: 0]
```

## Building
##### Windows
- Microsoft Visual Studio Community 2019 
- CUDA version 10.0
##### Linux
 - Edit the makefile and set up the appropriate CUDA SDK and compiler paths for nvcc. Or pass them as variables to `make` command.

    ```make
    CUDA       = /usr/local/cuda
    CXXCUDA    = /usr/bin/g++
    ```
 - To build with CUDA: pass CCAP value according to your GPU compute capability
    ```sh
    $ make CCAP=89 all
    ```

## License
PubHunt is licensed under GPLv3.

## Disclaimer
ALL THE CODES, PROGRAM AND INFORMATION ARE FOR EDUCATIONAL PURPOSES ONLY. USE IT AT YOUR OWN RISK. THE DEVELOPER WILL NOT BE RESPONSIBLE FOR ANY LOSS, DAMAGE OR CLAIM ARISING FROM USING THIS PROGRAM.
