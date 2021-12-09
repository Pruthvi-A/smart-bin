import RPi.GPIO as GPIO #initializing GPIO pins
import time #initializing modules which are required 
import os
import audio
from csv import file
from distance import measurement
TRIG = 21 #setting up ultrasonic sensor 
ECHO = 20
PIR_input = 5 #initializing variables 
count = 0
# Initial set up of all sensors 
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
GPIO.setup(17,GPIO.OUT)
GPIO.setup(PIR_input, GPIO.IN)
GPIO.setup(TRIG,GPIO.OUT)
GPIO.setup(ECHO,GPIO.IN)
servo1 = GPIO.PWM(17,50)
print("distance measurement in progress")
GPIO.output(TRIG,False) #measuring output from ultrasonic sensor 
print("waiting for sensor to settle")
SMART BIN National College Jayanagar
DEPARTMENT OF COMPUTER SCIENCE PAGE 20
time.sleep(0.2) #delay 
GPIO.output(TRIG,True)
time.sleep(0.00001)
GPIO.output(TRIG,False)
while GPIO.input(ECHO)==0:
 pulse_start=time.time()
while GPIO.input(ECHO)==1:
 pulse_end=time.time()
pulse_duration=pulse_end-pulse_start
distance=pulse_duration*17150
distance=round(distance,2)
print("distance:",distance,"cm")
Full_distance = 2050
Half_distance = distance / 2.0
Quartly_distance = distance / 4.0
Empty_distance = 275
print(distance)
print(Full_distance)
print(Empty_distance)
audio.begin()
def measurement():
 GPIO.output(TRIG,False)
 time.sleep(0.2)
 GPIO.output(TRIG,True)
 time.sleep(0.00001)
 GPIO.output(TRIG,False)
 while GPIO.input(ECHO) == 0:
 pulse_start=time.time()
 while GPIO.input(ECHO) == 1:
 pulse_end=time.time()
SMART BIN National College Jayanagar
DEPARTMENT OF COMPUTER SCIENCE PAGE 21
 pulse_duration = pulse_end-pulse_start
 distance = pulse_duration*17150
 distance = round(distance,2)
 print("distance:",distance,"cm")
 
while True:
 print("measurement in progress")
 servo1.start(0)
 GPIO.output(TRIG,False)
 print("waiting for sensor to settle")
 if(GPIO.input(PIR_input)):
 #GPIO.output(LED, GPIO.HIGH)
 print(GPIO.input(PIR_input))
 servo1.ChangeDutyCycle(2+(180/18))
 time.sleep(0.5)
 servo1.ChangeDutyCycle(0)
 audio.trash()
 time.sleep(5)
 audio.thanks()
 servo1.ChangeDutyCycle(2+(0/18))
 time.sleep(0.5)
 servo1.ChangeDutyCycle(0)
 time.sleep(1)
 servo1.stop()
 else:
 #GPIO.output(LED, GPIO.LOW)
 print(GPIO.input(PIR_input))
 measurement()
 measurement()
 print(distance)
 print(distance)
 print(Full_distance)
 print(Empty_distance)
SMART BIN National College Jayanagar
DEPARTMENT OF COMPUTER SCIENCE PAGE 22
 print('count :',count) 
 if(distance >= Full_distance and count == 1):
 audio.full()
 print('writing file')
 file('Full')
 count = 0
 
 print('count :',count) 
 if (Empty_distance <= distance and count == 0):
 print('writing file')
 file('Empty')
 count = 1
