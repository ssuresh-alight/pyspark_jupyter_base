## About

Running Jupyter notebook for testing out PySpark running in Docker compose.

## How to run

Start up the Jupyter server on http://localhost:8888

```sh
docker compose up --build
```

Stop using `Ctrl + C` and

```sh
docker compose down
```

Install the Python, Jupyter notebook, PyLance extensions in VSCode.

Open `.ipynb` notebook.

Connect to kernel using command: `Notebook: Select Notebook Kernel` -> `Select another kernel` -> `Existing Jupyter Server` -> `Enter the URL` -> enter `http://localhost:8888`

### Spark UI

Access Spark UI at http://localhost:4040

### Generate Data

Use the `generate_data.ipynb` notebook to generate data files - tweak params as needed

## Known issues

1. `Import "pyspark.sql" could not be resolved` warning for the import
    Autocomplete might still work, but intellisense/hover text for pyspark appears to not work. Refer to PySpark documentation or use `help()` function to get help

2. Bind mounting `./work` not working in WSL2
    Changes made to `work` directory in neither host nor container are persisted/visible in each other. This is with Rancher Desktop + WSL2 Ubuntu Linux. When running the code from Windows filesystem using `docker compose`, this issue seems to be not present.

    **Fix:** This seems to be a Rancher Desktop bug. Make sure your Windows `C:\` drive is mounted to `/mnt/c/` instead of something like `/c/` in WSL2.
    Remove any `[automount] root` settings from `/etc/wsl.conf`.

    See:
    
    - https://learn.microsoft.com/en-us/windows/wsl/wsl-config#automount-settings
    - https://github.com/rancher-sandbox/rancher-desktop/issues/3047
