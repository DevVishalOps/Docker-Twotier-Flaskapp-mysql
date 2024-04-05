# Flask App with MySQL Docker Setup
This is a simple Flask app that interacts with a MySQL database. The app allows users to submit messages, which are then stored in the database and displayed on the frontend.

# Prerequisites
Before you begin, make sure you have the following installed:

1.Docker
2.Git (optional, for cloning the repository)

# Setup for Dockerfile
1.Clone this repository 
```bash
https://github.com/VishalRepoWizard/Docker-Twotier-Flaskapp-mysql.git
```
2.Build Flaskapp image using Dockerfile run this command where Dockerfile present
```bash
sudo docker build . -t flaskapp
```
3.Pull Mysql Image from DockerHub
```bash
sudo docker pull mysql:5.7
```
4.Create network and check network
```bash
sudo docker network create twotier
sudo docker network ls
```
5.Using this command you can create container and run the flaskapp container
```bash
sudo docker run -d -p 5000:5000 --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DB=mydb --name=flaskapp flaskapp:latest
```

6.Using this command you can create container and run the Mysql container
```bash
sudo docker run -d -p 3306:3306 --network=twotier MYSQL_DATABASE=mydb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_ROOT_PASSWORD=admin --name=mysql mysql:5.7
```

7.If youwant see running container then run this commmand
```bash
sudo docker ps
```

8.Then enter mysql container using this and check databases is create or not 
```bash
sudo docker exec -it <here_container_id> bash
```

9.If you enter in mysql container then run this
```bash
mysql -u <username> -p <password>
```
10.create "message" table in your mysql database
```bash
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
```
# Setup for Docker compose
- Start the containers using Docker Compose:
```bash
sudo docker-compose up --build
```

# Usage 
1.Access the Flask app in your web browser:
- Frontend: http://localhost
- Backend: http://localhost:5000

2.Interact with the app:
- Visit http://localhost to see the frontend. You can submit new messages using the form.
- Visit http://localhost:5000/insert_sql to insert a message directly into the messages table via an SQL query.

# Cleaning Up
- If you create containers using Dockerfile and want to remove container use this command 
```bash
sudo docker kill -f <container_id>
```
- To stop and remove the Docker containers, press Ctrl+C in the terminal where the containers are running, or use the following command
```bash
sudo docker-compose down
```
# Notes

- Make sure to replace placeholders (e.g., your_username, your_password, your_database) with your actual MySQL configuration.

- This is a basic setup for demonstration purposes. In a production environment, you should follow best practices for security and performance.

- Be cautious when executing SQL queries directly. Validate and sanitize user inputs to prevent vulnerabilities like SQL injection.

- If you encounter issues, check Docker logs and error messages for troubleshooting.







