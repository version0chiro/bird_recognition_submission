# bird_recognition_submission
This is the submission repository for Adaptive Computing Developer Contest hosted by Xilinx 
These are the set of commands used in all three devices:
•	Windows
o	Jupyter notebook and python 3.6 was used to train models from scratch using keras framework with tensorflow backend (CUDA enabled)
o	The model generated can be found in the model folder of this repository
o	SSH was done to the linux machine running ubuntu to execute git related commands
•	Linux(Ubuntu)
o	The vitis-ai-tutorials was cloned from the following git repository to convert keras model into elf models. https://github.com/Xilinx/Vitis-AI-Tutorials.git
o	Commands run inside the repository:
	./docker_run.sh xilinx/vitis-ai:latest (to start the docker)
	source ./0_setenv.sh (initializing many of the parameters for the specific model)
	source ./2_keras2tf.sh (starting the keras to tensorflow conversion)
	source ./4_quant.sh (quantization of the images placed inside the calib_images folder)
•	A custom datagen.py script was written to convert the calib_images into proper format for the model input shape 
	source ./6_compile.sh ( compiling the model with path to the dcf and arch json file inside the DOUCZDX8G path)
o	The above command must have generated an elf file if executed properly.
•	Ultra96V2 (Petalinux)
o	The DPU runner was used to utilise the built elf model. Threads were used for the static version and no threads were utilised for the live feed version
o	The target board being Ultra96V2 obtained the code via git function. The original git version of the model can be found in this repo with all the commits: https://github.com/version0chiro/Xillinx_ULTRA96_BIRDS
o	There are two version of the code present in the git repo, one running on static images while the other working on live feed taking input frames directly from the Logitech webcam attached to the usb port of ultra96.  
	Running the static code: python3 recognize_birds.py -i {path to the image directory}
•	The code was executed in a batch format
	Running the live feed version : python3 bird_recognition_live_feed.py.py

These are the references that were used in this project:
•	The petalinux image pre-built was obtained from Mario Bergeron’s project https://www.hackster.io/AlbertaBeef/vitis-ai-1-2-flow-for-avnet-vitis-platforms-7cb3aa
•	The code for converting keras model into elf was referred from vitis-ai-tutorials: https://github.com/Xilinx/Vitis-AI-Tutorials.git
•	The dataset was a mixture of these two Kaggle dataset: 
o	https://www.kaggle.com/gpiosenka/100-bird-species?select=train
o	https://www.kaggle.com/dmcgow/birds-200
