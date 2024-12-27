#!/bin/bash

# Check if a repository URL is provided
if [ -z "$1" ]; then
    echo "Usage: pyget <repo_url>"
    exit 1
fi

# Variables
REPO_URL="$1"
REPO_NAME=$(basename "$REPO_URL" .git)
HOME_DIR="$HOME/tools"

# Try installing with pipx directly from the URL
echo "Attempting to install with pipx..."
if pipx install git+"$REPO_URL" --include-deps; then
    echo "Tool installed successfully with pipx."
    exit 0
else
    echo "pipx installation failed. Proceeding with repository cloning."
fi

# Clone the repository if pipx fails
cd "$HOME_DIR" || exit
if [ -d "$REPO_NAME" ]; then
    echo "Repository '$REPO_NAME' already exists. Skipping cloning."
else
    if git clone "$REPO_URL"; then
        echo "Repository cloned successfully."
    else
        echo "Failed to clone repository. Exiting."
        exit 1
    fi
fi

# Navigate to the repository
cd "$REPO_NAME" || exit


    # Create a virtual environment if not already present
    if [ ! -d "venv" ]; then
        if python3 -m venv venv; then
            echo "Virtual environment created successfully."
        else
            echo "Failed to create virtual environment. Exiting."
            exit 1
        fi
    else
        echo "Virtual environment already exists. Skipping creation."
    fi

    # Activate the virtual environment
    source venv/bin/activate

    # Install requirements if requirements.txt exists
    if [ -f "requirements.txt" ]; then
        if pip install -r requirements.txt; then
            echo "Requirements installed successfully."
        else
            echo "Failed to install requirements. Exiting."
            deactivate
            exit 1
        fi
    else
        echo "No requirements.txt file found. Skipping installation."
    fi

    # Deactivate the virtual environment
    deactivate


# Return to home directory
cd "$HOME_DIR" || exit
echo "Task completed."

