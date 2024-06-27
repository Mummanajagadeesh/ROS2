# Installing Ubuntu on VirtualBox

Follow these steps to install Ubuntu 24.04 on VirtualBox.

## Step 1: Download Ubuntu 24.04 ISO Image

Go to [Ubuntu 24.04 Desktop ISO](https://ubuntu.com/download/desktop) and download the 64-bit PC (AMD64) desktop image.

## Step 2: Download VirtualBox Installer

Download VirtualBox from [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads) according to your operating system.

## Step 3: Install VirtualBox

Run the VirtualBox installer and follow the installation steps.

## Create Virtual Machine

1. Open **Oracle VM VirtualBox Manager** and click on **New**.

2. **Name and OS Type:**
   - Name: Ubuntu 22.04 VM
   - Type: Linux
   - Version: Ubuntu (64-bit)

3. **Memory Size (RAM):**
   - Allocate RAM based on your computer's capacity. Recommended: 8 GB if your PC has 16 GB RAM.

4. **Hard Disk:**
   - Select **Create a virtual hard disk now**.
   - Hard Disk File Type: VDI
   - Storage on Physical Hard Disk: **Dynamically Allocated**
   - File Location and Size: **25 GB**

5. Click **Create**.

6. **Configure VM Settings:**
   - Select the VM and go to **Settings > Storage**.
   - Under **Controller: IDE**, click **Empty**.
   - Click the disk icon next to **Optical Drive** and choose the Ubuntu 22.04 ISO file downloaded in Step 1.
   - Click **OK** to save settings.

## Installing Ubuntu on VM

1. Start the VM by clicking **Start**.

2. In the GNU GRUB Menu, select **Try or Install Ubuntu**.

3. Choose **Install Ubuntu** and select your keyboard layout.

4. Select **Minimal Installation** for updates and software.

5. Select **Erase disk and install Ubuntu** for installation type. Click **Install Now** and then **Continue**.

6. Set your username, password, and choose **Log in automatically** if preferred.

7. Click **Continue** to begin installation.


