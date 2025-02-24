# Elegoo Saturn 4 Ultra Camera Viewer (PyQt Version)

A standalone desktop application to view the camera feed from your Elegoo Saturn 4 Ultra 3D printer using PyQt for improved cross-platform compatibility.

## Features

- **Native desktop interface** - Robust PyQt-based GUI that works well on all platforms
- **Automatic dependency installation** - Required packages are installed on first run
- **Recent printer history** - Remembers recently used printer IP addresses
- **Real-time video display** with timestamp overlay
- **Responsive interface** that properly scales with window resizing
- **Single-file solution** - Just run the Python script and go!

## Quick Start - Basic Usage

### macOS

1. Download the `rtsp_viewer_qt.py` file
2. Open Terminal
3. Navigate to the folder containing the file:
   ```
   cd /path/to/folder
   ```
4. Run the script:
   ```
   python3 rtsp_viewer_qt.py
   ```

### Windows

1. Download the `rtsp_viewer_qt.py` file
2. Right-click the file and select "Open with Python" or:
3. Open Command Prompt and run:
   ```
   python path\to\rtsp_viewer_qt.py
   ```

### Linux

1. Download the `rtsp_viewer_qt.py` file
2. Open Terminal and run:
   ```
   python3 rtsp_viewer_qt.py
   ```

## Creating a macOS Application (No Terminal Required)

You can convert the Python script into a proper macOS application that can be launched by clicking an icon in Finder:

### Option 1: Using py2app (Recommended)

1. Install py2app:
   ```
   pip3 install py2app
   ```

2. Create a setup.py file in the same directory as your rtsp_viewer_qt.py:
   ```python
   from setuptools import setup

   APP = ['rtsp_viewer_qt.py']
   OPTIONS = {
       'argv_emulation': True,
       'packages': ['PyQt5', 'cv2', 'numpy'],
       'iconfile': 'icon.icns',  # Optional: Path to your icon file
       'plist': {
           'CFBundleName': 'Elegoo Printer Camera',
           'CFBundleDisplayName': 'Elegoo Printer Camera',
           'CFBundleIdentifier': 'com.yourdomain.elegoocamera',
           'CFBundleVersion': '1.0.1',
           'CFBundleShortVersionString': '1.0.1',
           'NSHumanReadableCopyright': 'Your Name',
       }
   }

   setup(
       app=APP,
       name='Elegoo Printer Camera',
       options={'py2app': OPTIONS},
       setup_requires=['py2app'],
   )
   ```

3. Build the application:
   ```
   python3 setup.py py2app
   ```

4. Find your application in the `dist` folder. You can drag it to your Applications folder.

### Option 2: Using Script Editor (Simple Approach)

1. Open Script Editor (found in Applications > Utilities)
2. Paste the following AppleScript:
   ```applescript
   do shell script "python3 " & quoted form of "/path/to/your/rtsp_viewer_qt.py"
   ```
   Replace `/path/to/your/rtsp_viewer_qt.py` with the actual path to your script.

3. Save as Application:
   - Choose File > Save
   - Name your application (e.g., "Elegoo Camera Viewer")
   - Set File Format to "Application"
   - Save to your Applications folder or desktop

4. (Optional) Add an icon:
   - In Finder, locate your saved application
   - Right-click and select "Get Info"
   - Drag an image file to the icon in the top-left corner of the info window

### Option 3: Using Automator

1. Open Automator (found in the Applications folder)
2. Create a new Application
3. Add a "Run Shell Script" action
4. Enter: `python3 /path/to/your/rtsp_viewer_qt.py`
5. Save the application to your Applications folder or desktop

## Usage

1. When you start the application, you'll see a window with a connection field at the top
2. Enter your Elegoo Saturn 4 Ultra printer's IP address or select a previously used one from the dropdown
3. Click "Connect" to view the camera feed
4. The video will appear in the main window area
5. To disconnect, click the "Disconnect" button

### Command Line Options

If you're running from the terminal, you can specify a printer IP address to connect immediately:
```
python3 rtsp_viewer_qt.py --ip 192.168.1.100
```

## How It Works

The application:
1. Uses OpenCV to connect to your printer's RTSP stream (rtsp://your-ip:554/video)
2. Continuously captures frames from the stream
3. Processes and displays the frames using PyQt's high-performance graphics system
4. Adds timestamp and source information overlay to the video

## Troubleshooting

If you encounter issues:

1. **Connection problems:**
   - Ensure your printer is turned on and connected to your network
   - Verify the IP address is correct
   - Check that your printer's camera is enabled

2. **Display issues:**
   - Make sure you have a compatible graphics driver
   - Try running with a different Qt style: add `--style Windows` or `--style Fusion` to the command

3. **Application bundle issues:**
   - If the app bundle doesn't work, make sure all dependencies are correctly installed
   - You may need to install dependencies system-wide using:
     ```
     pip3 install --user PyQt5 opencv-python numpy
     ```

## License

This project is available under the MIT License.
