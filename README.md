# urban-tech-berlin-trees

## Project Setup

This guide explains how to set up the **Google Earth Engine Python API** inside a Conda environment named `berlin-trees`. All dependencies are installed via `requirements.txt`, and the guide includes full authentication steps for running Earth Engine inside Jupyter notebooks.

---

### 📦 1. Create and Activate the Conda Environment

```bash
conda create -n berlin-trees python=3.14
conda activate berlin-trees
```

---

### 📄 2. Install Dependencies from `requirements.txt`

Find the `requirements.txt` file in the project folder and install dependencies, this contains earthengine-api:

```bash
pip install -r requirements.txt
```

---

### 🔐 3. Authenticate Earth Engine in a Jupyter Notebook

Start Jupyter:

```bash
jupyter notebook
```

In a notebook cell:

```python
import ee
ee.Authenticate()
```

This launches a browser window where you will:

1. Log into your Google account
2. Create a new Google Cloud project (required by Earth Engine) and note down the project-id for later
3. Register your project for non-commercial usage (there should be a link in the flow alerting you to this)
4. Grant required permissions:
   - Access Google Drive files (optional, required only if you export to Drive)
   - Access Google Cloud data
   - Access Google Earth Engine data (required)
   - View Google Cloud Storage data (optional)


Copy the verification token back into the notebook when prompted.

---

### 🔐 4. Authenticate Earth Engine in the Conda Environment (CLI)

In the same terminal (with `berlin-trees` activated):

```bash
earthengine authenticate
```

This ensures the CLI and Python API share the same credentials.

---

### 🛠 5. Fix SSL Certificate Issues on macOS (If Needed)

If you encounter SSL certificate verification errors during authentication, run the installer script included with the python.org macOS installer:

```bash
# Open and run this file (double-click from Finder):
/Applications/Python 3.10/Install Certificates.command
```

Running this script installs the system CA bundle for Python and typically resolves the `CERTIFICATE_VERIFY_FAILED` error.

---

### 🚀 6. Initialize Earth Engine with Your Project ID

Because Earth Engine uses a Google Cloud project for quota and API access, initialize with the project ID you created during the web-based authentication flow.

In a notebook:

```python
import ee
ee.Initialize(project='projects/<your-project-id>')
```

Replace `<your-project-id>` with the project ID shown in the web flow (for example `projects/berlin-trees-123456`).

This step succeeds only if:

- The project exists
- Earth Engine API is enabled for the project
- Your Google account has access to the project

---

## ✔️ 7. Verify Your Installation

Try running the code for loading a small sample in script load_ndvi_sample.ipynb to check your authentication.

---

## 🎉 Notes & Tips

- Only grant additional Google permissions (Drive, Cloud Storage) if you plan to export data to those services.
- If you run into `ee.Initialize: no project found`, explicitly pass the `project=` argument as shown above.
- If macOS SSL problems persist, ensure the Jupyter kernel uses the same Python executable from the `berlin-trees` conda environment.