#!/bin/bash

# Check if a file path is provided
if [ -z "$1" ]; then
    echo "Usage: pyvenv <path_to_tool.py> [arguments...]"
    exit 1
fi

# Check if the tool.py file exists
if [ ! -f "$1" ]; then
    echo "Error: '$1' not found."
    exit 1
fi

# Get the directory of the tool.py file
TOOL_DIR=$(dirname "$1")

# Check if there's a venv directory in the tool's directory
if [ ! -d "$TOOL_DIR/venv" ]; then
    echo "Error: No virtual environment found in '$TOOL_DIR'."
    exit 1
fi

# Activate the virtual environment
source "$TOOL_DIR/venv/bin/activate"

# Shift past the first argument (tool.py), and pass the remaining arguments to python3
shift

# Run the tool.py script with any additional arguments
python3 "$1" "$@"

# Deactivate the virtual environment
deactivate
