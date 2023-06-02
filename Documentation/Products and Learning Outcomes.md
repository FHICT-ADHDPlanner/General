# Products and Learning Outcomes
This document will showcase the different products I have made during this semester. This will also explain what part of the products cover the different outcomes.

## Table of Content

## GitHub
Before starting anything, it was important to set up a way to handle project files in an efficient way: GitHub. I started by making an [GitHub Organization](https://github.com/FHICT-ADHDPlanner) in which I could bundle my repositories. The goal of this was to put the API, frontend and general documentation in separate repositories. This way it is easier to keep the different elements apart while keeping it in one place. 

### CI/CD
The next important element to set up was the CI/CD. This stands for continuous integration and continuous delivery, this means the automation of integration and delivery/deployment of the many different aspects of the project. Every repository goes through roughly the same process. Although this process does contain a few different key steps:

- Build- and unit-testing

The beginning of the CI/CD process is pretty straight forward: This step tests if the application can be build successfully. If this build is successful, then run through all the tests in the project. If these also pass then this step is done. This step is done so it can be ensured that only the functional code will be pushed to the main branches. This means that the live environment will always have the functional code. 

- Docker build-testing and deployment

The next step in this process is the docker-testing and deployment. All of the services run in dockerized containers. More about this will be discussed in the Docker chapter. To build containers, docker requires docker images. These images will be supplied through Dockerhub in separate repositories. 

When a push or merge to main transpires, the image on Dockerhub will need to be replaced with the new most recent code. This part of the CI/CD is responsible for that. The start of this is that GitHub will test if the docker image can be build from the new files in the main branch, using the custom made Dockerfile. If this build succeeds, the process will log into Dockerhub with the credentials that are in GitHub secrets, and then push this docker image to the corresponding Dockerhub repositories. If these both succeed, the new image will be deployed to Dockerhub and is ready to be used for server-sided deployment. 

<details>
<summary>GitHub CI/CD Flow File (yaml)</summary>

``` yaml
name: Main

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: 7.0.x
    - name: Restore dependencies
      run: dotnet restore "./ADHDPlanner-Backend" 
    - name: Build
      run: dotnet build --no-restore "./ADHDPlanner-Backend"
    - name: Test
      run: dotnet test --no-build --verbosity normal "./ADHDPlanner-Backend"

  deployment:
   name: deployment
   runs-on: ubuntu-latest
   needs: build
   steps:
     - name: Checkout repository
       uses: actions/checkout@v2
     - name: Set up Docker Buildx
       uses: docker/setup-buildx-action@v1
     - name: Login to DockerHub
       uses: docker/login-action@v1
       with:
         username: ${{ secrets.DOCKER_HUB_USERNAME }}
         password: ${{ secrets.DOCKER_HUB_TOKEN }}
     - name: Build and push
       uses: docker/build-push-action@v2
       with:
         context: ./ADHDPlanner-Backend/
         file: ./ADHDPlanner-Backend/ADHDPlanner-Backend/Dockerfile
         push: ${{ github.event_name != 'pull_request' }}
         tags: ${{ secrets.DOCKER_HUB_USERNAME }}/adhdplanner-backend:latest
         
  SonarCloud:
    name: Build and analyze
    runs-on: windows-latest
    steps:
      - name: Set up JDK 11
        uses: actions/setup-java@v3
        with:
          java-version: 11
          distribution: 'zulu' # Alternative distribution options are available.
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis
      - name: Cache SonarCloud packages
        uses: actions/cache@v3
        with:
          path: ~\sonar\cache
          key: ${{ runner.os }}-sonar
          restore-keys: ${{ runner.os }}-sonar
      - name: Cache SonarCloud scanner
        id: cache-sonar-scanner
        uses: actions/cache@v3
        with:
          path: .\.sonar\scanner
          key: ${{ runner.os }}-sonar-scanner
          restore-keys: ${{ runner.os }}-sonar-scanner
      - name: Install SonarCloud scanner
        if: steps.cache-sonar-scanner.outputs.cache-hit != 'true'
        shell: powershell
        run: |
          New-Item -Path .\.sonar\scanner -ItemType Directory
          dotnet tool update dotnet-sonarscanner --tool-path .\.sonar\scanner
      - name: Build and analyze
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}  # Needed to get PR information, if any
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        shell: powershell
        run: |
          .\.sonar\scanner\dotnet-sonarscanner begin /k:"FHICT-ADHDPlanner_Back-end" /o:"fhict-adhdplanner" /d:sonar.login="${{ secrets.SONAR_TOKEN }}" /d:sonar.host.url="https://sonarcloud.io"
          dotnet build "./ADHDPlanner-Backend"
          .\.sonar\scanner\dotnet-sonarscanner end /d:sonar.login="${{ secrets.SONAR_TOKEN }}"
```


</details>

### Security and quality
Next to the building and deployment of the application, GitHub also provides useful tools to analyze the code and make sure vulnerabilities get noticed and resolved. My project utilizes two of these technologies. These are part of the CI/CD process. These technologies are the following:

- CodeQL



## Planner API microservice
The first product I have worked on for this project was the main API backend application that makes sure that tasks can be requested, saved and edited. The API contains Secure Access points, this was done as to not have user see other users tasks. 

These secure access points require authorization through Auth0 (which will be touched upon later in the Auth0 *add link* chapter). These access points are CRUD access points for data and are only meant to be accessed by authorized users. 

The decision was made to use CRUD instead of CRUA because of the nature of the service. It is not necessary to archive any data if the user wants to delete a task from their planner. Thus CRUD was used. 

#### Accessing the API
As the API is running on a separate server, the endpoints are slightly different. In this case, the API endpoints will be:
> GET Task: http://86.92.40.132:1001/api/Task/{id}

> GET Tasks: http://86.92.40.132:1001/api/Task

> POST Task: http://86.92.40.132:1001/api/Task

> PUT Task: http://86.92.40.132:1001/api/Task/{id}

#### Demonstration
Here is a quick demonstration of the API. For demonstration purposes Postman was used. 

#### Outcomes
The product touches learning outcomes 1 and 2.


