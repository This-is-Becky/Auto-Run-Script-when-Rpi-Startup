# Auto Run-Script-when-Rpi-Startup
In **Raspberry Pi Linux** systems, **autoscripts** refer to custom scripts or programs that are automatically executed during system events, such as Startup. 

The tool used to control these scripts is `systemctl`, which allows users to define, enable, and manage services that run automatically. This is especially useful for automating tasks such as:
- Starting sensor monitoring or data logging scripts
- Start recording when Vehicle-mounted camera reboot
- Auto connect to WiFi when restart
  
## Step1. Prepare the script(here using python file as example)
- stored in the specific desire direcotry
Example:
```
/home/pi/cam_record.py
```
## Step2. Create a Systemd Service File
Type 
```
sudo nano /lib/systemd/system/autoscript.service
```
## Step3. Define the Service Configuration
Add
```
[Unit]
Description=Start Script on Boot
After=network.target
 
[Service]
ExecStart=/usr/bin/python3 /home/pi/Downloads/cam_record.py
WorkingDirectory=/home/pi/Downloads
StandardOutput=inherit
StandardError=inherit
Restart=always
User=pi
 
[Install]
WantedBy=multi-user.target
```
- Press `Ctrl+O` to save, then press `Enter`
- Press ` Ctrl+X` to exit

## Step4. Reload Systemd
` sudo systemctl daemon-reload`

## Step5. Enable/ Start the function
`sudo systemctl enable autoscript.service`
`sudo systemctl start autoscript.service`

# Note:
- To check the **Status**: `sudo systemctl status autoscript.service`
- To **Stop** the function: `sudo systemctl stop autoscript.service`
- To **Disable** the function: `sudo systemctl disable autoscript.service`
- To **Remove** the function: `sudo rm /lib/systemd/system/autoscript.service`
