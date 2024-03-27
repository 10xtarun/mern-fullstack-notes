# What is npm?

> npm stands for Node Package Manager. In simple terms, npm is a tool that helps developers manage and share JavaScript code packages or libraries.

Here's how npm works:

1. Package Management:
    * npm allows developers to easily install, manage, and update JavaScript packages or libraries (also known as "packages" or "modules") for their projects. These packages contain reusable code that can perform specific tasks or provide functionality, such as handling HTTP requests, working with databases, or implementing user interfaces.

2. Dependency Management:
    * When a developer installs a package using npm, it automatically handles any dependencies required by that package. This means that npm will also download and install any other packages that the main package depends on, ensuring that all necessary code is available for the project to function correctly.

3. Version Control:
    * npm also provides version control for packages. Each package has a version number, and developers can specify which version of a package they want to install in their project. This allows developers to ensure that their projects use the correct version of a package and avoid compatibility issues with newer or older versions.

4. Publishing and Sharing:
    * Developers can publish their own JavaScript packages to the npm registry, making them available for other developers to use in their projects. This allows developers to share their code with the community and contribute to the ecosystem of open-source JavaScript libraries.

> In summary, npm is a powerful tool that simplifies the process of managing, installing, and sharing JavaScript code packages or libraries. It helps developers streamline their development workflow and leverage the vast ecosystem of available packages to build robust and feature-rich applications.

## How to use NPM in NodeJS Project?

To use npm in a Node.js project, follow these steps:

1. Initialize a Node.js project:
    * Open your terminal or command prompt.
    * Navigate to the directory where you want to create your Node.js project.
    * Run the following command to initialize a new Node.js project:

```bash
npm init -y
```

This command will create a package.json file in your project directory, which will store information about your project and its dependencies.

2. Install npm packages:
    * To install npm packages for your project, use the npm install command followed by the name of the package you want to install.
    * For example, to install the Express.js framework, run the following command:

```bash
npm install express
```

This command will download and install the Express.js package and its dependencies into your project's node_modules directory.

3. Save dependencies to package.json:
    * By default, npm will save installed packages as dependencies in your package.json file.
    * If you want to save a package as a development dependency (e.g., for testing or development purposes), use the --save-dev flag.
    * For example, to install the mocha testing framework as a development dependency, run the following command:

```bash
npm install mocha --save-dev
```

4. Use installed packages in your code:
    * Once the packages are installed, you can use them in your Node.js code.
    * For example, if you installed Express.js, you can create a new Express application in a JavaScript file like this:
```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

5. Run your Node.js project:
    * After installing npm packages and writing your code, you can run your Node.js project using the node command followed by the filename of your main JavaScript file.
    * For example, if your main file is named app.js, you can run it with the following command:

```bash
node app.js
```

> That's it! You've successfully used npm in your Node.js project to install packages and manage dependencies. You can now continue building and developing your Node.js application using npm.


> Note: `npm init` by running this command, npm will ask few straightforward question regarding the project details.

---









