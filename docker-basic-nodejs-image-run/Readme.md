docker build .
//Any time a request comming from port http://localhost:8080 need to redirect to 8080 on docker container
docker run -p 8080:8080 <container-id>

//To run command inside containers
docker run -it <cid> sh
OR
docker exec -it <cid> sh

//To show all container files
docker ps

//To log container
docker log <cid>
