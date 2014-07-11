`pix_opencv` is a computer vision library for Puredata and Gem.
It's free and open-source and  it uses OpenCV.
It is based on work by Yves Degoyon and Lluis Gomez i Bigorda.

# 1. Prepare you machine
You need to have puredata and Gem installed on your system.
And you need to know where they are…

You also need a compiling toolchain, e.g. GCC on Linux/Mac or Microsoft Visual C++ on Windows.

# 2. Get the sources :

## 2.1 Get the latest release
You can download a source tarball here : https://github.com/avilleret/pix_opencv/releases.

## 2.2 Get the latest sources
The is a `pix_opencv` folder in the externals folder of the Puredata SVN repository.
This is the primary version of `pix_opencv` but as it is quite hard to maintain this version, I decided to fork it in Githud. Thus the latest sources are here : https://github.com/avilleret/pix_opencv
You can clone it : 

~~~~
git clone https://github.com/avilleret/pix_opencv
~~~~

or fork it, or even download a snapshot.

The SVN repository will be updated on each release.

# 3. Get opencv :
## Ubuntu/Linux
The easiest way to get it is to install it from the repository :
`sudo apt-get install libopencv-*`

## Mac OSX :
The easiest way is to get from some packaging repository like Macports, fink or homebrew.
with fink :

~~~~
sudo fink install opencv-dev
with macport :
sudo port install opencv
~~~~

## Windows : 
Download the binary release on opencv.org
You can follow the quickstart guide on opencv.org to setup environment variables.

# 4. Build the Sources :

## Ubuntu/Linux & MacOSX
Go to the fresh created folder, i.e. « pix_opencv ».
If you cloned the git repo, you first have to run `./autogen.sh`.
Then run those commands :

~~~~
cd pix_opencv
./configure
make
~~~~

If you see something like « can’t find m_pd.h », you need to tweak pd’s path with this command :
`configure --with-pd=/path/to/pd`
If you see something like « can’t find Base/GemPixObj.h », you need to tweak Gem’s path with this command :
`configure --with-gem=/path/to/gem`
You can combine options like :
`configure --with-pd=/path/to/pd --with-gem=/path/to/gem`
To see more option, run `configure --help`.

Then you can install the package in the `pd/extra` directory with `sudo make install`.

## Windows
You need Visual C++ (at least the free express edition) to build pix_opencv on Windows.
There is a solution in build/vs2010 folder.
It was made with Visual C++ Express 2010 and surely need some tweaks before producing any DLL.
You need to change the include and the library paths.
The include must contain the following :
  - puredata include (pd-extended) or src (vanilla) folder : path\to\pd\src or path\to\pd-extended\include
  - Gem include folder : path\to\Gem
  - OpenCV include path, wich is ususally $(OPENCV_DIR)\..\..\include if you setup OPENCV_DIR according to Windows quickstart guide on opencv.org.
  
# 5. Optional
## 5.1 Build the `FaceTracker` lib

From the `pix_opencv` directory :
~~~~
  git submodule init
  git submodule update
  cd FaceTrakcer
  make 
~~~~
Then re-run `./configure` and `make` to add `pix_opencv_facetracker`.

## 5.2 Add non-free features support
Some OpenCV feature are non-free, this mean the licence doesn't allow packaging for these.
Anyway, you can use them but you have to build OpenCV library yourself.
Refer to opencv website to learn how to build it.
Then you can re-run `./configure` and `make` to add non-free feature support.

Currently, only `pix_opencv_surf` is affected by this.

# 6. Packaging !! OBSOLETE !!
## 6.1 To make a Distribuable source tarbal :
  `make dist`
	
This archive is called "pix_opencv-VERSION".
This archive must contains all sources files and headers, the build mechanism, and all other files needed to build it.

## 6.2 To make a binary archive :
  `make libdir`

This archive is called "pix_opencv-VERSION-TARGET".
This archive must contains binary of VERSION for TARGET architecture.
  
# 7. Testing 
  Open the `pix_opencv-help.pd` patch.
  It shows an overview of all available externals.
  And this tests the creation of each external.