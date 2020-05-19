# Pipeline that builds docker images and uses terraform to create cluster and deploy application for testing

0. PREREQUISITES: make sure cloud build and kubernetes apis are enabled in the gcp project.

1. Create compute engine instance with following settings:
        Deploy a container image to this VM instance 
            Use hello-world for the container
        Allow full access to all Cloud APIs
        Allow HTTP traffic

2. SSH into the vm and run the following command:

    docker run -d -p 80:8080 -p 50000:50000 --name jenkinsdemo -v jenkins_home:/var/jenkins_home drehnstrom/jenkins-gcp:v0.2

3. When it has completed, run the following to get the admin password. You may need to wait a while even after the previous command finishes before this is ready.

    docker exec jenkinsdemo cat /var/jenkins_home/secrets/initialAdminPassword

4. Log in to Jenkins and install suggested plugins.

5. After creating a user, create a new pipeline, and configure it with the content of the Jenkinsfile in this repo

6. In the script, set the projectId variable on the first line to your project id.

    def projectId = "your-project-id-here"

7. Run the pipeline. It takes a while, as it downloads 2 repos, runs tests, builds docker images and pushes them to gcr.io, then downloads terraform repo, builds the cluster and deploys the images.


If you want to set up a trigger from a commit, you'll need to create your own repos from at least one of the git endpoints in the script, and modify the Jenkinsfile accordingly.