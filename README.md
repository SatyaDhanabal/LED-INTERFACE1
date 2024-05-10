# LED-INTERFACE
import sys
sys.path.append('/home/pi/Adafruit-Raspberry-Pi-Python-Code￾legacy/Adafruit_CircuitPython_MCP230xx-main') # LIBRARY
import time
import board
import busio
from digitalio import Direction, Pull
from adafruit_mcp230xx.mcp23017 import MCP23017
# Initialize the I2C bus:
i2c = busio.I2C(board.SCL, board.SDA)
# Initialize the MCP23017 chip on the bonnet
mcp = MCP23017(i2c)
# Optionally change the address of the device if you set any of the A0, A1, A2
# pins. Specify the new address with a keyword parameter:
mcp = MCP23017(i2c, address=0x20) # MCP23017
# Make a list of all the port A pins (Refer User Manual page no 14)
PortA = [ ]
for pin in range(0, 8):
 PortA.append(mcp.get_pin(pin))
# Make a list of all the port B pins (Refer User Manual page no 14)
PortB = [ ]
for pin in range(8, 16):
 PortB.append(mcp.get_pin(pin))
for pin in range(0,8): # CLEARING ALL THE PORT A PINS
 PortA[pin].value=False
for pin in range(0,8): # CLEARING ALL PORT B PINS
 PortB[pin].value=False
PortA[0].direction = Direction.OUTPUT
PortA[1].direction = Direction.OUTPUT
PortA[2].direction = Direction.OUTPUT
PortA[3].direction = Direction.OUTPUT
PortA[4].direction = Direction.OUTPUT
PortA[5].direction = Direction.OUTPUT
PortA[6].direction = Direction.OUTPUT
PortA[7].direction = Direction.OUTPUT
PortB[0].direction = Direction.OUTPUT
try:
 while True:
 print("RED LED ON")
 PortA[0].value = True
 PortA[3].value = True 
 PortA[6].value = True
 time.sleep(2)
 print("GREEN LED ON")
 PortA[1].value = True
 PortA[4].value = True 
 PortA[7].value = True
 time.sleep(2)
 print("BLUE LED ON")
 PortA[2].value = True
 PortA[5].value = True 
 PortB[0].value = True
 time.sleep(2)
 print("RED LED OFF")
 PortA[0].value = False
 PortA[3].value = False 
 PortA[6].value = False
 time.sleep(2)
 print("GREEN LED OFF")
 PortA[1].value = False
 PortA[4].value = False 
 PortA[7].value = False
 time.sleep(2)
 print("BLUE LED OFF")
 PortA[2].value = False
 PortA[5].value = False 
 PortB[0].value = False
 time.sleep(2)
except KeyboardInterrupt: # CLEAR ALL PORT PINS Press CTRL+C
 for pin in range(0,8):
 PortA[pin].value=False
 for pin in range(0,8):
 PortB[pin].value=False
