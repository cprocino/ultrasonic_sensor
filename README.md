# ultra sonic sensor
for this project we needed to set up an ultra-sonic sensor to show a color value on its built in led dependent on the distence from the sensor.
this project took some time to get the code and set up the wiring but over all was not too difficult 
here is the code I used courtesy of help from Gaby:



import time #huge thanks to gaby for help on this code
import board
import adafruit_hcsr04
import neopixel
import simpleio

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)   # creating sonar variable
dot = neopixel.NeoPixel(board.NEOPIXEL, 10, brightness=0.5) # creating dot variable 

r = 0  # setting my three colors ints to 0
g = 0
b = 0


while True:

    try:
        distance = sonar.distance # setting the variables
        print((distance))

        if distance < 5: # start of if statement if distance is less than f then set the color vaiables to red
            r = 255 # acitivated variable
            g = 0
            b = 0
        elif distance > 5 and distance < 20: # this else statement creates the second color preset
            r = simpleio.map_range(distance, 5, 20, 255, 0) # set up the distance color conection
            b = simpleio.map_range(distance, 5, 20, 0, 255) # set up the distance color conection
            g = 0 
            r = int(r)   # ints set up
            g = int(g)
            b = int(b)
        elif distance > 20 and distance < 35: # this else statement creates the second color preset
            r = 0
            b = simpleio.map_range(distance, 20, 35, 255, 0)  # acitivated variable with the var distance to get blue and green going 
            g = simpleio.map_range(distance, 20, 35, 0, 255)
            r = int(r)
            g = int(g)   # ints set up
            b = int(b)
        elif distance > 35:  #else if for > than 35
            r = 0    #  vars  set to pure green if its out side the range we want
            b = 0
            g = 255
            r = int(r)
            g = int(g)
            b = int(b)
        print(r, g, b)  # prints the color variables to show us the color in code
        time.sleep(0.05)

    except RuntimeError:  # gives us simple error message if it doesn't work 
        print("Retrying!")
        r = 0
        g = 0
        b = 255
        time.sleep(0.1)

    print(r, g, b)  
    dot.fill((r, g, b)) # tells the dot variable what to do
    time.sleep(0.05) # delay so code don't break

this project took focus and time to complete and the consistant problem of getting the correct file to the right place in my computer. the code for this is long but not overly complex.
