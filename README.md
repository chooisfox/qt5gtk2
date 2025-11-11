# Qt5Gtk2 - GTK+ 2.0 Integration Plugins for Qt5

**Official Home Page:** [https://github.com/trialuser02/qt5gtk2](https://github.com/trialuser02/qt5gtk2)

---

## **Important!**

This is NOT the original repository. Please refer to the official repository for the latest updates and support.

This repository was created just for easier AUR -git package maintenance.

The environment variable `QT_STYLE_OVERRIDE` should be unset before usage.

---

## Requirements

*   GNU Linux or FreeBSD
*   A C++ compiler (`gcc` or `clang`)
*   `cmake` >= 3.16
*   `qtbase` >= 5.7.0 (with private headers installed, e.g., `qtbase5-private-dev` on Debian/Ubuntu)
*   GTK+ 2.0 (`libgtk2.0-dev`)
*   libX11 (`libx11-dev`)

---

## Building and Installation

### Building with CMake (Recommended)

1.  **Configure the Build**
    Create a separate directory for the build and run `cmake` from there.
    ```bash
    mkdir build
    cd build
    cmake ..
    ```
    *   **Tip for System Installation:** To install the plugins into a standard system directory like `/usr`, set the `CMAKE_INSTALL_PREFIX`.
        ```bash
        cmake -DCMAKE_INSTALL_PREFIX=/usr ..
        ```

2.  **Compile the Plugins**
    Once CMake has configured the project, run `make`.
    ```bash
    make
    ```

3.  **Run Tests (Optional)**
    After a successful build, you can run the integrated tests to verify functionality.
    ```bash
    ctest --verbose
    ```

4.  **Install the Plugins**
    Use `make install` to copy the compiled plugins to the installation directory. This usually requires root privileges.
    ```bash
    sudo make install
    ```

### Building with qmake (Legacy Method)

1.  **Build the plugins:**
    ```bash
    qmake
    make
    ```

2.  **Install the plugins (as root):**
    ```bash
    sudo make install
    ```
    *To change the default installation root, run the following command:*
    ```bash
    sudo make install INSTALL_ROOT="custom root"
    ```

---

## Configuration

After installing the plugins using either method, you must configure your system to use them.

1.  **Set the environment variable:**
    Add the following line to your `~/.profile` and re-login:
    ```bash
    export QT_QPA_PLATFORMTHEME=qt5gtk2
    ```
    *Alternatively, for a system-wide setting, create the file `/etc/X11/Xsession.d/100-qt5gtk2` with the following content:*
    ```bash
    export QT_QPA_PLATFORMTHEME=qt5gtk2
    ```

2.  **Apply the changes:**
    Restart your X11 server or log out and log back in for the changes to take effect.

---

## Files and Directories

*   `libqt5gtk2.so` - GTK+2.0 platform plugin
*   `libqt5gtk2-style.so` - GTK+2.0 style plugin
