# spdclient

`spdclient` is a python wrapper around scrapy's [scrapyd](https://github.com/scrapy/scrapyd) webservice for ease of use.

## Basics

### Install

```
pip install spdclient
```

### Basic Usage
```python
from spdclient import SPDClient

client = SPDClient(
        host,               # Scrapyd Server default 127.0.0.1
        port,               # Scrapyd Server port default 6800
        username=None,      # Scrapyd Server Basic Auth Username if enabled
        password=None,      # Scrapyd Server Basic Auth Password if enabled
        is_https=False      # Is the server secured on https or not.
)
response=client.daemonstatus()
```

## Endpoints

### [/daemonstatus.json](https://scrapyd.readthedocs.io/en/stable/api.html#daemonstatus-json)
```python
response=client.daemon_status()
```

### [/addversion.json](https://scrapyd.readthedocs.io/en/stable/api.html#addversion-json)
```python
response=client.add_version(
    project:str,        # Project Name
    egg:str,            # Egg File Path
    version:str=None    # Version defaults to None for auto
)
```

### [/schedule.json](https://scrapyd.readthedocs.io/en/stable/api.html#schedule-json)
```python
response=client.schedule(
        project: str,               # Project Name
        spider: str,                # Spider Name
        setting: dict = None,       # Spider Settings Eg:{'DOWNLOAD_DELAY':10}
        jobid: str = None,          # Unique jobid defaults to None for auto UUID4
        priority: float = None,     # Priority defaults to 0
        version: str = None,        # Version to schedule on
        spider_args: dict = None,   # Spider Args Eg:{'URL':'www.google.com'}

)
```
### [/cancel.json](https://scrapyd.readthedocs.io/en/stable/api.html#cancel-json)
```python
response=client.cancel(
    project:str,        # Project Name
    job:str             # Unique Job ID
)
```
### [/listprojects.json](https://scrapyd.readthedocs.io/en/stable/api.html#listprojects-json)
```python
response=client.list_projects()
```
### [/listversions.json](https://scrapyd.readthedocs.io/en/stable/api.html#listversions-json)
```
response=client.list_versions()
```
### [/listspiders.json](https://scrapyd.readthedocs.io/en/stable/api.html#listspiders-json)
```python
response=client.list_spiders(
    project:str,        # Project Name
    version:str=None    # Version Name defaults to None for latest version
)
```
### [/listjobs.json](https://scrapyd.readthedocs.io/en/stable/api.html#listjobs-json)
```python
response=client.list_jobs(
    project:str=None  # Project Name use for project specific job group
)
```
### [/delversion.json](https://scrapyd.readthedocs.io/en/stable/api.html#delversion-json)
```python
response=client.delversion(
    project: str,       # Project Name 
    version: str        # Version Name to delete for the above project.
)
```
### [/delproject.json](https://scrapyd.readthedocs.io/en/stable/api.html#delproject-json)
```python
response=client.delproject(
    project: str    # Project Name for project to delete
)
```
