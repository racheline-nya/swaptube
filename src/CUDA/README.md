here's an old ubuntu workaround for getting CUDA to run properly on older devices

install ubuntu 20.04, apt update and upgrade, install gcc, g++
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh the file you just downloaded, accept the EULA, deselect the driver option and install
download the runfile at https://us.download.nvidia.com/XFree86/Linux-x86_64/535.230.02/NVIDIA-Linux-x86_64-535.230.02.run
try to sudo sh it, if you get errors telling you to disable existing drivers (probably nouveau) then do that and try again (the error might say it created a modprobe to disable the drivers, in which case you might just need to reboot and possibly go into recovery mode to try again). you might have to install more stuff, i don't remember, but it should always tell you what to install
then probably reboot, idk (i had to because i did it through recovery mode)
add the following two lines to ~/.bashrc:
export PATH="$PATH:/usr/local/cuda-11.8/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda-11.8/lib64"
restart your terminal

then just the swaptube instructions:
sudo apt install cmake libswscale-dev libavcodec-dev libavformat-dev libavdevice-dev libavutil-dev libavfilter-dev gnuplot librsvg2-dev libglib2.0-dev libcairo2-dev libpng-dev nlohmann-json3-dev git ninja-build libtinyxml2-dev libgtkmm-3.0-dev libgtksourceviewmm-3.0-dev liblzma-dev
git clone https://github.com/2swap/swaptube/
go into the swaptube directory
run go.sh with any valid parameters and say yes to installing MicroTeX

if you get errors, go into CMakeFiles.txt and edit the cmake_minimum_required line to match your cmake version. if you still get errors, you may need to edit the CMAKE_CUDA_STANDARD line to set it to 14 instead of 17, and/or you may need to remove the line adding the -fdiagnostics-color=always option.