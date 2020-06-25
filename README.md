# limestack

##   First, "sudo apt update"  and enter your password, to lock in the sudo without password entry.
##   Then, copy and paste including the white space between hashtag breaks one at a time
##   Or, simply drag and drop the text to your terminal window, really quick and easy.

### need to find deb alternative.

sudo add-apt-repository -y ppa:bladerf/bladerf;
sudo add-apt-repository -y ppa:ettusresearch/uhd;
sudo add-apt-repository -y ppa:myriadrf/drivers;
sudo add-apt-repository -y ppa:myriadrf/gnuradio;
sudo apt install gdebi snapd software-properties-gtk -y;

software-properties-gtk


#########
###     After that, software updates window should open, go into it and Edit the 4 PPA's to Bionic instead of Disco
###     Because, well Ubuntu ie: Disco isn't in those yet, but the bionic version work fine in 19.04
###     Then, enable all the multiverse, etc, just beacuse.. let'suse all the sources, mmkay?
###     This won't work if doing this on ssh. a simple install of a light desktop and XRDP could help.
##########

echo "UBUNTU_STORE_ID=LimeNET" | sudo tee -a /etc/environment
echo "UBUNTU_STORE_ID=LimeSDR" | sudo tee -a /etc/environment
sudo service snapd restart
sudo apt-get update

########
########   "BOTH DEB/UBU"
########

sudo apt-get install autopoint -y; sudo apt-get install libboost-all-dev -y; sudo apt-get install libi2c-dev -y; sudo apt-get install libusb-1.0-0-dev -y; sudo apt-get install build-essential -y; sudo apt-get install git -y; sudo apt-get install cmake -y; sudo apt-get install g++ -y; sudo apt-get install libsqlite3-dev -y; sudo apt-get install libpython-dev -y; sudo apt-get install python-numpy -y; sudo apt-get install swig -y; sudo apt-get install python -y; sudo apt-get install python-pip -y; sudo apt-get install python3 -y; sudo apt-get install python-setuptools -y; sudo apt-get install python-distutils-extra -y; sudo apt-get install qt5* -y; sudo apt-get install pyqt5-dev -y; sudo apt-get install libqt5svg5-dev -y; sudo apt-get install libportaudio2 -y; sudo apt-get install portaudio19-dev -y; sudo apt-get install doxygen -y; sudo apt-get install libwxgtk3.0-dev -y; sudo apt-get install freeglut3-dev -y; sudo apt-get install libsndfile1-dev -y; sudo apt-get install sndfile-tools -y; sudo apt-get install sndfile-programs -y; sudo apt-get install libcap-dev -y; sudo apt-get install orc-0.4 -y; sudo apt-get install python-apt -y; sudo apt-get install libuhd* -y; sudo apt-get install uhd-host -y; sudo apt-get install libosmosdr-dev -y; sudo apt-get install soapysdr-module-all -y; sudo apt-get install octave -y; sudo apt install gnuradio -y; sudo apt install gnuradio-dev -y; sudo apt install gnuradio-doc -y; sudo apt install gr-air-modes -y; sudo apt install gr-fcdproplus -y; sudo apt install gr-fosphor -y; sudo apt install gr-gsm -y; sudo apt install gr-hpsdr -y; sudo apt install gr-iio -y; sudo apt install gr-osmosdr -y; sudo apt install libair-modes0 -y; sudo apt install libgnuradio-analog -y; sudo apt install libgnuradio-atsc -y; sudo apt install libgnuradio-audio -y; sudo apt install libgnuradio-blocks -y; sudo apt install libgnuradio-channels -y; sudo apt install libgnuradio-comedi -y; sudo apt install libgnuradio-digital -y; sudo apt install libgnuradio-dtv -y; sudo apt install libgnuradio-fcd -y; sudo apt install libgnuradio-fcdproplus -y; sudo apt install libgnuradio-fec -y; sudo apt install libgnuradio-fft -y; sudo apt install libgnuradio-filter -y; sudo apt install libgnuradio-fosphor -y; sudo apt install libgnuradio-hpsdr -y; sudo apt install libgnuradio-iio0 -y; sudo apt install libgnuradio-iqbalance -y; sudo apt install libgnuradio-noaa -y; sudo apt install libgnuradio-osmosdr -y; sudo apt install libgnuradio-pager -y; sudo apt install libgnuradio-pmt -y; sudo apt install libgnuradio-qtgui -y; sudo apt install libgnuradio-radar -y; sudo apt install libgnuradio-rds -y; sudo apt install libgnuradio-runtime -y; sudo apt install libgnuradio-trellis -y; sudo apt install libgnuradio-uhd -y; sudo apt install libgnuradio-video-sdl -y; sudo apt install libgnuradio-vocoder -y; sudo apt install libgnuradio-wavelet -y; sudo apt install libgnuradio-wxgui -y; sudo apt install libgnuradio-zeromq -y; sudo apt install wxwidgets* -y


