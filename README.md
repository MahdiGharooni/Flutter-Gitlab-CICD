# Flutter in Gitlab CI\Cl

If you want to get Flutter output in Gitlab Ci\Cl this articla is for you.

I want to explain how you can get **Flutter** ouput by **Docker Image**.

**NOTE:** If you are new in gitlab CI\Cl you can read [this](https://docs.gitlab.com/ee/ci/ "this"), to know why should we use it.

**NOTE:** If you are new in docker you can read [this](https://docs.docker.com/get-started/ "this").



## Getting Started
As you read before you should add a `.gitlab-ci.yml` file to root of project. Gitlab will read this file to execute and get flutter output. It needs **Java & Flutter SDK** for woking, so we will add them by a **docker image** and you can use flutter commands easily.
In this project I use my flutter docker image that exists in [dockerHub](https://hub.docker.com/repository/docker/mahdigharooni/flutter "dockerHub"). If you want know how I prepare it you can see this [Github repository](https://github.com/MahdiGharooni/flutter_docker_image "Github repository") .


You should add this in first line of  `.gitlab-ci.yml` file:
	`image: mahdigharooni/flutter:latest `

and now you can introduce your stages and what Gitlab should do . In mine I want to get a debug apk in develop branch and keep it in artifacts:


    image: mahdigharooni/flutter:latest
    
    stages:
      - build
    
    flutter_build:
      stage: build
      before_script:
        - flutter channel stable
        - flutter upgrade
        - flutter pub get
        - flutter clean
      script:
        - flutter analyze
        - flutter build apk --debug
      artifacts:
        paths:
          - build/app/outputs/apk/debug/app-debug.apk
      only:
        refs:
          - develop
    


you can change it as you project.

