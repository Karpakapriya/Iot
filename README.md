# Iot
import time
from pyfirmata import Arduino, util

# Define pins
sensor_pin = "A6"
red_led_pin = 12
green_led_pin = 11
pump_pin = 10
REF = 700

# Initialize Arduino board
board = Arduino('/dev/ttyACM0')  # Adjust the port as needed

# Set pin modes
board.digital[red_led_pin].mode = pyfirmata.OUTPUT
board.digital[green_led_pin].mode = pyfirmata.OUTPUT
board.digital[pump_pin].mode = pyfirmata.OUTPUT

while True:
    # Read sensor value
    sensor_value = board.analog[sensor_pin].read()

    if sensor_value > REF:
        board.digital[red_led_pin].write(1)
        board.digital[green_led_pin].write(1)
        board.digital[pump_pin].write(1)
        time.sleep(0.07)
    else:
        board.digital[red_led_pin].write(0)
        board.digital[green_led_pin].write(0)
        board.digital[pump_pin].write(0)
        time.sleep(0.07)
