# n8n Local Installation Guide

This guide provides detailed instructions to install and run n8n on your Windows or macOS computer.

---

## Node.js Platform

Node.js is a runtime environment that allows your computer to execute JavaScript code outside of a web browser. Since n8n is built on Node.js, it must be installed on your system for n8n to function correctly.

---

## Download Node.js

Visit the official Node.js website at [https://nodejs.org/en/download/](https://nodejs.org/en/download/) and download the Long-Term Support (LTS) version suitable for your operating system — either Windows or macOS.

---

## Install Node.js

* **Windows:**
  Locate the downloaded `.msi` installer file in your Downloads folder. Double-click to launch the installer and follow the prompts, accepting default options until the installation completes.

* **macOS:**
  Locate the downloaded `.pkg` installer file in your Downloads folder. Double-click it to open the installer, then follow the on-screen instructions to complete the installation.

---

## Node Package Manager (npm)

npm is the package manager that comes with Node.js. It helps install and manage software packages like n8n easily.

---

## Verify Node.js and npm Installation

Open the terminal or command prompt:

* **Windows:** Press `Win + R`, type `cmd`, and press Enter to open the Command Prompt.
* **macOS:** Open Terminal via Applications > Utilities or by using Spotlight search.

Run the following commands, pressing Enter after each:

```
node -v
```

This command displays the installed Node.js version (for example, `v18.16.0`).

```
npm -v
```

This command displays the installed npm version.

If both commands return version numbers, Node.js and npm are installed correctly.

---

## Install n8n Globally

Using npm, install n8n globally by running:

```
npm install -g n8n
```

The process may take several minutes as npm downloads and configures n8n and its dependencies. Wait until the installation completes before proceeding.

---

## Start n8n

Launch n8n by running:

```
n8n
```

Upon successful startup, the terminal will display a message similar to:

```
n8n ready on http://localhost:5678
```

This indicates that n8n is running locally and ready for use.

---

## Access n8n Web Interface

Open your preferred web browser and navigate to:

```
http://localhost:5678
```

The n8n graphical interface will load, allowing you to create and manage your workflows.

---

## Stop n8n

To stop the n8n server, return to the terminal where it is running and press:

```
Ctrl + C
```

This command will safely terminate the n8n process and return you to the command prompt.

---

## Additional Notes

* Keep the terminal window open to maintain the n8n server active.
* To restart n8n, open a new terminal window and execute the `n8n` command again.
* For assistance with running n8n as a background service or configuring it to start automatically, please seek further guidance.
