# my-second-project
![Asset-36-1](https://user-images.githubusercontent.com/64473684/85101273-a9292e00-b21f-11ea-9eb2-a05776d88b3f.png)
A CI/CD Pipeline implementation, or Continuous Integration/Continuous Deployment, is the backbone of the modern DevOps environment. It bridges the gap between development and operations teams by automating the building, testing, and deployment of applications.Having vast applications of these devops tools integrations , SCM tools like Github , management tools like Jenkins and container tool like docker becomes the backbone of this pipeline of CI/CD to launch the applications within few clicks where all the internal works are done by these tools in the background. The main intention of this pipeline is to make this deployment as fast as possible wherein no human intervention occurs.

As part of the projects I've been building , I've come up with one more integration of github , jenkins and dockers where your application containing the code is deployed in the webserver within seconds.

Wholelly the task goes as : I've created an image of the docker , when launched it automatically starts jenkins inside the container with the "git" software previously installed to support the github plugin. The container launched also has access to the docker service running on the base system to launch containers remotely from inside the container. So , as soon as the code has been pulled from the github seeing the code my jenkins will sutomatically start the necessary code interpreter and hosts it in the webserver. Moving furthur ahead , it also checks the status code of the deployed web services to lauch the application into the production world.

Going deep dive into the project :

Creation of Dockerfile: Using the dockefile concept I've built an images that has git and jenkins pre installed and starts the jenkins services as soon as the container is lauched using that image. I've pre-installed git to support the github plugin in the jenkins services.
![1](https://user-images.githubusercontent.com/64473684/85101740-c0b4e680-b220-11ea-8d6f-abc29eba6508.PNG)
Now build the image and push it to the docker hub using the following commands
 ![7](https://user-images.githubusercontent.com/64473684/85103398-340c2780-b224-11ea-9c5c-16bae418df0a.PNG)

Launching the container: With the docker image created , it is now up to make the docker commands run inside the container launched by using the above image created so that Jenkins can directly launch the required containers. For this I've directly mounted the "docker.sock file" on to the container and the docker config files on to the container to make the docker commadns executable. Also expose the container on the port 8080 to access the WebUI of the Jenkins.
![8](https://user-images.githubusercontent.com/64473684/85103379-2bb3ec80-b224-11ea-9fb5-5f43c8b6238c.PNG)

Jenkins running on the port number 8080, initially enter the jenkins using the initial admin password provided by jenkins at the location /root/.jenkins/secrets/initialAdminPassword. With jenkins properly functioning install the GITHUB plugin adn the build pipeline plugin.
