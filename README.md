# NP
Nachiket's Projects
ERPNext Weighing Scale Client Script
This client-side JavaScript script enables continuous, real-time reading of weight data from a serial-connected weighing scale directly into an ERPNext DocType form (e.g., "Weighing Scale").
It utilizes the browser's Web Serial API—supported by Chrome and Edge—to communicate with scales connected via USB/COM ports.

Features
User-friendly COM Port Selection:
Users can select and permanently save a serial port ("COM Port") for their weighing scale using a button. Port info is stored in browser localStorage, minimizing extra permission prompts.

Live Weight Updates:
Continuously reads serial data as long as the form is open and displays the latest weight value in the weight field of the ERPNext form without needing repeated button presses.

Robust Data Parsing:
Handles streaming data by buffering and extracting numeric weight values—compatible with most common scale output formats.

Resource Management:
Serial port and stream reader are safely closed and cleaned up when the form is closed or a new port is selected.

Error Handling:
Alerts users to failures in reading, parsing, or connecting to the scale for easier troubleshooting.

How to Use
Paste the script into ERPNext’s Client Script for your “Weighing Scale” DocType.

Open the form in Chrome or Edge.

Click "Select COM Port" to grant serial port access if not already set.

When the form opens, weight readings will appear automatically in the weight field—no need to click "Read Weight" each time.

Close the form or reload to stop reading and release the port.

Technical notes
Script stores selected port info in localStorage and attempts reuse for seamless operation.

Designed for ERPNext v13+, with compatibility for v15.

Baud rate is set to 9600—adjust in code for different scale hardware.

Reading/parsing is robust against partial/fragmented serial transmissions.

Requirements
ERPNext DocType with a field named weight (type: Float/Data).

Chrome or Edge (Web Serial API support).

User permission for serial port access.

This script enables seamless, live weight display from a physical scale into ERPNext, ideal for manufacturing, logistics, or inventory workflows requiring precise, real-time measurement logging.
