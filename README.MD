<h1 align = "center">LilyGo SIM7000G</h1>

LilyGo SIM7000G will have two inputs, Passive Infrared Sensor (PIR) and magnetic reed switch. There will be two outputs, one will be on/off and the other driving a servo to 90, delay 2 seconds and then back to 0.

The LilyGo SIM7000G will also upload via MQTT its GPS location once a day and the battery voltage if it changes by 5%.

The LilyGo SIM7000G listen on MQTT to messages to know its state. If the user changes the state the will update it state.

### Operation

1. Will listen and publish to a MQTT broker via NB-IOT. If NB-IOT is not available it needs the cycle thru 4G, 3G and 2G and set to the most reliable mode.
2. The LilyGo listen to MQTT stream.
3. The MQTT stream contain information as to if the outputs needs to be active or not. It will save this state.
4. If the outputs are set to active, when the PIR is triggered or the reed switch change state. The output go high for 3 seconds and the servo output will cycle from 0 => 90 delay 2 seconds and 90=>0 
5. It will at the same time publish to the MQTT broker that the PIR is triggered or the reed switch change state
6. When the battery voltage changes more that 5% it will publish to the MQTT broker the new voltage.
7. Once a day the LilyGo will publish via MQTT its location to the DB.
8. If via MQTT a request is published to the LilyGo for its location it will update the DB with its location.
9. Via Bluetooth the state of the outputs will be set to active or not. If this state is set via blue tooth the LilyGo will publish via MQTT and update the DB.
10. The LilyGo will have a EUI that consist of 16 hex characters.

### Mqtt

* []()mqtt_user = "IamHere"
* []()mqtt_pass = "*************"
* []()mqtt_broker = 10.0.0.1
* []()mqtt_port = 8883
* []()ma=qtt_topic = EUI


### Json

1. Downlink setting outputs active
      
      "payload": {
            "eui": "24E124136B320041",
            "set": "0", // Bool 0/1
        }

2. Uplink setting were done via Bluetooth
         
         "payload": {
            "eui": "24E124136B320041",
            "set": "0", // Bool 0/1
         }

3. Uplink setting location
         
         "payload": {
            "eui": "24E124136B320041",
            "lattitude": -29.992233,
            "longnitude": 30.112233
         }

4. Downlink requsting location
         
         "payload": {
            "eui": "24E124136B320041",
            "location":  "1", // Bool 1
         }

5. Uplink updating battey voltage
         
         "payload": {
            "eui": "24E124136B320041",
            "battV":  4.102
         }