

In this article we will be deploying the game “2048” using Docker and Amazon Web Services (AWS). we’ll go through the step-by-step process of containerizing the 2048 game and then seamlessly deploying it onto the AWS platform.

The tools utilized in this project are as follows:
Github
Visual Studio Code
Docker
AWS -Elastic Beanstalk
Step1: Create a Docker file
Open the terminal and execute the following commands.

mkdir <directory name>
cd <directory name>
code .

After executing the commands, the Visual Studio Code window will open.


Create a file “Dockerfile” inside the created directory


Next, type the following script

FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y nginx zip curl
RUN echo "daemon off;">>/etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/jabir000/2048/zip/master
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip
EXPOSE 80
CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
*please replace the “ubuntu:22.04” with yours


Open a new terminal


Execute the following commands in the new terminal

pwd

ls

docker build -t <docker image name> . 

docker images

docker run -d -p 80:80 <container id>

docker ps

The creation of the container is successful.

To verify if the game is functioning correctly, access localhost via port 80.


Now, we want to deploy it to AWS using Elastic Beanstalk
AWS Elastic Beanstalk
It is a fully managed Platform as a Service (PaaS) offering from Amazon Web Services.

It simplifies the deployment and management of web applications and services in the cloud.

With support for various programming languages and platforms, developers can easily upload their code and let Elastic Beanstalk handle the provisioning and scaling of the infrastructure.

The service automatically monitors application health and performs auto-scaling to adjust resources based on demand.

This enables developers to focus on building their applications without worrying about the underlying infrastructure complexities.

1 . Create Application


2. Select Web Server Environment.


3. Give a name to the Application.


4. Give a name to Environment and give a description.


5. Choose platform type as Managed Platform and platform as Docker.


6. In this section choose the option for Upload your code and upload the Docker file you created.



7. Choose the free tier eligible option.


8. Skip to review.


9. Submit.


10. The environment creation has been initiated.


11. Once the environment creation is successful, load the domain.



The game has been successfully deployed to AWS.
