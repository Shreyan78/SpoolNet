# SpoolNet
Automated Filament Tracking combining basic sensors, pcbs, and webhook functionaility alongside a web UI to facilitate easy FDM material management


# READ ME
Still a WIP page!

## See the system in action!
[![Watch the demo](https://img.youtube.com/vi/H7J6-Q6CeBQ/maxresdefault.jpg)](https://youtu.be/H7J6-Q6CeBQ)

## Features

- Automatic Filament tracking
- NFC spool identification
- Webhook-based server communication
- Mobile App

## Hardware
WIP

## How It Works

Spoolnet is a concept which utilizes the above mentioned to create a workflow that goes as follows:

Scan filament to hub -> Load and use filament normally -> Automatic updates being sent to server

Spoolnet can track filament extrudes/retracts and works on any printer provided a suitable mount is modeled and produced.

The basic idea involved a PN532 NFC sensor in the hub alongside a nfc sticker on each roll of filament to allow users to scan filament to the hub, allowing the system to understand what filament is being used and send proper information to the server regarding filament location and filament usage details. The concept is that all filament in a workplace would have a sticker, and filament would be scanned to the hub prior to printing, and would only need to be done once (when filament is initially loaded).

## Architecture

The system leverages 3 main software point:
-Mobile app for filament setup + easy scanning of rolls to track current filament remaining
-Lightweight server for webhooks and runs all processes in the background
-Web UI for managing and viewing material database


