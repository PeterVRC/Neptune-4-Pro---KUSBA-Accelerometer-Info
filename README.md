# Neptune-4-Pro---KUSBA-Accelerometer-Info
Neptune 4 Pro - KUSBA Accelerometer use

The KUSBA USB Accelerometer can be bought with Klipper firmware already installed into it. I chose the "Anchor Rampon" Firmware version.
It can just be plugged into the Neptune 4 Pro USB port and then only needs minimal configuration changes for it to be used.
The configuration changes tell Klipper that it exists and then it MUST be there or Klipper will fail with an error. This means you
really need to remove the configuration information when it is not being used. There is a way to do this in a very quick and easy manner.
I used a new config file to hold the parameters and that config file is called by the printer.cfg   That means you only need to
comment out ONE line to remove all of the KUSBA parameters.
There is an "inputShaperKUSBA.cfg" file in the repository. Just copy that into the configuration folder. Using Fluidd - the same
place that the printer.cfg is.
In the printer.cfg just add a line at the top where any other includes are listed:

#[include inputShaperKUSBA.cfg]     # Uncomment if you want to run an InputShaper Calibration

Now you only need to uncomment that line when you intend to use the KUSBA Accelerometer.

I also removed any other entries to do with Accelerometers. Loom into the KUSBA config file to see what they look like and
then look through the printer.cfg and remove fields of those same names/layouts.
eg [adxl1345] and [resonance_tester] and [MCU ADXL]

Then plug in the KUSBA and restart Klipper.

Once Klipper is running you can use these commands at the console:

Check Accelerometer:
ACCELEROMETER_QUERY
MEASURE_AXES_NOISE

Run Tests(Manual computation):
TEST_RESONANCES AXIS=X
TEST_RESONANCES AXIS=Y

Run Test ALT (auto computation and addition):
SHAPER_CALIBRATE AXIS=X
SHAPER_CALIBRATE AXIS=Y


You could find that ACCELEROMETER_QUERY does NOT work. That is fine, as it is not really needed anyway.
Run  MEASURE_AXES_NOISE   and you will see results from that. They are not too important either, but at least shows you it is working.

I have just settled for the   SHAPER_CALIBRATE AXIS=X   or   AXIS=Y   to do the task.
These are fully automatic and will do the tests and then save the results to the printer.cfg
You need to mount the Accelerometer for its tests. It actually does not care which way up, or sideways, it is because the
routine will know by one of the Axis having a higher Acceleration due to gravity on that Axis. But you do need to mount it
close to vertical, or horizontal etc.
There is an STL for a universal type mount that I made up for it.  It can be bolted onto the printhead under the front shroud/cover
bolt, for the X Axis test.   And it can be clamped onto the Bed, at the front edge, with a bulldog clip or a peg, for the Y Axis test.

Once those are both completed, you can edit the printer.cfg to comment out the KUSBA include, and unplug and store thee KUSBA until 
ever required again.

The    TEST_RESONANCES AXIS=X  and  Y  produce a data file that can be used to get more details, and possibly a better end result
but i have not tried that yet.  You would have to Goole up some info on what to do with that file to produce a choice/result.


