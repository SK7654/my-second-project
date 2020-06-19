# my-second-project
![Asset-36-1](https://user-images.githubusercontent.com/64473684/85101273-a9292e00-b21f-11ea-9eb2-a05776d88b3f.png)
A CI/CD Pipeline implementation, or Continuous Integration/Continuous Deployment, is the backbone of the modern DevOps environment. It bridges the gap between development and operations teams by automating the building, testing, and deployment of applications.Having vast applications of these devops tools integrations , SCM tools like Github , management tools like Jenkins and container tool like docker becomes the backbone of this pipeline of CI/CD to launch the applications within few clicks where all the internal works are done by these tools in the background. The main intention of this pipeline is to make this deployment as fast as possible wherein no human intervention occurs.

As part of the projects I've been building , I've come up with one more integration of github , jenkins and dockers where your application containing the code is deployed in the webserver within seconds.

Wholelly the task goes as : I've created an image of the docker , when launched it automatically starts jenkins inside the container with the "git" software previously installed to support the github plugin. The container launched also has access to the docker service running on the base system to launch containers remotely from inside the container. So , as soon as the code has been pulled from the github seeing the code my jenkins will sutomatically start the necessary code interpreter and hosts it in the webserver. Moving furthur ahead , it also checks the status code of the deployed web services to lauch the application into the production world.

Going deep dive into the project :

Creation of Dockerfile: Using the dockefile concept I've built an images that has git and jenkins pre installed and starts the jenkins services as soon as the container is lauched using that image. I've pre-installed git to support the github plugin in the jenkins services.
