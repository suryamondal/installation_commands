# installation commands
this readme contains some commands to install various software



pythia8:
tar -zxvf pythia8235.tgz
pythia8235-source
mv pythia8235 pythia8235-source
cd pythia8235-source
mv pythia8235/* .
rm -rf pythia8235
./configure --enable-shared -fPIC --prefix=/home/surya/products/pythia8235/
make
make install


pythia6:
tar -zxvf pythia6.tar.gz
gunzip -k pythia-6.4.28.f.gz
mv pythia6 pythia6428/
rm pythia6428/pythia6428.f
mv pythia-6.4.28.f pythia6428/pythia6428.f
cd pythia6428/
./makePythia6.linuxx8664
rm *.o


Root Dependencies:
```
sudo apt-get install dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev python libssl-dev gfortran libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev qtwebengine5-dev
```

CMake Root6.26.04: Less flags : worked
```
wget https://root.cern/download/root_v6.26.04.source.tar.gz
tar -zxvf root_v6.26.04.source.tar.gz
rm -rf root_v6.26.04
mv root-6.26.04 root_v6.26.04
mkdir root_v6.26.04-build
cd root_v6.26.04-build
#cmake -Dgdml=ON -Dpythia6=OFF -Dpythia8=OFF -DCMAKE_INSTALL_PREFIX=/home/surya/products/ROOT/root_v6.26.04/ /home/surya/products/ROOT/root_v6.26.04/
cmake -Dminimal=ON -Dgdml=ON -Dminuit2=ON -DCMAKE_INSTALL_PREFIX=/home/surya/products/ROOT/root_v6.26.04/ /home/surya/products/ROOT/root_v6.26.04/
make -j2
make install
cd ..
rm -rf root_v6.26.04-build
```
### "modules" error: Solved by editing some file: contact jim
### solved by adding adding "/modules/" before RootMacros.cmake



CMake Root6:
```
cmake -Dgdml=ON -Dbuiltin_gsl=ON -Dmathmore=ON -Dpythia6=ON -Dpythia8=ON -Droofit=ON -DGSL_DIR=/home/surya/products/gsl25/ -DGSL_CONFIG_EXECUTABLE=/home/surya/products/gsl25/bin/gsl-config -DPYTHIA6_LIBRARY=/home/surya/products/pythia6428/libPythia6.so -DPYTHIA8_DIR=/home/surya/products/pythia8235/ -DPYTHIA8_INCLUDE_DIR=/home/surya/products/pythia8235/include/ -DPYTHIA8_LIBRARY=/home/surya/products/pythia8235/lib/libpythia8.so -DCMAKE_INSTALL_PREFIX=/home/surya/products/root-6.14.00/ ../root-6.14.00/
```

CLHEP, GEANT prerequisites:
```
sudo apt-get install libxmu-dev libxi-dev libconfig++-dev qt5-default libpq-dev postgresql-12 postgresql-server-dev-all libxerces-c-dev
```

Geant4.10.07.p01, CHLEP 2.4.4.0

CMake CLHEP:
```
wget https://proj-clhep.web.cern.ch/proj-clhep/dist1/clhep-2.4.4.0.tgz
tar -zxvf clhep-2.4.4.0.tgz
rm -rf clhep_v2.4.4.0
mv 2.4.4.0/CLHEP/ clhep_v2.4.4.0
rm -rf 2.4.4.0
mkdir clhep-build
cd clhep-build
cmake -DCMAKE_INSTALL_PREFIX=/home/surya/products/CLHEP/clhep_v2.4.4.0/ /home/surya/products/CLHEP/clhep_v2.4.4.0/
make -j2
make install
cd ..
rm -rf clhep-build
```

CMake Geant4:
```
wget https://geant4-data.web.cern.ch/releases/geant4.10.07.p01.tar.gz
wget https://geant4-data.web.cern.ch/releases/patch_geant4.10.07.p01.tar.gz
wget https://geant4-data.web.cern.ch/datasets/G4NDL.4.6.tar.gz
wget https://geant4-data.web.cern.ch/datasets/G4EMLOW.7.13.tar.gz
wget https://geant4-data.web.cern.ch/datasets/G4RealSurface.2.2.tar.gz
wget https://geant4-data.web.cern.ch/datasets/G4TENDL.1.3.2.tar.gz

mkdir geant4_data
cd geant4_data
tar -zxvf ../G4TENDL.1.3.2.tar.gz 
tar -zxvf ../G4NDL.4.6.tar.gz 
tar -zxvf ../G4EMLOW.7.13.tar.gz 
tar -zxvf ../G4RealSurface.2.2.tar.gz 
cd ..

tar -zxvf geant4.10.07.p01.tar.gz
tar -zxvf patch_geant4.10.07.p01.tar.gz
cp -rp geant4.10.07/* geant4.10.07.p01/
rm -rf geant4.10.07
rm -rf geant_v4.10.07.p01
mv geant4.10.07.p01 geant_v4.10.07.p01
mkdir geant4-build
cd geant4-build
cmake -DCMAKE_INSTALL_PREFIX=/home/surya/products/GEANT4/geant_v4.10.07.p01/ -DGEANT4_USE_SYSTEM_CLHEP=ON -DCLHEP_ROOT_DIR=/home/surya/products/CLHEP/clhep_v2.4.4.0/ -DGEANT4_USE_GDML=ON -DGEANT4_USE_QT=ON -DGEANT4_USE_OPENGL_X11=ON -DGEANT4_USE_RAYTRACER_X11=ON -DGEANT4_INSTALL_DATA=ON -DGEANT4_INSTALL_DATADIR=/home/surya/products/GEANT4/geant4_data/ /home/surya/products/GEANT4/geant_v4.10.07.p01/
make -j2
make install
cd ..
rm -rf geant4-build
```

GEANT4 Example:
### Do this in any directory
```
cmake /home/surya/products/GEANT4/geant_v4.10.07.p01/share/Geant4-10.7.1/examples/basic/B1/
make -j2
```

### if GEANT4 environment is not sourced
### cmake -DGeant4_DIR=/home/surya/products/GEANT4/geant4.10.04.p02-install/share/Geant4-10.4.2/ /home/surya/products/GEANT4/geant_v4.10.07.p01/share/Geant4-10.7.1/examples/basic/B1/




GENIE:
./configure --prefix=/home/surya/products/GENIE/genie --disable-profiler --disable-validation-tools --disable-cernlib --enable-lhapdf6 --enable-flux-drivers --enable-geom-drivers --disable-doxygen --enable-test --enable-mueloss --enable-dylibversion --enable-t2k --enable-fnal --enable-atmo --enable-nucleon-decay --disable-masterclass --disable-debug --with-optimiz-level=O2 --with-pythia6-lib=/home/surya/products/pythia6428/libPythia6.so --with-lhapdf6-inc=/home/surya/products/LHAPDF/lhapdf621/include --with-lhapdf6-lib=/home/surya/products/LHAPDF/lhapdf621/lib --with-libxml2-inc=/home/surya/products/LIBXML2/libxml2/include/libxml2 --with-libxml2-lib=/home/surya/products/LIBXML2/libxml2/lib --with-log4cpp-inc=/home/surya/products/LOG4CPP/log4cpp/include --with-log4cpp-lib=/home/surya/products/LOG4CPP/log4cpp/lib

HepMC:
curl -O http://lcgapp.cern.ch/project/simu/HepMC/download/HepMC-2.06.09.tar.gz
cmake -DCMAKE_INSTALL_PREFIX=/home/surya/products/EVTGEN/external/HepMC /home/surya/products/EVTGEN/external/HepMC-2.06.09 -Dmomentum:STRING=GEV -Dlength:STRING=MM

PHOTOS:
curl -O http://photospp.web.cern.ch/photospp/resources/PHOTOS.3.61/PHOTOS.3.61.tar.gz
./configure --with-hepmc=/home/surya/products/EVTGEN/external/HepMC

TAUOLA:
curl -O http://tauolapp.web.cern.ch/tauolapp/resources/TAUOLA.1.1.6c/TAUOLA.1.1.6c.tar.gz
./configure --with-hepmc=/home/surya/products/EVTGEN/external/HepMC

EVTGEN:
git clone http://phab.hepforge.org/source/evtgen.git
./configure --hepmcdir=/home/surya/products/EVTGEN/external/HepMC --photosdir=/home/surya/products/EVTGEN/external/PHOTOS --pythiadir=/home/surya/products/pythia8235 --tauoladir=/home/surya/products/EVTGEN/external/TAUOLA

RooUnfold:
svn co https://svnsrv.desy.de/public/unfolding/RooUnfold/trunk RooUnfold
cd RooUnfold
make

```
### ROOT6.26.04
export ROOTSYS=/home/surya/products/ROOT/root_v6.26.04
export PATH=$ROOTSYS/bin:$PATH
export LD_LIBRARY_PATH=$ROOTSYS/lib/:$LD_LIBRARY_PATH

### CLHEP-2.4.4.0
export CLHEP_BASE_DIR=/home/surya/products/CLHEP/clhep_v2.4.4.0/
export PATH=$PATH:$CLHEP_BASE_DIR/bin
export LD_LIBRARY_PATH=$CLHEP_BASE_DIR/lib:$LD_LIBRARY_PATH

### GEANT4.10.07.p01
export G4INSTALL=/home/surya/products/GEANT4/geant_v4.10.07.p01/share/Geant4-10.7.1/geant4make
### export G4WORKDIR=/home/surya/G4WORK
export G4WORKDIR=./
source $G4INSTALL/geant4make.sh
source /home/surya/products/GEANT4/geant_v4.10.07.p01/bin/geant4.sh
```
