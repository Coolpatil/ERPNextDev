Weighbridge Weight Reader for ERPNext
This project provides a JavaScript integration to read weight data from a serial weighbridge scale and display it in an ERPNext field (weighbridge_weight). It uses the Web Serial API to communicate with the scale COM port and continually updates the weight on the form.

Features
Automatically detects and stores selected COM port for future connections

Continuously reads weight packets from the serial scale

Parses raw weight data encapsulated between STX (0x02) and ETX (0x03)

Displays weight in the ERPNext form field weighbridge_weight

Allows selecting a new COM port via a custom button in ERPNext form

How it works
COM Port Selection and Storage
On form refresh, the script attempts to reopen the last used COM port saved in localStorage. If unavailable, it prompts the user to select a COM port and saves this info for subsequent sessions.

Reading Serial Data
The script reads serial data continuously from the scale. It expects the scale to send weight messages framed between STX ('\u0002') and ETX ('\u0003') characters, e.g., +017680013.

Parsing Raw Weight Values
Once a packet is received, the script extracts the signed numeric value. This raw number represents the weight with a certain scale factor applied by the weighbridge hardware.

Scaling Raw Weight
The raw number is converted to a human-readable weight by dividing by a scale divisor. This divisor depends on your specific weighbridge model and configuration.

Customizing Scale Division
By default, the script divides the raw scale reading by 100 to convert it to the correct weight units. This value can be changed to suit your scale's output precision.

Locate this line in the code:

js
const weight = sign * (rawNumber / 100);
If your scale outputs weight in grams, divide by 1000 to convert to kilograms.

If your raw number is already in kilograms, use a divisor of 1 (i.e., no division).

Adjust the divisor as needed; common values are 1, 10, 100, or 1000.

For example, if your scale outputs 2304000 to represent 2304.000 kg, use:

js
const weight = sign * (rawNumber / 1000);
If it outputs 848000 for 8480.00 kg, use:

js
const weight = sign * (rawNumber / 100);
Setup and Usage
Add the script to your ERPNext weighbridge form client script or custom app.

On loading the form, either reuses the saved COM port or prompts to select a COM port.

The weight field updates live with values read from the scale.

Use the "Select COM Port" button to change the port if needed.

Close the form to properly release the port.

Troubleshooting
Ensure your browser supports the Web Serial API (e.g., Chrome).

Verify the baud rate and serial settings match your weighbridge scale's configuration.

Use the browser console log to view raw values for debugging (console.log("Raw number from scale:", rawNumber);).

Adjust the division factor based on the raw values observed and expected real weight.
