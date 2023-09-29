MERN Project 

1. Create EC2 instance for Frontend and Backend Servers 

    Frontend Server: tilak-travelapp_frontend 
    Backend Server: tilak-travelapp_backend 

2. Install updates on Frontend and Backend servers and install the required applications 
    #apt update 
    Install Nginx Application 
    #apt install nginx –y 
    Install Node JS and NPM Followed the link to install NodeJS 

# curl -s https://deb.nodesource.com/setup_18.x | sudo bash 
# sudo apt install nodejs –y 
# node -v 

Till now we have gone with the required application installation now will go with the Cloning of the code from Github. 

Now will make few manual configurations on the backend server. 

Create a new .env file in the Backend application directory 

Mongo_URI=” mongodb+srv://tilakpechetti:xxxxxx%4012@cluster0.nitiwty.mongodb.net/” 

PORT=”3000” 

3. Backend Server configuration 

Simple configuration right!!! That's it no other changes are required. 

    Now start the application using below commands 
    #npm install 
    #node index.js (which will start the application) Please see the screenshot for reference. 
    To Test if the application is running or not 
    Use the Server IP or else custom domain name or else an API URL. 
    
    Configure Nginx to bypass proxy on backend server. 
    Below is the configuration steps that needs to be updated 
    #sudo unlink /etc/nginx/sites-enabled/default 
    #cd /etc/nginx/sites-available/ 

        #sudo nano custom_server.conf 
        server { listen 80; 
        location / { 
        proxy_pass http://my_server; 
        }} 

    #sudo service nginx configtest 
    #sudo service nginx restart  

Now we will configure the  Frontend server 
After the required applications are installed follow the below steps 
Clone the code 
    # sudo git clone https://github.com/UnpredictablePrashant/TravelMemory 
    Check the node version is latest, I have v18.17.1 
    Next step is to update the backend URL in the frontend server on below path 
    My Application path is: 
    /opt/TravelMoemory/frontend/src/url.js 
    After the configuration is done,  
    
    #npm install 
    Then  
    #npm start 
    Which will allow you to launch and you should be able to connect to frontend server 
    Test: 
    # Curl –V localhost 

    It should give you the result 
    Once are you able to access the URL, please the record and it should be visible in the database. 

Configuring Load-Balancer 

In AWS Create a New application loadbalancer and create a listner port no:80 and attach the target group as shown below. 

Make sure the Target group is healthy 
Attached target group 
Target group should be Healthy 

Below are the details of the load balancer configured as shown 
Load_Balancer DNS Name:  

# tilak-loadbalancer-1665065052.ap-south-1.elb.amazonaws.com 

Opened website with Load Balancer URL 
Updating the Load balancer DNS Name in Cloud Flair as CNAME record 
Custome domain name for URL: Travel-api.tilakpechetti.co.in 

Done 

 
##########################################################################################################################################
# Travel Memory

`.env` file to work with the backend:

```
MONGO_URI='ENTER_YOUR_URL'
PORT=3000
```

Data format to be added: 

```json
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
```
