# cicd-pipeline-train-schedule-docker

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Running the app

You need a Java JDK 7 or later to run the build. You can run the build like this:

    ./gradlew build

You can run the app with:

    ./gradlew npm_start

Once it is running, you can access it in a browser at http://localhost:8080

## Docker based deployment of the app

### Installing Docker on a Jenkins (centos) server

Run the following commands to install the docker and enable it to start at boot.

    sudo yum -y install docker
    sudo systemctl enable docker
    sudo systemctl start docker

Run the following commands to enable Jenkins to run various docker command without needing `sudo` credentials.

    sudo groupadd docker
    sudo usermod -aG docker jenkins

After doing the group related changes listed above, restart both docker and jenkins so that they both recognise the updated group permissions.

    sudo systemctl restart jenkins
    sudo systemctl restart docker

### Build the docker image

Refer to the added Dockerfile for details on the details of what will be included in the docker image.
Run the following command to build the docker image:

    docker build -t train-schedule .

Refer to the added Dockerfile for details on the details of what will be included in the docker image.

Run the following command to launch the app in a container.

    docker run -d -p 8080:8080 train-schedule

Access the application by lauching a browser and accessing the page `localhost:8080`

Add the `--restart always` switch to `docker run` command so that if the app in the container crashes for any reason the docker will automatically launch a new container in its place.
