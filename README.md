# BM3Ddenoising
This project is C++ implementation of the state-of-the-art BM3D (Block matching and 3D filtering) image denoising algorithm based on OpenCV library.  
 
##(1).	Project Configuration 

The project is implemented in Microsoft Visual C++ 2015 Express and OpenCV 2.2.0. 
After successfully installing VC2015 and OpenCV 2.2, the BCDenoising solution should set up the necessary including, lib directory and dependable lib files. 

For example, the OpenCV2.2 is installed in “C:\OpenCV2.2\.”. CMake generates a dynamic opencv solution with Visual C++ 2015 in “C:\OpenCV2.2\VS2015\”. All the setups are saved in current solution. Please change them to correct OpenCV directory. 

Go to folder “\BCDenoising\”. Open “BCDenoising.sln” with Visual C++ 2015 ( or other  VC++ versions)  and set it in the Release Mode. In the Solution Explorer window, right-click the BCDenoising and open the property pages.
1) In the “Configuration Properties->C/C++->General”, input “ C:\OpenCV2.2\include\opencv; C:\OpenCV2.2\VS2010\include” in the Additional Include Directories command.  
2) In the “Configuration Properties->Linker->General”, input “C:\OpenCV2.2\VS2010\lib” in the Additional Library Directories command.
3) In the “Configuration Properties->Linker->Input”, add “ opencv_ml220.lib;opencv_imgproc220.lib; opencv_core220.lib; opencv_highgui220.lib” in the Additional dependencies command. 

##(2).	Program execution

There are two ways to execute the program. Two input parameters are needed: image file name and Gaussian standard derivative variance value. 

1) In the Release Mode, press “Debugging” or F5 and an executable file is created. Place it in the folder “\executable\”, double click “run_house.bat” bat file to test it on house128.png (128x128) with sigma 20. Or “run_peppers.bat” on peppers.png (256x256) with sigma 25 and “run_lena.bat” on Lena512.png (512x512) with sigma 30. 
    
Testing other images can be modified in the *.bat file. It should be “BCDenoising.exe image file (*.png or *.jpg) sigma. 

2) In the Release Mode, go to “Configuration Properties->Debugging” and input “image file (*.png) sigma” in the Command Arguments command. For example, input “house128.png 20” and make sure image files are in the same folder as all the *.cpp and *.h files. Press “Debugging” or F5 to run the code. 

The program will display the PSNR (Peak Signal to Noise Ratio) of noisy image to original image, restore image in the 1st step and 2nd step together with the original input image in the pop-up window. When it finishes, the original image, noisy image and final denoised image are displayed in three windows. Press any key to exit the program. 

##(3). Test images and results

Test images are included in the folder “\executable\”. The results are listed below and compared to the results from reference paper with DFT transformation implementation.  The program was run in Windows XP with 2.20GHz and 2GB RAM. 

Image	house ( 128x128) 	  Peppers(256x256)	 Lena(512x512)
Sigma	20	  25 	 30
PSNR (noisy)	22.09	 20.16	18.57
PSNR (denoised)	31.19	 29.28	30.81
PSNR(noisy)-BM3D	22.11	 20.18	18.59
PSNR(denoised)-BM3D	31.34 	 29.80 *	31.29 *
Execution time	~ 1min	~ 3 min	~ 10min
* denotes obtaining from http://www.cs.tut.fi/~foi/3D-DFT/. 

##(4). Comments 

The results are comparable to the reference results with same parameters. It uses FFT (Fast Fourier Transformation) to do 2D or 3D transformation. In theory, BM3D algorithm could use other transformations, such as bior1.5 for the 2D hard thresholding step and DCT transformation for Wiener filtering step and 1D Harr for the separable 3D transform. It will not achieve tremendous improvement according to the results shown in http://www.cs.tut.fi/~foi/GCF-BM3D/index.html#ref_results. 

The codes could be further optimized since we use exhaustive full search in both two steps. If predictive search is performed, the running time will be reduced. However, it is still acceptable compared to BM3DDFT Matlab implementation. The default searching window and maximum number of similar blocks can be customized to accelerate the code speed. 

##(5).	References

[1] K. Dabov, A. Foi, V. Katkovnik, and K. Egiazarian, “Image denoising by sparse 3D transform-domain collaborative filtering,” IEEE Trans. Image Process., vol. 16, no. 8, pp. 2080-2095, August 2007. 
[2] OpenCV 2.2 Reference Manul from the installed OpenCV2.2. 
