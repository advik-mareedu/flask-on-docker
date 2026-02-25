# Homework 3: Flask on Docker ![CI](https://github.com/advik-mareedu/flask-on-docker/actions/workflows/ci.yml/badge.svg)

This repository demonstrates how to design, containerize, and deploy a production-ready Flask web application using Docker and PostgreSQL. It walks through building a clean development environment with Docker Compose, integrating a persistent Postgres database, and configuring a secure production stack powered by Gunicorn and Nginx. The project highlights best practices such as multi-stage Docker builds, non-root containers, environment-based configuration, and proper handling of static and user-uploaded media files—serving as a practical reference architecture for deploying scalable Python microservices.

Below is a video showing myself using this Flask web application to upload an image and view it.
![flask web app video](flask_web_app_vid.mov)

Here are the Build Instructions:

Development Setup
1. Build the images:
```
docker-compose build
```
2. Start the contains:
```
docker-compose up -d
```
3. Create the database tables:
```
docker-compose exec web python manage.py create_db
```
(Optional) Seed the database:
```
docker-compose exec web python manage.py seed_db
```
4. Access the application:
App: http://localhost:8000/  
Static files: http://localhost:8000/static/hello.txt  
File uploads: http://localhost:8000/upload
5. View logs (if needed):
```
docker-compose logs -f
```
6. Stop containers:
```
docker-compose down -v
```

Production Setup
1. Build and start the production stack:
```
docker-compose -f docker-compose.prod.yml up -d --build
```
2. Create the database:
```
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```
3. Access the application:
App (via Nginx): http://localhost:8000
Static files: http://localhost:8000/static/hello.txt
Media files: http://localhost:8000/media/<filename>
4. View production logs:
```
docker-compose -f docker-compose.prod.yml logs -f
```
5. Shut down production stack:
```
docker-compose -f docker-compose.prod.yml down -v
```

Quick Start (TL;DR)
Development:
```
docker-compose up -d --build
docker-compose exec web python manage.py create_db
```
Production:
```
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```
