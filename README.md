# CUDA Toolkit Installation
## An easy instruction to install cuda-toolkit and cuda-driver on Ubuntu 20.04/22.04

1. Pre-installation
	1-0. CUDA installation guide: `https://docs.nvidia.com/cuda/cuda-installation-guide-linux` <be>
	1-1. CUDA-Capable GPU list: `https://developer.nvidia.com/cuda-gpus` <be>
	1-2. Verify You Have a CUDA-Capable GPU: `lspci | grep -i nvidia` <be>
	1-3. Verify You Have a Supported Version of Linux: `uname -m && cat /etc/*release` <be>
	1-4. Verify the System Has gcc Installed: `gcc --version` <br> <br>

2. Install cuda-toolkit and cuda-driver <br>
	`https://developer.nvidia.com/cuda-downloads` <br>
	2-0. Linux/x86-64/22.04/deb(local) <br>
	2-1. Run all the commands under Best Installer section <br>
	2-2. Run one of the options under Driver Installer section: `sudo apt-get install -y cuda-drivers` <br>
	2-3. Reboot the system: `sudo reboot` <br> <br>

3. Post-installation <br>
	3-0. Check the cuda-toolkit installed version: `nvidia-smi` <br>
	3-1. Open .bashrc: `nano ~/.bashrc` <br>
	3-2. Add the following lines to .bashrc (make sure to change the cuda version-here 12-2): <br>
		`export PATH=/usr/local/cuda-12.2/bin${PATH:+:${PATH}}` <br>
		`export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}` <br>
	3-3. Re-open the terminal and check the cuda-toolkit: `nvcc --version` <br>
	3-4. You can test whether it works correctly by creating a file with `'.cu'` extention containing the following code and run it (`nvcc -o cuda-test cuda-test.cu`): <br> <br>

 ```
#include <cuda_runtime.h>
#include <device_launch_parameters.h>
#include <stdio.h>

#define CUDA_CHECK_ERROR(err) \
    do { \
        if (err != cudaSuccess) { \
            fprintf(stderr, "CUDA error: %s, line %d\n", cudaGetErrorString(err), __LINE__); \
            exit(EXIT_FAILURE); \
        } \
    } while (0)

__global__ void hello_cuda()
{
    printf("Hello CUDA!\n");
}

int main()
{
    dim3 grid(2);
    dim3 block(3);
    
    hello_cuda<<<grid, block>>>();
    
    cudaError_t cuda_err = cudaDeviceSynchronize();
    CUDA_CHECK_ERROR(cuda_err);
    
    cuda_err = cudaDeviceReset();
    CUDA_CHECK_ERROR(cuda_err);

    return 0;
}
```
