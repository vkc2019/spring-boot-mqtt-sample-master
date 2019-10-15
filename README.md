
## MQTT PUBLISHER AND SUBSCRIBER
Sample Spring Boot application that publishes message to a topic on mqtt server and receives messages from specific topics.

**Before Run And Compile**

You should change publisherId and server url from 

> src/main/java/com/gulteking/mqttbackendserver/config/Mqtt.java

Edit Lines Below(publisher id optional):

    private static final String MQTT_PUBLISHER_ID = "spring-server";  
    private static final String MQTT_SERVER_ADDRES= "tcp://127.0.0.1:1883";

**Compile and Run(in pom.xml)**

    mvn clean install
    java -jar target/mqtt-backend-server-0.0.1-SNAPSHOT.jar

**Publish message(POST: /api/mqtt/publish)**

    {
    	"message": "testMessage",
    	"topic":"test",
    	"retained":true,
    	"qos":0
    }

**Subscribe Messages From a Topic For X Milliseconds**

**GET: /api/mqtt/subscribe?topic=test&wait_millis=5000**

Returns message array after 5 seconds:

    [
        {
            "message": "testMessage",
            "qos": 0,
            "id": 0
        }
    ]

** RUN USING PM2 **
> create a file process.json

	{
	    "apps":[
	    {
	        "name":"pm2-java",
	        "cwd":".",
	        "script":"/usr/bin/java",
	        "args":[
	            "-jar",
	            "/path/mqtt-backend-server-0.0.1-SNAPSHOT.jar"
	        ],
	        "watch":[
	            "/path/mqtt-backend-server-0.0.1-SNAPSHOT.jar"
	        ],
	        "node_args":[],
	        "log_date_format":"YYYY-MM-DD HH:mm Z",
	        "exec_interpreter":"",
	        "exec_mode":"fork"
	     }
	   ]
	}

> pm2 start process.json

> original project : https://github.com/gulteking/spring-boot-mqtt-sample