#########

export LIME_INSTALL=/usr/local/;
export LIME_SRC=/usr/src/sdr/;
sudo mkdir -p $LIME_SRC;
cd $LIME_SRC;
sudo git clone https://github.com/myriadrf/LimeSuite.git;
sudo git clone https://github.com/pothosware/SoapySDR.git;
sudo git clone https://github.com/gnuradio/volk.git;
sudo git clone --recursive https://github.com/pothosware/PothosCore.git;
sudo git clone https://github.com/gnuradio/gnuradio.git;
sudo git clone https://github.com/osmocom/rtl-sdr.git;
sudo git clone https://git.osmocom.org/gr-osmosdr;
sudo git clone https://github.com/csete/gqrx.git;
sudo git clone https://github.com/orocos-toolchain/log4cpp.git;
sudo git clone https://github.com/pulseaudio/pulseaudio.git;

#########

#soapy 

cd $LIME_SRC/SoapySDR/;
sudo mkdir mybuild;
cd mybuild;
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL ..;
sudo make -j56;
sudo make install;
sudo ldconfig;

#########

cd $LIME_SRC/LimeSuite/;
sudo mkdir mybuild;
cd mybuild;
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL ..;
sudo make -j56;
sudo make install;
sudo ldconfig;
;

##########

sudo LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/LimeUtil;
sudo LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/SoapySDRUtil --probe;
sudo LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/SoapySDRUtil --make:"driver=lime,type=sdr";
sudo LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/LimeSuiteGUI;

##########

sudo pip install mako six;

#########

cd $LIME_SRC/volk;
sudo mkdir mybuild;
cd mybuild;
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL  ..
sudo make -j56;
sudo make install;
sudo ldconfig;

LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/volk_profile;
sudo ldconfig;

##########

cd $LIME_SRC/pulseaudio;
sudo ./bootstrap.sh;
sudo make -j56;
sudo make install;

##########

cd $LIME_SRC/PothosCore;
sudo mkdir mybuild;
cd mybuild;
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL  ..;
sudo make -j56;
sudo make install;
sudo ldconfig;

sudo LD_LIBRARY_PATH=$LIME_INSTALL/lib/ $LIME_INSTALL/bin/PothosFlow;
sudo ldconfig;

##########

cd $LIME_SRC/log4cpp;
sudo mkdir mybuild;
cd mybuild;
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL  ..;
sudo make -j56;
sudo make install;
sudo ldconfig;

##########
# just because gnuradio for the hell of it add pybombs

pip install PyBOMBS thrift;
pybombs recipes add gr-recipes git+https://github.com/gnuradio/gr-recipes.git;
pybombs recipes add gr-etcetera git+https://github.com/gnuradio/gr-etcetera.git;
pybombs prefix init $LIME_INSTALL;

#########
# Because Ubuntu let us do this the easy way

sudo apt install gnuradio -y;
sudo apt install gr-gsm -y;

##########

cd $LIME_SRC/rtl-sdr
sudo mkdir mybuild
cd mybuild
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL ..
sudo make -j56
sudo make install

##########

cd $LIME_SRC/gr-osmosdr
sudo mkdir mybuild
cd mybuild
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL ..
sudo make -j56
sudo make install

##########

cd $LIME_SRC/gqrx
sudo mkdir mybuild
cd mybuild
sudo cmake -DCMAKE_INSTALL_PREFIX=$LIME_INSTALL -DCMAKE_PREFIX_PATH=$LIME_INSTALL ..
sudo make -j56
sudo make install

##########

sudo apt install sdrangelove cubicsdr  soapysdr-tools -y;

##########
 
 
sudo SoapySDRUtil --make="driver=lime,type=sdr"


 



 
 ## DONE.. ish?   ---- MOVED TO TOP. REPEAT NOT NEEDED


 #core framework and toolkits (required)
sudo add-apt-repository -y ppa:pothosware/framework

#support libraries for pothos (required)
sudo add-apt-repository -y ppa:pothosware/support

#supplies soapysdr, and drivers (required)
sudo add-apt-repository -y ppa:myriadrf/drivers

sudo apt-get update

sudo apt-get install soapysdr-tools python-soapysdr python-numpy python3-soapysdr python3-numpy soapysdr-module-remote -y;
 
 
 

apt install libmirisdr-dev  libfreesrp-dev  libmirisdr-dev  libhackrf-dev  libairspy-dev    libfreesrp-dev  UHD*  gnuradio* -y
 

###################################################
