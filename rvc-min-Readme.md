[**English**](rvc-min-Readme.md) | [**日本語**](rvc-min-Readme.ja.md)

# Project Setup Instructions

This README provides detailed instructions for setting up the Python environment and preparing the necessary packages for the project.

**Note:** The main environment performing the build should use Python 3.9 to ensure compatibility with the CPP release version libraries.

0. **Copy Files from GitHub:**

    First, copy all the files from the specified GitHub page to the CPP release directory.

## Setting up the Python Virtual Environment

1. **Navigate to the CPP Release Directory:**

    Start by navigating to the CPP release directory:

    ```cmd
    cd <CPP_RELEASE_DIR>
    ```

2. **Create and Activate the Virtual Environment:**

    Create a new virtual environment in the current directory:

    ```cmd
    python -m venv .venv
    ```

    This command will create a new directory named `.venv`.

    Then, activate the virtual environment:

    ```cmd
    .\.venv\Scripts\activate
    ```

    The terminal prompt will change to show the name of the virtual environment, indicating that it is active.

## Installing PyTorch

3. **Install PyTorch:**

    Install PyTorch along with torchvision and torchaudio:

    ```cmd
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
    ```

## Installing Additional Dependencies

4. **Install Other Required Packages:**

    Install other required packages:

    ```cmd
    pip install -r rvc-min-requirements.txt
    ```

## Updating the CPP Release Directory

5. **Prepare and Update the `site-packages`:**

    Rename the existing `site-packages` directory:

    ```cmd
    ren "lib\site-packages" "site-packages_old"
    ```

    Copy the contents of `.venv\Lib\site-packages`:

    ```cmd
    xcopy /E /I ".venv\Lib\site-packages" "lib\site-packages"
    ```

## Optional Steps

6. **Manual Installation of `tkinter`:**

    If you encounter an error because Python 3.9 was installed without `tkinter`, you can manually copy the `tkinter` folder from the Python distribution to the `lib\site-packages` directory:

    ```cmd
    xcopy /E /I "tkinter" "lib\site-packages\tkinter"
    ```
   
    This step should only be performed if you're sure that `tkinter` is not included in your Python installation.

    After successfully copying the `tkinter` directory, you can delete the original `tkinter` directory from the current directory:

    ```cmd
    rmdir /S /Q "tkinter"
    ```

    This step cleans up the unnecessary `tkinter` folder in the current directory.


## Optional Cleanup and Finalization

7. **Move Specific Directories to 'to_remove':**

    Check if the directories exist, and if they do, move them to a 'to_remove' directory:

    ```cmd
    md assets\to_remove
    move "assets\pretrained" "assets\to_remove"
    move "assets\pretrained_v2" "assets\to_remove"
    move "assets\uvr5_weights" "assets\to_remove"
    ```

    Remove all unnecessary asset files except for 'hubert', 'rmvpe', and 'weights'.

8. **Delete the Old `site-packages` Directory:**

    After testing, delete the `site-packages_old` directory:

    ```cmd
    rmdir /S /Q "lib\site-packages_old"
    ```

9. **Final Cleanup:**

    Finally, remove the created virtual environment directory:

    ```cmd
    rmdir /S /Q ".venv"
    ```
   
