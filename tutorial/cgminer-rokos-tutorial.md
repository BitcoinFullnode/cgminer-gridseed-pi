# CGGMiner 372 ROKOS with GridSeed GC3355 support

## Installing Required Libraries

sudo apt-get install libcurl4-gnutls-dev libusb-1.0 udev libudev-dev libncurses-dev

## Compiling cgminer for gridseed miners

git clone https://github.com/BitcoinFullnode/cgminer-gridseed-rokos372

cd cgminer-gridseed-rokos372

./configure --enable-scrypt --enable-gridseed

make -j4

## Find attached usb gridseed miner port numbers

lsusb | grep "STM" | cut -c5-7,15-18,20-32

## Running (replace $1 $2 with corresponding USB port numbers)

sudo ./cgminer --gridseed-options=baud=115200,freq=825,chips=5,modules=1,usefifo=0,btc=0 --hotplug=0 -o stratum+tcp://scrypt.mine.zpool.ca:3433 -u 1MDwAu8dY3t3kZv3AbEN2dJiN8ibg6y9Kp -p CGMINER --usb=$1:$2 --scrypt

GC3355-specific options can be specified via --gridseed-options or
"gridseed-options" in the configuration file as a comma-separated list of
sub-options:

* baud - miner baud rate (default 115200)
* freq - a choice of 250/400/450/500/550/600/650/700/750/800/850/900/950/1000
* pll_r, pll_f, pll_od - fine-grained frequency tuning; see below
* chips - number of chips per device (default 5)
* per_chip_stats - print per-chip nonce generations and hardware failures

If pll_r/pll_f/pll_od are specified, freq is ignored, and calculated as follows:
* Fin = 25
* Fref = int(Fin / (pll_r + 1))
* Fvco = int(Fref * (pll_f + 1))
* Fout = int(Fvco / (1 << pll_od))
* freq = Fout

This version of cgminer turns off all BTC cores so that power usage is low.
On a 5-chip USB miner, power usage is around 10 W. GPUs are also supported.
