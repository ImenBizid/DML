# DML
# Testing the YOLO object detection API

Clone this project

    git clone https://github.com/ImenBizid/DML.git


Define these variables

    INPUT_IMAGE=test_data/melissani.jpg
    OUTPUT_IMAGE=test_data/result.jpg
    YOLO_demo=YOLO_demo
    DOCKER_IMAGE=darknet:1.0
    export variables_DOCKER_IMAGE_NAME=${DOCKER_IMAGE}
    export variables_DOCKER_CONTAINER_NAME=${YOLO_demo}
    export variables_INPUT_IMAGE=${INPUT_IMAGE}
    export variables_OUTPUT_IMAGE=${OUTPUT_IMAGE}

Build your image FROM DML/YOLO

    Docker build -t $variables_DOCKER_IMAGE_NAME .

Run a new container with mapping the container repository with your host repository
the folder test_data must be a shared directory with docker (You can add it Docker -> Preferences -> File Sharing ..)

    Docker run -it -d --name $variables_DOCKER_CONTAINER_NAME -v test_data:/root/darknet/test_data $variables_DOCKER_IMAGE_NAME

Test the detection algorithm 

    Docker exec $variables_DOCKER_CONTAINER_NAME ./darknet detect cfg/yolo.cfg yolo.weights $variables_INPUT_IMAGE

Copy and paste the result in your host repository

    Docker cp $variables_DOCKER_CONTAINER_NAME:/root/darknet/predictions.png $variables_OUTPUT_IMAGE

Check now your output image to visualize the detection result :)
