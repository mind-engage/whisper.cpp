## Cuda issue
- system has unsupported display driver / cuda driver combination  
https://github.com/NVIDIA/nvidia-docker/issues/1256


Build the image
```
docker buildx build -t mind-engage-transcribe -f .devops/main-cuda.Dockerfile .
```

Download image
```
docker run --rm -v $PWD:/data -it mcntech/mind-engage-transcribe:v01 "./models/download-ggml-model.sh medium.en"
```

Test the docker image
```
docker run --gpus device=0 -p 8090:8080 -v $PWD:/data -it mcntech/mind-engage-transcribe:v01 "./server --convert --host 0.0.0.0 -debug -m /data/ggml-medium.en.bin"
```