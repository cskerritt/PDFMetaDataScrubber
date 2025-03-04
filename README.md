# **🚀 Complete Guide to Setting Up and Running the PDF Metadata Removal Tool on Windows**

This guide will walk you through **installing Python, setting up an IDE, configuring a virtual environment, installing dependencies, and running the GUI-based script**.

---

## **Step 1: Install Python on Windows**
Before running the script, you need to install Python.

### **1.1 Download Python**
1. Visit the [official Python website](https://www.python.org/downloads/).
2. Click **Download Python 3.x.x** (latest version).
3. Run the downloaded `.exe` file.

### **1.2 Install Python**
1. **Check the box** that says **"Add Python to PATH"** (this is important!).
2. Click **"Customize Installation"** (optional, but recommended).
3. Keep the default settings and click **"Next"**.
4. On the next screen, check **"Install for all users"**.
5. Click **"Install"**.
6. Wait for the installation to complete, then click **"Close"**.

### **1.3 Verify Python Installation**
1. Open **Command Prompt (cmd)** by pressing `Win + R`, typing `cmd`, and hitting `Enter`.
2. Type the following command:
   ```sh
   python --version
   ```
   If installed correctly, it should return something like:
   ```
   Python 3.x.x
   ```

---

## **Step 2: Install an IDE (PyCharm or VS Code)**
An **Integrated Development Environment (IDE)** is where you'll write and run your Python scripts.

### **Option 1: Install PyCharm (Recommended for Beginners)**
1. Go to [PyCharm’s official website](https://www.jetbrains.com/pycharm/download/).
2. Download the **Community Edition** (it's free).
3. Run the installer and follow these steps:
   - Choose the installation location and click **Next**.
   - Check **"Add launchers to PATH"**.
   - Click **Install**.
4. Once installed, **open PyCharm**.

#### **Configure PyCharm for Python:**
1. Open PyCharm and **click "New Project"**.
2. Select a **Location** where you want your project to be stored.
3. Under **Python Interpreter**, select **"New Virtual Environment"**.
4. Click **"Create"**.

PyCharm will now set up a virtual environment automatically.

---

### **Option 2: Install VS Code (For Advanced Users)**
1. Go to [VS Code’s website](https://code.visualstudio.com/).
2. Download and install it.
3. Open VS Code and install the **Python extension**:
   - Press `Ctrl + Shift + X` to open the **Extensions Marketplace**.
   - Search for **"Python"** and click **Install**.

4. Open a folder for your project:
   - Click **File > Open Folder**.
   - Select the folder where you will store your script.

---

## **Step 3: Set Up a Virtual Environment**
A **virtual environment** ensures that your project dependencies are isolated.

### **3.1 Open Command Prompt (cmd)**
1. Press `Win + R`, type `cmd`, and hit `Enter`.

### **3.2 Navigate to Your Project Folder**
Type:
```sh
cd path\to\your\project\folder
```
For example:
```sh
cd C:\Users\YourName\Documents\PythonProjects
```

### **3.3 Create a Virtual Environment**
Run:
```sh
python -m venv venv
```
This will create a folder named `venv`, which contains a separate Python environment for your project.

### **3.4 Activate the Virtual Environment**
```sh
venv\Scripts\activate
```
Once activated, you should see `(venv)` in your command prompt.

---

## **Step 4: Install Required Python Libraries**
With the virtual environment activated, install the necessary libraries:

```sh
pip install pikepdf
```

*(Tkinter is built into Python, so no need to install it separately.)*

---

## **Step 5: Create the Python Script**
### **5.1 Open Your IDE**
- Open **PyCharm** or **VS Code**.
- Click **File > New File** and name it `pdf_metadata_remover.py`.

### **5.2 Copy and Paste the Script Below**
```python
import pikepdf
import tkinter as tk
from tkinter import filedialog, messagebox
import os

def check_metadata(pdf_path):
    """Check and return metadata of a PDF file."""
    pdf = pikepdf.Pdf.open(pdf_path)
    return pdf.metadata

def remove_metadata(input_pdf, output_pdf):
    """Remove all metadata from a PDF file and save the cleaned version."""
    pdf = pikepdf.Pdf.open(input_pdf)
    pdf.metadata.clear()  # Clears all metadata
    pdf.save(output_pdf)

def select_file():
    """Opens a file dialog to select a PDF and processes metadata removal."""
    file_path = filedialog.askopenfilename(title="Select a PDF File", filetypes=[("PDF Files", "*.pdf")])
    
    if not file_path:
        return  # If user cancels file selection, do nothing

    # Generate output filename by appending "_cleaned" before file extension
    base_name, ext = os.path.splitext(file_path)
    output_pdf = f"{base_name}_cleaned{ext}"

    # Check metadata before removal
    before_metadata = check_metadata(file_path)
    before_text = "\n".join([f"{key}: {value}" for key, value in before_metadata.items()]) if before_metadata else "No metadata found"
    
    # Remove metadata
    remove_metadata(file_path, output_pdf)
    
    # Check metadata after removal
    after_metadata = check_metadata(output_pdf)
    after_text = "\n".join([f"{key}: {value}" for key, value in after_metadata.items()]) if after_metadata else "Metadata successfully removed."

    # Display results in a messagebox
    messagebox.showinfo("Metadata Removal Results",
                        f"📄 **Selected File:** {file_path}\n\n"
                        f"🧐 **Metadata Before Removal:**\n{before_text}\n\n"
                        f"✅ **Metadata After Removal:**\n{after_text}\n\n"
                        f"💾 **Cleaned File Saved As:** {output_pdf}")

# Create GUI window
root = tk.Tk()
root.title("PDF Metadata Remover")
root.geometry("400x200")

# Button to select a file and process it
btn_select = tk.Button(root, text="Select PDF File", command=select_file, font=("Arial", 12), padx=10, pady=5)
btn_select.pack(pady=40)

# Run the GUI event loop
root.mainloop()
```

---

## **Step 6: Run the Script**
### **Option 1: Run in PyCharm**
1. Click **Run > Run ‘pdf_metadata_remover’**.
2. The GUI window will appear.

### **Option 2: Run in Command Prompt**
1. Navigate to your project folder:
   ```sh
   cd path\to\your\project\folder
   ```
2. Activate the virtual environment:
   ```sh
   venv\Scripts\activate
   ```
3. Run the script:
   ```sh
   python pdf_metadata_remover.py
   ```

---

## **Step 7: Using the GUI**
1. **Click** the **"Select PDF File"** button.
2. **Choose** a PDF file from your computer.
3. The script will:
   - **Check metadata** before removal.
   - **Remove all metadata**.
   - **Save a cleaned file** with `_cleaned` appended to its name.
   - **Show a message box** with before/after metadata details.

---

## **🎯 Conclusion**
✅ **Installed Python & an IDE**  
✅ **Set up a virtual environment**  
✅ **Installed required libraries**  
✅ **Created a user-friendly GUI tool**  
✅ **Successfully removed metadata from PDFs**  

