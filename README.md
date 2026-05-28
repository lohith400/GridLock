# GridLock Project

This project contains the `GridLock.ipynb` notebook for training a LightGBM model on traffic demand data.

## Virtual Environment Setup

From the `Personal/GridLock` folder:

```bash
python -m venv .venv
```

Activate the venv:

- Windows PowerShell:
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
- Windows Command Prompt:
  ```cmd
  .\.venv\Scripts\activate.bat
  ```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

## Dependencies

- pandas
- numpy
- scikit-learn
- lightgbm

## Notes

- Ensure your dataset files are available in the `/dataset` directory used by `GridLock.ipynb`.
- After activation, you can run the notebook using Jupyter or VS Code notebook support.
