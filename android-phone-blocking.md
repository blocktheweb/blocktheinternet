## Guide to Locking Down an Android Phone’s Internet and App Access

**Purpose**: To restrict internet access, remove all loopholes for app installation and browsing, and ensure the device is consecrated for disciplined use.

   _“Therefore, come out from among them and be separate, says the Lord. Touch no unclean thing, and I will receive you.”_  
   — 2 Corinthians 6:17

   _“Do not give the devil a foothold.”_  
   — Ephesians 4:27


---

### 🙅️ Web Blocking
*This section is just about preventing some web content from displaying. These settings are not fool proof, as they can be easily removed.*

Use AdAway (requires root or VPN mode) to block garbage, ads, and unnecessary sites altogether.

Note: _This is just a precaution as this vpn content filter can be turned on and off at will!_

To turn off images in your site settings on Android, follow these steps:

#### For Chrome (Android Browser)

1. **Open Google Chrome** on your device.
2. **Tap the three dots** (menu icon) in the top-right corner.
3. Go to **Settings** > **Site settings**.
4. Under **Content**, tap on **Images**.
5. Toggle the switch to **block images**.

This will disable images from loading on all websites in Chrome. Images can be turned on per site in the same settings area as needed.


---
### Clean Install of Android

Its best to start fresh with the operating system—free from any unwanted apps, files, or data that might have been lingering from previous setups. This is especially important when securing a device and locking it down from unnecessary internet or app access.

 Some apps might store encrypted data that could be accessed later, even after they’re removed. For example, hidden VPN apps could have a **vault** of encrypted data. Some of these apps are disguised as working calculators, with a virtual environment hidden behind a key combination. These virtual environments contain browsers and encrypted storage for all sorts of garbage.

---

### Setup (Local ADB Install & Developer Access)

**Step 1: Install ADB on Your Computer**

- Download the Android SDK Platform Tools: [https://developer.android.com/studio/releases/platform-tools](https://developer.android.com/studio/releases/platform-tools)
- Extract and open a terminal (CMD) in that folder.

**Step 2: Enable Developer Options on the Phone**

- Go to **Settings > About Phone**, tap **Build Number** 7 times.
- Now go to **Settings > System > Developer Options**:
  - Turn ON **OEM Unlocking**.
  - Turn ON **USB Debugging**.

---

### Connect to ADB and Access the Phone’s Shell

```bash
adb devices       # Confirm connection
adb shell         # Enter shell
```

---

### 👥 **User Management and Switching**

```bash
pm list users                 # List user IDs
am switch-user 0             # Switch to system user (user 0)
```

### **Set Up a Separate Play Store Account**

- Create a **dedicated Play Store account** just for this device.
- Don't use it on other devices to lock down ability for remote app installation from the web play store.

---

### Enable Parental Controls in the Play Store

1. Go to Play Store > Settings > Family > Parental Controls.
2. Turn it on, create a PIN.
3. Set the **Content Rating** to the lowest (e.g., "Everyone").
4. This blocks apps with other ratings from being installed remotely if somehow that was available.

### 🔒 App Locking & App Hiding (Built-In Settings)

Use the built-in **App Lock** and **App Hide** features to lock down specific internet access apps like Chrome, YouTube, and the Play Store. By allowing these apps to remain installed, link functionality will ask for the privacy pin, mitigating risk where links could be opened in other apps. The Play Store is necessary for other installed apps to function.

- Go to **Settings > Privacy > App Lock**:

  - Set a secure privacy password.
  - Lock down any apps that could provide web access or bypass .
  - Lock key apps: YouTube, Chrome, Play Store

- Then navigate to **Settings > Security > App Hide**:

  - Hide these same apps from the home screen and app drawer.

🔐*The app lock password should be set by a trusted authority. This keeps the apps usable for legitimate system behavior, but invisible and inaccessible.*

---

### 1. **Disable Unknown Sources (for APK Installation)**

This is the primary setting that allows apps to install apps (APKs) outside of the Google Play Store.

- **Step 1**: Go to **Settings > Security** (or **Settings > Apps & notifications** depending on your phone's version).
- **Step 2**: Look for the option **Install unknown apps** or **Allow installation of apps from unknown sources**.
- **Step 3**: Turn off the toggle for any apps that you may have previously allowed to install APKs. Disable this permission for apps like **file managers** or **browser apps** that may have this permission enabled.

**Note**: Some Android devices might group these settings under different categories depending on the brand.

### Block APK Installations and External Content
We can remove this ability in addition to revoking permissions:
```bash
# Disable Package Installer
pm disable-user --user 0 com.google.android.packageinstaller
```

---

### ↺ **Remove Guest & Other Users**

To turn off multiple users through the phone settings:

1. Go to **Settings > System > Multiple Users** (or **Users & Accounts > Users** depending on your Android version).
2. Turn OFF the toggle for **Multiple Users** if available.
3. Delete or remove any existing guest or secondary users.

---

### ❌ Alternative Browsers & Loophole Apps to Disable

Manually  remove apps that have built-in browsers or content access. A lot of times this functionality is found by looking for frames where content is loaded from the internet. These sometimes have links, such as in terms and conditions.
*  T-Life
* FB Messenger
* Lyft
* ...others

---

### 🧷 **Prevent Accidental App Uninstallation or Layout Changes**

In **Settings > Home Screen & Wallpaper**:

- Turn ON **Lock Home Layout** — prevents uninstalling or moving apps.

---

### Disable Access to Settings and Unwanted Apps

⚠️ Caution: Only disable what you don't need and when you're ready.

```
# Disable Google Play Store -- This breaks some apps, so it is better to lock this instead of the below command.
pm uninstall -k --user 0 com.android.vending

# Disable browser -- Its better to lock this instead
pm disable-user --user 0 com.android.chrome

# Disable YouTube -- Its better to lock this instead
pm disable-user --user 0 com.google.android.youtube

# Disable search --  This is a way to search without the browser.
pm disable-user --user 0 com.google.android.googlequicksearchbox

# Remove lense
com.google.ar.lens

# Disable other known loopholes
# Remove Google files app, which may have access to reenable apps.
pm disable-user --user 0 com.google.android.apps.nbu.files


# Disable settings -- this should be done last.
pm disable-user --user 0 com.android.settings
```

---

### Review All Disabled Apps

```bash
adb shell pm list packages -d  # See disabled packages
pm enable <package_name>       # Enable any if needed
```
