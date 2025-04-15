# Microservice-App
Microservice Architecture and System Design with Python &amp; Kubernetes

## The Application
A user can upload a video to be converted in a mp3-file. The request will first hit the gateway. The gateway will store the video in MongoDB and then put a message on the queue (RabbitMQ). The downstream services will know that there is a video to be processed in the database. The video-to-mp3 converter service will consume messages from the queue. It will then get the ID of the video from the message, pull the video from the DB and convert it to mp3. The mp3 will be stored in the database and put a new message on the queue. The message will be consumed by the notification serivce that informs the user about job completion via email. The client will then use a unique ID aquired from the notification plus the jwt to make a request to the API-gateway to download the mp3-file. The API-gateway will pull the mp3-file from the storage and serve it to the client. 

<img width="1097" alt="image" src="https://github.com/user-attachments/assets/33487a08-fc7f-4bd2-adad-60b52fcebd41" />

