# Pipeline that builds docker images and uses terraform to create cluster and deploy application for testing

# 1. Create compute engine instance with following settings:
        Deploy a container image to this VM instance 
            Use hello-world for the container
        Allow full access to all Cloud APIs
        Allow HTTP traffic

# 2. SSH into the vm and run the following command:

docker run -d -p 80:8080 -p 50000:50000 --name jenkinsdemo -v jenkins_home:/var/jenkins_home drehnstrom/jenkins-gcp:v0.2

# 3. When it has completed, run the following to get the admin password. You may need to wait a while even after the previous command finishes before this is ready.

docker exec jenkinsdemo cat /var/jenkins_home/secrets/initialAdminPassword

# 4. Create a new pipeline, configure it with the content of the Jenkinsfile

# 5. set the projectID var on the first line to your project id.

# 6. Run the pipeline.

# If you want to set up a trigger, you'll need to create your own repos from at least one of the git endpoints in the script, and modify the Jenkinsfile accordingly.