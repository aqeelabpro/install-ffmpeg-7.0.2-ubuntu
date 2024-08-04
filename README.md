# Install ffmpeg v7.0.2 on Ubuntu
create a file called install_ffmpeg.sh or whatever name you want and paste in
```
#!/bin/bash

# Define variables
FFMPEG_VERSION="7.0.2"
TARBALL="ffmpeg-$FFMPEG_VERSION.tar.xz"
DOWNLOAD_URL="https://ffmpeg.org/releases/$TARBALL"
INSTALL_DIR="/usr/local"

# Function to check for command existence
command_exists() {
    command -v "$1" >/dev/null 2>&1
}

# Update and install necessary dependencies
echo "Updating package list and installing dependencies..."
sudo apt update
sudo apt install -y build-essential yasm pkg-config libavcodec-dev libavformat-dev libswscale-dev libavfilter-dev libavdevice-dev wget

# Download the tarball if it doesn't exist
if [ ! -f "$TARBALL" ]; then
    echo "Downloading FFmpeg $FFMPEG_VERSION..."
    wget "$DOWNLOAD_URL"
else
    echo "Tarball $TARBALL already exists."
fi

# Extract the tarball
echo "Extracting $TARBALL..."
tar -xf "$TARBALL"

# Navigate to the extracted directory
cd "ffmpeg-$FFMPEG_VERSION" || { echo "Failed to enter directory ffmpeg-$FFMPEG_VERSION"; exit 1; }

# Configure the build
echo "Configuring the build..."
./configure --prefix="$INSTALL_DIR" --enable-gpl --enable-libx264

# Compile FFmpeg
echo "Compiling FFmpeg..."
make

# Install FFmpeg
echo "Installing FFmpeg..."
sudo make install

# Verify installation
if command_exists ffmpeg; then
    echo "FFmpeg installed successfully."
    ffmpeg -version
else
    echo "FFmpeg installation failed."
    exit 1
fi

echo "FFmpeg installation script completed."

```

# Instructions To Install:
Save the script:
Save the above script into a file named ```install_ffmpeg.sh```

Make the script executable:
Open a terminal and navigate to the directory where the script is saved. Then, make the script executable using the following command:

```chmod +x install_ffmpeg.sh```
Run the script:
Execute the script with superuser privileges to install FFmpeg:

```sudo ./install_ffmpeg.sh```
This script will automate the entire process, making it easier for you to install FFmpeg on your system.
