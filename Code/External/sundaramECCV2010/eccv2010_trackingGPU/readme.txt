This code is for scientific use only. Any commercial use is 
prohibited.
________________________________________________________________

Point tracking binary for 64 bit Linux (GPU version)

Requires CUDA 5.0 
________________________________________________________________

(c) Narayanan Sundaram, Thomas Brox 2011

If you use this program, you should cite the following paper:

N. Sundaram, T. Brox, K. Keutzer. Dense point trajectories by 
GPU-accelerated large displacement optical flow, European 
Conference on Computer Vision (ECCV), 2010.

---------------

Usage: 

Compile the package using make. You must have a CUDA capable 
GPU in your system and must have installed the CUDA toolkit. 
Add the paths to the CUDA libraries to the LD_LIBRARY_PATH 
environment variable via
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<path_to_cuda_library>

After that you can run the program via

./tracking bmfFile startFrame numberOfFrames sampling

bmfFile is a text file with a very short header, comprising the 
number of images in the sequence and 1. After the header all 
image files of the sequences are listed separated by line breaks. 
See cars1.bmf for an example. All input files must be in the 
PPM format (P6). 

startFrame is the frame where the computation is started. 
Usually this is frame 0. If you want to start later in the 
sequence you may specify another value.

numberOfFrames is the number of frames for which you want to 
run the tracker. Make sure that the value is not larger than 
the total number of frames of your sequence.

sampling specifies the subsampling parameter. If you specify 8, 
only every 8th pixel in x and y direction is taken into account. 
If you specify 1, the sampling will be dense. Since the tracker 
is based on dense optical flow, the choice of this parameter 
has little effect on the computation speed, but the size of the
trajectory file can become huge in case of dense trajectories. 

Known problems:

If the images get too large, the code can crash. Either downsample
your images or use the CPU version of the code. 1200x800 images
should be about the theoretical limit. 

There has been some change in how texture memory is handled between 
cuda versions. This can cause "Cuda error in file 'Filters.cu' 
in line 496 : invalid device symbol". If this error occurs, make
sure that you use the cuda drivers and toolkit for version 5.0.

__________________________________________________________________

Bugs
__________________________________________________________________

Please report bugs to narayans@eecs.berkeley.edu with CC to 
brox@informatik.uni-freiburg.de

