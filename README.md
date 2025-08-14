Creative Story & Scene Generator
This project is a full-stack Django web application developed for the IISc Aerospace Engineering Internship creative assignment. It leverages the LangChain framework and generative AI models to transform a single user prompt into a rich, multi-modal narrative experience, including a short story, detailed character and scene descriptions, and a final, programmatically composited image.

Core Features
Multi-Modal Generation: Produces a short story, character description, and background description from a single text prompt.

AI-Powered Image Generation: Uses the generated descriptions to create two separate images (a character and a background) using the Stable Diffusion XL model.

Automated Scene Composition: Intelligently removes the background from the character image and composites it onto the scene image to create a unified, coherent illustration.

Futuristic Web Interface: A modern, responsive UI built with Django and enhanced with CSS animations to provide an engaging user experience.

Modular Service-Oriented Architecture: The backend logic is decoupled from the web layer into distinct services for text generation, image generation, and orchestration, ensuring the code is maintainable, testable, and robust.

Technology Stack
Category

Technology / Model

Purpose & Justification

Backend Framework

Django 4.2+

Provides a robust and scalable "batteries-included" foundation for the web application, handling URL routing, request/response cycles, and template rendering.

AI Orchestration

LangChain

Manages the complex, multi-step workflow of interacting with AI models. Its components are essential for creating modular and reliable chains that handle the entire generative process.

Language Model

Google Gemini (via langchain-google-genai)

Chosen for its advanced narrative capabilities and its ability to generate structured JSON output, satisfying the project's "free tools" constraint via its API.

Image Model

stabilityai/stable-diffusion-xl-base-1.0

A powerful, high-resolution, open-source text-to-image model. It is distributed as a complete diffusers pipeline on Hugging Face, which simplifies loading and running the model locally.

Image Generation

Hugging Face diffusers

The standard library for interacting with diffusion models in Python. It provides the tools to load and run the Stable Diffusion model locally on a GPU.

Image Processing

Pillow (PIL)

A versatile image processing library used for the critical task of compositing the final scene, including removing the character's background and pasting it onto the scene image.

Environment Mgmt.

Python venv

The standard Python tool for creating isolated project environments, ensuring that dependencies are managed cleanly and the project is fully reproducible.

Dependency Mgmt.

pip and requirements.txt

Provides a declarative and reproducible way to manage all project dependencies. A single command is sufficient to install all necessary packages.

🚨 URGENT: API Key Security Protocol
A critical security vulnerability was identified: a Google Gemini API key was publicly exposed. This key must be considered compromised.

Immediate Action Required:

Revoke the Key: Go to the Google AI Studio API Key Console. Find the exposed key (...KaA4) and delete it immediately.

Generate a New Key: Create a new, confidential API key for this project.

Use Secure Storage: The project is set up to use a .env file for this purpose. Never hard-code secrets directly in your code.

🚀 Setup and Local Deployment Guide
Follow these steps precisely to get the project running on your local machine.

Prerequisites
Hardware: A CUDA-enabled NVIDIA GPU with at least 12 GB of VRAM is strongly recommended. The image model is computationally intensive and will likely fail on a CPU or a less powerful GPU.

Software: Python 3.10 or newer.

Step-by-Step Installation
Clone the Repository (if applicable)
If you are using Git, clone the repository. Otherwise, ensure all the project files are in a single root folder.

Create and Activate a Virtual Environment
This is a critical step to isolate project dependencies. Open your terminal in the project's root directory.

On Windows (PowerShell):

# Create the environment
python -m venv venv

# Activate the environment
.\venv\Scripts\activate

On macOS/Linux:

# Create the environment
python3 -m venv venv

# Activate the environment
source venv/bin/activate

Your terminal prompt should now be prefixed with (venv).

Install Dependencies
With your virtual environment active, install all required packages from requirements.txt. This will take several minutes.

pip install -r requirements.txt

Configure Environment Variables

Create a file named .env in the project root directory.

Open the .env file and add your new, secure Google Gemini API key:

GOOGLE_API_KEY="YOUR_NEW_API_KEY_HERE"

Initialize the Database
Run the Django migrate command to set up the local SQLite database.

python manage.py migrate

Start the Development Server
You're ready to launch the application!

python manage.py runserver

Access the Application
Open your web browser and navigate to http://127.0.0.1:8000/.

IMPORTANT NOTE: The first time you submit a prompt, the application will hang for several minutes. This is expected behavior as the system downloads the multi-gigabyte Stable Diffusion model. Subsequent image generations will be significantly faster.

📁 Project Structure
The project follows a standard Django layout, enhanced with a services directory to enforce modularity and separation of concerns.

IISCPROJECT3/
├── creative_story_generator/  # Django project configuration
│   ├── settings.py            # Main project settings
│   ├── urls.py                # Root URL configuration
│   └── ...
├── story_app/                 # The core Django application
│   ├── migrations/
│   ├── static/                # CSS and other static files
│   │   └── story_app/css/style.css
│   ├── templates/             # HTML templates
│   │   └── story_app/index.html
│   ├── services/              # CORE LOGIC: All AI operations
│   │   ├── __init__.py
│   │   ├── text_generation_service.py
│   │   ├── image_generation_service.py
│   │   └── orchestration_service.py
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py                # App-specific URL patterns
│   └── views.py               # Handles web requests and renders templates
├── .env                       # Stores secret API keys (MUST NOT be committed to Git)
├── manage.py                  # Django's command-line utility
└── requirements.txt           # Lists all Python dependencies
