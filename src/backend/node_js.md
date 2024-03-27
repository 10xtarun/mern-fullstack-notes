# NodeJS

> Node.js is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside of a web browser. It allows developers to use JavaScript to build server-side and networking applications.

The role of Node.js in the backend is to handle server-side logic, manage data, and process requests and responses in web applications. Some key roles of Node.js in the backend include:

1. Server-side JavaScript execution: Node.js allows developers to write server-side code in JavaScript, enabling them to use the same language for both frontend and backend development.

2. Non-blocking I/O: Node.js uses an event-driven, non-blocking I/O model, which makes it lightweight and efficient for handling multiple connections simultaneously. This allows Node.js applications to handle a large number of concurrent requests without blocking the execution of other operations.

3. Building scalable applications: Node.js is well-suited for building scalable and high-performance applications due to its non-blocking I/O model and event-driven architecture. It allows developers to easily scale their applications to handle increasing loads by adding more servers or utilizing clustering techniques.

4. Access to a rich ecosystem of packages: Node.js has a vast ecosystem of open-source packages available through npm (Node Package Manager). These packages provide ready-made solutions for various backend tasks, such as web frameworks, database drivers, authentication libraries, and more, allowing developers to quickly build and extend their applications.

Overall, Node.js plays a crucial role in modern backend development by enabling developers to build fast, scalable, and efficient web applications using JavaScript.

---

## What is Non-blocking I/O?

Let's break down non-blocking I/O in layman's terms:

1. Imagine you're waiting in line at a coffee shop to order your favorite drink. In a traditional, blocking I/O scenario, you'd have to wait until the person in front of you finishes ordering before you can place your order. Everyone has to wait their turn, and if someone takes a long time, it slows down the entire line.

2. Now, let's consider a non-blocking I/O scenario. Instead of waiting in line, you grab a number and can continue doing other things while you wait for your turn. You're not stuck waiting for the person in front of you to finish – you're free to multitask and be productive.

3. In the context of software, non-blocking I/O works similarly. When an application performs an I/O operation (like reading data from a file or fetching data from a database), it doesn't wait for the operation to complete before moving on to the next task. Instead, it continues executing other tasks or processing requests while waiting for the I/O operation to finish.

4. This non-blocking approach allows the application to remain responsive and handle multiple tasks simultaneously without getting stuck waiting for one task to complete. It's like being able to do other things while waiting in line – you're not blocked or slowed down by one task, and you can make better use of your time.

---

## Installation guide for NodeJS

Following are the step-by-step instructions to set up Node.js on both Windows and Linux:

### Windows

1. Download Node.js Installer:
    * Visit the official Node.js website: https://nodejs.org/
    * Download the Windows installer (.msi file) for the LTS (Long-Term Support) version or the latest version.

2. Run Node.js Installer:
    * Once the installer is downloaded, double-click on the .msi file to run it.
    * Follow the prompts in the installer wizard to complete the installation.
    * Accept the license agreement, choose the installation directory, and click "Next" to proceed.

3. Verify Installation:
    * After the installation is complete, open Command Prompt (or PowerShell).
    * Using Command Prompt is recommended. (Better use Linux/Ubuntu)
    
* Type the following command and press Enter:
```bash
node -v
```

* This command should print the installed Node.js version. Similarly, you can check the installed npm version using:
```bash
npm -v
```

### Linux (Ubuntu/Debian)

1. Install Node.js using Package Manager:
    * Open a terminal window.
    * For Ubuntu/Debian-based distributions, use the following commands to install Node.js:
    * These commands will update the package index and install Node.js along with npm (Node Package Manager).

```bash
sudo apt update
sudo apt install nodejs npm
```

2. Verify Installation:
    * After the installation is complete, you can verify Node.js and npm versions by running the following commands in the terminal:

```bash
node -v
npm -v
```

### macOS

1. Install Node.js using Homebrew:
    * Open Terminal, which you can find in the "Utilities" folder within the "Applications" folder, or by searching for it in Spotlight (Cmd + Space, then type "Terminal").
    * Install Homebrew if you haven't already. You can do this by running the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Once Homebrew is installed, you can use it to install Node.js. Run the following command:

```bash
brew install node
```

3. Verify Installation:
    * After the installation is complete, you can verify Node.js and npm versions by running the following commands in Terminal:

```bash
node -v
npm -v
```

> Note: current commands may vary from the commands mentioned above due to updates, check the latest guide available from the internet.

---

## Writing "Hello World" in Node.js

1. Create a New File:
    * Open your preferred text editor (e.g., Visual Studio Code, Sublime Text, or Notepad).
    * Create a new file and name it hello.js.

2. Write the Code:
    * Inside the hello.js file, write the following JavaScript code:

```javascript
console.log("Hello World!");
```

3. Save the File:
    * Save the hello.js file in a location of your choice.


### Running Node.js Code

Now, let's see how to run the Node.js code:

1. Open Terminal/Command Prompt:
    * Open Terminal (macOS/Linux) or Command Prompt (Windows).

2. Navigate to the Directory:
    * Use the cd command to navigate to the directory where you saved the hello.js file. For example:

```bash
cd path/to/directory
```

3. Run the Node.js Code:
    * Once you're in the correct directory, run the following command in Terminal/Command Prompt:

```bash
node hello.js
```

4. View Output:
    * After executing the command, you should see the output "Hello World!" printed in the Terminal/Command Prompt.

### Explanation:

* The console.log() function is used in Node.js to print messages to the console.
In the code console.log("Hello World!");, "Hello World!" is the message that will be printed to the console.

* When you run the command node hello.js, Node.js executes the JavaScript code in the hello.js file, and the output is displayed in the Terminal/Command Prompt.

* That's it! You've successfully written a "Hello World" program in Node.js and learned how to run it. You can now experiment with writing more complex Node.js applications and running them using the same process.

---










