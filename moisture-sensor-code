from machine import ADC
import time

adc = ADC(26)  # GP26 on pico board
samples = 10 #this helps our output be more stable by the code reading the sensor 10 times
#i2c to sd card
#cloud storage and use wifi and bluethooth to send text file to controller
# prototyping a controller for all of this 
#  

def read_moisture(): #the A0 on the Soil Moisture Sensor Module maps to ADC(26) pin GP26 on the board which is where we are reading from
    total = 0
    for _ in range(samples):
                
        total += adc.read_u16() #this reads the analog voltage from the sensor 0 to 65535 where 0 is 0V and 65535 is 3.3V
    avg = total / samples
    return avg

while True:
    raw_voltage = read_moisture() 
    moisture_percent = int((raw_voltage / 65535) * 100) #to get the moisture percent I took the read analog voltage(line 11), divided it by the max voltage (65535 = 3.3V), and then multiplied by 100
    
    if moisture_percent > 22.5: #the 22.5 is the moisture detection percent for sandy loam which is sand silt and clay... we can change it depending on NASA Soil type
        status = "Moisture Detected"
    else:
        status = "Soil is Dry"
    
    print(f"Moisture: {moisture_percent}% ({status})")
    time.sleep(180) #it reruns every 3 minutes, this can be shortened/increased so 180 seconds
