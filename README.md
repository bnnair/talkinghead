Here are the steps to run the latest jupyter file for generate a talking head

1. SET UP THE ENVIRONMENT ON COLAB
	A. SHOW GPU INFO: 
	
		 i. !nvidia-smi --query-gpu=name,memory.total,memory.free --format=csv,noheader
	        ii. !pwd
	       iii. !ls
	
	B. CHECK THE TORCH:
	   Normally colab would have the latest torch. When i ran this i got version torch-2.5.1+cu124. But it was not compatible 
	   many other dependent libraries. so i uninstalled it and downgraded it.
	   
	   i. !pip uninstall torch $(pip list | grep nvidia- | cut -d' ' -f1 | xargs)
	   ii.!pip install torch --index-url https://download.pytorch.org/whl/cu117
	   
	   ## The torchvision and torchaudio version required was also not compatible , and since torch was downgraded,
           ## they also need to be downgraded.
	   
	   iii. !pip install torchvision==0.15.2 torchaudio==2.0.2
	   
	   ## Now you should have torch-2.0.1+cu117 installed.
	
	C: INSTALL PACKAGES:
	
		i. !pip install tensorrt==8.6.1 librosa tqdm filetype imageio opencv_python_headless scikit-image cython cuda-python imageio-ffmpeg colored polygraphy numpy==1.26.4
			
		Here also we have to downgrade numpy as the numpy lib in torch should be same as the numpy installed.
		
3. UPDATE ONE PYTHON CODE file
	
	A. In the package core ---> Auxillary models ---> mediapipe_landmark478.py file
		
			change the line from :
				angle = -np.atan2(y0 - y1, x1 - x0)
			to 
				angle = -np.arctan2(y0 - y1, x1 - x0)
			
	The application should run without any issue. Thanks!
	
	   
