# DML
# Testing the YOLO object detection API

#clone this project
	git clone https://github.com/ImenBizid/DML.git


#define these variables
	INPUT_IMAGE=test_data/melissani.jpg
	OUTPUT_IMAGE=YOLO/test_data/result.jpg
	YOLO_demo=YOLO_demo
	DOCKER_IMAGE= darknet
	export variables_DOCKER_IMAGE_NAME=${DOCKER_IMAGE}
	export variables_DOCKER_CONTAINER_NAME=${YOLO_demo}
	export variables_INPUT_IMAGE=${INPUT_IMAGE}
	export variables_OUTPUT_IMAGE=${OUTPUT_IMAGE}

#Build your image using DML/YOLO/Dockerfile
	Docker build -t variables_DOCKER_IMAGE_NAME:1.0 .

#run a new container with mapping the container repository with your host repository
	Docker run -it -d --name variables_DOCKER_CONTAINER_NAME -v /YOLO/test_data:/root/darknet/test_data variables_DOCKER_IMAGE_NAME

#test the detection algorithm 
	Docker exec $variables_DOCKER_CONTAINER_NAME ./darknet detect cfg/yolo.cfg yolo.weights $variables_INPUT_IMAGE

#copie and paste the result in your host repository
	Docker cp $variables_DOCKER_CONTAINER_NAME:/root/darknet/predictions.png $variables_OUTPUT_IMAGE

#check now your output image to visualize the detection result
