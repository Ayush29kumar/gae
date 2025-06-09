# gae

# Google App Engine Flask Application Setup Guide

This guide provides step-by-step instructions for creating and deploying a Flask application to Google App Engine on Ubuntu/Debian systems.

## Prerequisites

- Ubuntu/Debian operating system
- Administrative access (sudo privileges)
- Active Google Cloud Platform account
- Internet connection

## Step 1: System Setup and Dependencies

### Install Python and Package Manager
Update your system package list and install Python with pip package manager:

```bash
sudo apt update
sudo apt install python3 python3-pip
```

### Upgrade pip and Install Virtual Environment Tool
Ensure you have the latest version of pip and install virtualenv for creating isolated Python environments:

```bash
pip3 install --upgrade pip
pip3 install virtualenv
```

### Install Google Cloud SDK
Download and install the Google Cloud SDK using the interactive installer:

```bash
curl https://sdk.cloud.google.com | bash
exec -l $SHELL
```

After installation, initialize the Google Cloud configuration:

```bash
gcloud init
```

Follow the prompts to authenticate with your Google account and select your project.

## Step 2: Project Structure Setup

### Create Application Directory
Create a dedicated directory for your Google App Engine application:

```bash
mkdir gae-hello-world
cd gae-hello-world
```

### Create and Activate Virtual Environment
Set up an isolated Python environment for your project dependencies:

```bash
virtualenv venv
source venv/bin/activate
```

**Note:** You should see `(venv)` in your terminal prompt, indicating the virtual environment is active.

## Step 3: Application Development

### Create the Main Application File
Create the primary Flask application file (`main.py`):

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World from GAE!'

if __name__ == '__main__':
    app.run(host='127.0.0.1', port=8080, debug=True)
```

### Define Project Dependencies
Create a requirements file (`requirements.txt`) to specify your application dependencies:

```
Flask==2.3.2
```

### Install Dependencies
Install the required packages using pip:

```bash
pip install -r requirements.txt
```

## Step 4: Google App Engine Configuration

### Create App Engine Configuration File
Create the `app.yaml` configuration file for Google App Engine deployment:

```yaml
runtime: python310
entrypoint: gunicorn -b :$PORT main:app

handlers:
- url: /.*
  script: auto
```

### Install Production Web Server
Install Gunicorn, which will serve your application in the Google App Engine environment:

```bash
pip install gunicorn
```

## Step 5: Local Testing

### Run the Application Locally
Test your application on your local development environment:

```bash
python main.py
```

Your application will be accessible at `http://127.0.0.1:8080` in your web browser.

## Project Structure Summary

After completing these steps, your project directory should contain the following files:

```
gae-hello-world/
├── venv/               # Virtual environment directory
├── main.py            # Flask application code
├── requirements.txt   # Python dependencies
└── app.yaml          # Google App Engine configuration
```

## Next Steps

Once you have successfully tested your application locally, you can deploy it to Google App Engine using:

```bash
gcloud app deploy
```

This command will upload your application to Google Cloud Platform and make it available at your assigned App Engine URL.

## Troubleshooting

**Virtual Environment Issues:** If you encounter permissions errors, ensure you have activated the virtual environment with `source venv/bin/activate`.

**Google Cloud Authentication:** If `gcloud init` fails, verify your internet connection and ensure you have a valid Google Cloud Platform account.

**Local Testing Problems:** Check that port 8080 is not being used by another application, and verify that Flask is properly installed in your virtual environment.
