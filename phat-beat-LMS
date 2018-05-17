#!/usr/bin/env python
import RPi.GPIO as GPIO
import time
from pylms.server import Server
from pylms.player import Player

sc = Server(hostname="192.168.2.109", port=9090, username="", password="")
sc.connect()

#print "Logged in: %s" % sc.logged_in
#print "Version: %s" % sc.get_version()

sq = sc.get_player("b8:27:eb:3c:1b:be")

GPIO.setmode(GPIO.BCM)

GPIO.setup(5, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(6, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(13, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(26, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(12, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(16, GPIO.IN, pull_up_down=GPIO.PUD_UP)

def myCallback(channel):
  if channel == 6:
    sq.toggle()
  if channel == 12:
    isOn = sq.get_power_state()
    if isOn:
        sq.set_power_state(0)
    else:
        sq.set_power_state(1)
  if channel == 5:
    sq.next()
  if channel == 13:
    sq.prev()
  if channel == 16:
    sq.volume_up(amount=5)
  if channel == 26:
    sq.volume_down(amount=5)

GPIO.add_event_detect(5, GPIO.FALLING, callback=myCallback, bouncetime=200)
GPIO.add_event_detect(6, GPIO.FALLING, callback=myCallback, bouncetime=200)
GPIO.add_event_detect(13, GPIO.FALLING, callback=myCallback, bouncetime=200)
GPIO.add_event_detect(26, GPIO.FALLING, callback=myCallback, bouncetime=200)
GPIO.add_event_detect(12, GPIO.FALLING, callback=myCallback, bouncetime=50) 
GPIO.add_event_detect(16, GPIO.FALLING, callback=myCallback, bouncetime=50)

while True:
	pass
time.sleep(0.2)
