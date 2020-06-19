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
#INSTALLED_JENKINS_PLUGIN_SCREENSHOOT
![9 1](https://user-images.githubusercontent.com/64473684/85106568-0c1fc280-b22a-11ea-83b9-9807e896f0c3.PNG)
![9 2](https://user-images.githubusercontent.com/64473684/85106584-117d0d00-b22a-11ea-8046-33307f858371.PNG)
![9 3](https://user-images.githubusercontent.com/64473684/85106600-180b8480-b22a-11ea-8e52-98bead54e2b4.PNG)
![9 4](https://user-images.githubusercontent.com/64473684/85106623-20fc5600-b22a-11ea-8cbe-f608c373f51b.PNG)
![9 5](https://user-images.githubusercontent.com/64473684/85106636-28bbfa80-b22a-11ea-83d1-f032e9bb7256.PNG)
![9 6](https://user-images.githubusercontent.com/64473684/85106659-2fe30880-b22a-11ea-9c4e-2738dccc213c.PNG)
![9 7](https://user-images.githubusercontent.com/64473684/85106677-36718000-b22a-11ea-890c-c5a11c5a9023.PNG)

Moving furthur into various jobs of the jenkins. I've created a jenkins pipeline of 4 jobs wherein:

JOB 1 : Pulls the code from github and copies it in the folder named code in the /var folder of the base container named "jen1" in my case. Ive used a remote URL trigger to trigger the job as soon as the code is launched to github by placing it in the post-commit actions of the git.

![2 1](https://user-images.githubusercontent.com/64473684/85108833-062be080-b22e-11ea-8eb2-9225f07566ec.PNG)
![13](https://user-images.githubusercontent.com/64473684/85108902-20fe5500-b22e-11ea-89ae-9df9ec7c307d.PNG)
![11](https://user-images.githubusercontent.com/64473684/85108848-0d52ee80-b22e-11ea-874a-ca8cdc2389d0.PNG)

JOB 2 : This job triggers as soon as the JOB1 is built successfully and this job checks the code and respectively launches the respective interpreter, copies the code to that interpreter container and deploys the code to the webserver.
![14](https://user-images.githubusercontent.com/64473684/85109758-771fc800-b22f-11ea-935e-a274b11729db.PNG)


JOB3 : This JOB simultaneously triggers after the successful build of the job2 and this job checks the "http code" of the webserver i.e., this job ensure if the code is working properly on the wenserver if it has any error it sends a mail to the developer to recheck the code.

![15](https://user-images.githubusercontent.com/64473684/85111952-a421aa00-b232-11ea-98e7-c39cd104239d.PNG)
![16](https://user-images.githubusercontent.com/64473684/85111978-a84dc780-b232-11ea-830b-95a85f0de27d.PNG)

JOB4 : After all the above mentioned jobs are run successfully then this job triggers and keeps on checking whether the interpreter container is running and if in case the container stops it starts the container again. Finally it acts as a monitoring job to monitor the interpreter container.
![21](https://user-images.githubusercontent.com/64473684/85113603-2c08b380-b235-11ea-9587-86e8726669c8.PNG)

With all the jobs successfully run and no errors in the code , the port 80 of my apache webserver shows this output which is the php code in my github:

![23](https://user-images.githubusercontent.com/64473684/85114722-0c26bf00-b238-11ea-8738-a21f2e006c30.PNG)

Using the build pipeline plugin I've created a project overview of the jobs so that it would be easy to manage the jobs which looks like :







