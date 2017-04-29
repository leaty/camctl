#!/usr/bin/env python3

import usb.core
import usb.util
import argparse
import sys

class CAM:
	def __init__(self, vid, pid):
		self.vendor = vid
		self.product = pid
		self._find()

	def _find(self):
		devices = list(usb.core.find(idVendor=vid, idProduct=pid, find_all=True))
		self.device = devices[0]

	def claim(self):
		if self.device.is_kernel_driver_active(0):
			print('Detaching kernel driver..')
			self.device.detach_kernel_driver(0)

	def declaim(self):
		if not self.device.is_kernel_driver_active(0):
			print('Reattaching kernel driver..')
			usb.util.dispose_resources(self.device)
			self.device.attach_kernel_driver(0)

	def fan(self, speed):
		print('Setting fan speed to {}..'.format(speed))
		self.device.write(1, [2, 77, 0, 0, speed, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

	def pump(self, speed):
		print('Setting pump speed to {}..'.format(speed))
		self.device.write(1, [2, 77, 64, 0, speed, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

# Change these if they differ from yours
# See lsusb (e.g. Bus 001 Device 004: ID 1e71:170e NZXT)
vid = 0x1e71
pid = 0x170e

parser = argparse.ArgumentParser()
parser.add_argument('-f', '--fanspeed', dest='fanspeed', type=int, default=None, help="Fan speed between 10 - 100")
parser.add_argument('-p', '--pumpspeed', dest='pumpspeed', type=int, default=None, help="Pump speed between 10 - 100")
args = parser.parse_args()

if args.fanspeed:
	if args.fanspeed < 10 or args.fanspeed > 100:
		print('Fan speed must be between 10 - 100')
		sys.exit(0)
if args.pumpspeed:
	if args.pumpspeed < 10 or args.pumpspeed > 100:
		print('Pump speed must be between 10 - 100')
		sys.exit(0)
try:
	cam = CAM(vid, pid)
	cam.claim()
	if args.fanspeed:
		cam.fan(args.fanspeed)
	if args.pumpspeed:
		cam.pump(args.pumpspeed)
	cam.declaim()
except Exception as e:
	cam.declaim()
	raise(e)
