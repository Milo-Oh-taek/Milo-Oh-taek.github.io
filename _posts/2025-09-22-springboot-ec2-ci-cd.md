---
title: springboot github action docker ec2 cicd
date: 2025-09-22 20:40:00 +01:00
categories: [CICD]
tags: [cicd, github, docker]
---

### Dockerfile

```
FROM openjdk:23

WORKDIR /app

COPY target/demo-*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

### main.yml

```
name: build test

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up JDK
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: 23

      - name: Build with Maven
        run: mvn clean package -DskipTests

      - name: Docker build
        run: docker build -t ${{ secrets.DOCKER_HUB_USERNAME }}/javademo:latest .

      - name: Docker login
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKER_HUB_USERNAME }}
          password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

      - name: Docker push
        run: docker push ${{ secrets.DOCKER_HUB_USERNAME }}/javademo:latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Install SSH key
        uses: webfactory/ssh-agent@v0.9.0
        with:
          ssh-private-key: ${{ secrets.EC2_SSH_PRIVATE_KEY}}

      - name: Deploy on EC2
        run: |
          ssh -o StrictHostKeyChecking=no ${{ secrets.EC2_USER }}@${{ secrets.EC2_HOST }} << 'EOF'
                      sudo docker login -u ${{ secrets.DOCKER_HUB_USERNAME }} -p ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}
                      sudo docker pull ${{ secrets.DOCKER_HUB_USERNAME }}/javademo:latest
                      sudo docker stop javademo || true
                      sudo docker rm javademo || true
                      sudo docker run -d --name javademo -p 80:8080 ${{ secrets.DOCKER_HUB_USERNAME }}/javademo:latest
          EOF
```
