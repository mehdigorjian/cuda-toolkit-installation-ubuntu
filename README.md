# CUDA Toolkit Installation
## An easy instruction to install cuda-toolkit and cuda driver on Ubuntu 20.04/22.04

1. Pre-installation
	1-0. CUDA installation guide: `https://docs.nvidia.com/cuda/cuda-installation-guide-linux`
	1-1. CUDA-Capable GPU list: `https://developer.nvidia.com/cuda-gpus`
	1-2. Verify You Have a CUDA-Capable GPU: `lspci | grep -i nvidia`
	1-3. Verify You Have a Supported Version of Linux: `uname -m && cat /etc/*release`
	1-4. Verify the System Has gcc Installed: `gcc --version`

2. Install cuda-toolkit and cuda-driver
	`https://developer.nvidia.com/cuda-downloads`
	2-0. Linux/x86-64/22.04/deb(local)
	2-1. Run all the commands under Best Installer section
	2-2. Run one of the options under Driver Installer section: `sudo apt-get install -y cuda-drivers`
	2-3. Reboot the system: `sudo reboot`

3. Post-installation
	3-0. Check the cuda-toolkit installed version: `nvidia-smi`
	3-1. Open .bashrc: `nano ~/.bashrc`
	3-2. Add the following lines to .bashrc (make sure to change the cuda version-here 12-2):
		`export PATH=/usr/local/cuda-12.2/bin${PATH:+:${PATH}}` \
		`export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`
	3-3. Re-open the terminal and check the cuda-toolkit: `nvcc --version`
	3-4. You can test whether it works correctly by creating a file with `'.cu'` extention containing the following code and run it (`nvcc -o cuda-test cuda-test.cu`):
