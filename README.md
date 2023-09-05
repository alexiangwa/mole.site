# mole.site
deploy the mole website


#!/bin/bash

# Switch to the superuser (root) to execute subsequent commands with elevated privileges.
sudo su

# Update the system packages to the latest versions.
yum -y update

# Install the Apache HTTP server (httpd) package with automatic "yes" response to prompts.
yum install httpd -y

# Change the current directory to the default web server root directory.
cd /var/www/html

# Download the web application source code from a GitHub repository.
wget https://github.com/alexiangwa/mole.site/archive/refs/heads/main.zip

# Unzip the downloaded ZIP archive to access its contents.
unzip main.zip

# Change the current directory to the directory created after unzipping the main archive.
cd mole.site-main/

# Unzip another ZIP archive with a filename containing spaces and special characters.
# Backslashes are used to escape these characters.
unzip mole\ \(2\).zip

# Copy the contents of the extracted `mole-main/` directory to the web server's root directory,
# effectively deploying the web application.
cp -r mole-main/* /var/www/html

# Clean up by removing the downloaded ZIP files.
rm -rf mole\ \(2\).zip main.zip

# Clean up by removing the extracted directories and the remaining ZIP file.
rm -rf mole.site-main/ main.zip

# Enable the Apache HTTP server to start automatically at boot.
systemctl enable httpd

# Start the Apache HTTP server immediately.
systemctl start httpd
