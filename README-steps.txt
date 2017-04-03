Compiling cgminer for gridseed miners:
sudo apt-get install libcurl4-gnutls-dev libusb-1.0 udev libudev-dev libncurses-dev
./configure --enable-scrypt --enable-gridseed
make -j4

Find attached usb gridseed miner port numbers:
lsusb | grep "STM" | cut -c5-7,15-18,20-32

Running (replace $1 $2 with corresponding USB port numbers):
sudo ./cgminer --gridseed-options=baud=115200,freq=825,chips=5,modules=1,usefifo=0,btc=0 --hotplug=0 -o stratum+tcp://scrypt.mine.zpool.ca:3433 -u 1MDwAu8dY3t3kZv3AbEN2dJiN8ibg6y9Kp -p CGMINER --usb=$1:$2 --scrypt
