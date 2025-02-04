## Python Environment Management

### Python virtual environment
- **Create virtual environment**:
  ```bash
  > python<version> -m venv <virtual-environment-name>
  ```
- **Activate virtual environment**:
  ```bash
  > <virtual-environment-name>/bin/activate # Linux/MacOS
  > <virtual-environment-name>/Scripts/activate.bat # In CMD
  > <virtual-environment-name>/Scripts/Activate.ps1 # In Powershell
  ```
- **Deactivate virtual environment**:
  ```bash
  > deactivate
  ```

### Python virtual environment with conda
- **Create virtual environment**:
  ```bash
  > conda create -n <my-environment> python=<python-version>
  > conda create -n <my-environment> python=<python-version> ipykernel # if kernel is required (jupyternotebook)
  ```
- **Activate virtual environment**:
  ```bash
  > conda activate <my-environment> # Linux/MacOS
  > activate <my-environment> # Windows
  ```
- **Deactivate virtual environment**:
  ```bash
  > conda deactivate
  ```
- **Setup ipykernel (if there was no kernel created)**:
  ```bash
  > conda install ipykernal
  > python3 -m ipykernel install --user --name <my-environment> --display-name "Python3 (<my-environment>)"
  ```
- **List all conda environment created**:
  ```bash
  > conda env list
  ```
- **List all packages and versions installed in active environment**:
  ```bash
  > conda list
  ```
- **Remove conda environment**:
  ```bash
  > conda remove --name <my-environment> --all
  ```

### Useful python package to manage dependency
```bash
> pip install pip-chill
> pip-chill > requirements.txt
```

## Install dependency through a requirements.txt file
```bash
> pip install -r requirements.txt
```
