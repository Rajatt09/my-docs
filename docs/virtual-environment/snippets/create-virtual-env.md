# Creating a Virtual Environment

## Python

To create a virtual environment in Python, follow these steps:

1. **Install `virtualenv`** (if not already installed): `pip install virtualenv`

2. **Navigate to your project directory**: `cd your-project-directory`

3. **Create a virtual environment**: `virtualenv venv`

4. **Activate the virtual environment**:

   - On Windows:
     ```
     venv\Scripts\activate
     ```
   - On macOS/Linux:
     ```
     source venv/bin/activate
     ```

5. **Deactivate the virtual environment** when done:
   ```
   deactivate
   ```

## Node.js

To create a virtual environment in Node.js, you can use `nvm` (Node Version Manager):

1. **Install `nvm`** (if not already installed):
   Follow the installation instructions from the [nvm repository](https://github.com/nvm-sh/nvm).

2. **Install a specific Node.js version**: `nvm install <version>`

3. **Use the installed version**: `nvm use <version>`

4. **Deactivate the version**: `nvm deactivate`
