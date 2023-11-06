## CICD with github action in heruku



__create a django project__

__create folder .github/workflows__

__create file django.yml inside workflows__

```
name: Django Github Action

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      max-parallel: 2
      matrix:
        python-verison: [3.11]
    
    steps:
    - uses: actions/checkout@v4
    - name: Setup Python Version ${{ matrix.python-version }}
      uses: actions/setup-python@v4.7.1
      with:
        python-version: ${{matrix.python-verison}}
    - name: Install Dependency for django
      run:
        python -m pip install --upgrade pip
        pip install -r requirements.txt
  
```
> This code is for building, and it works on when push the code. This runs on ubuntu latest and python version use this verison for building. And some command which work while building.


_click github action button for check for checking progress_

create app in heruku

copy app name in github __settings>secrets and variables>action__

create new repository secret with app name another secret for heruku api key

```
deploy:
    runs-on: ubuntu-latest
    name: deploy djanog app on heruku
    steps:
      - name: checkout
        uses: actions/checkout@v4

      - name: Deploy
        uses: akhileshns/heroku-deploy@v3.12.14 # This is the action
        with:
          heroku_api_key: ${{secrets.HERUKU_SECRET_KEY}}
          heroku_app_name: ${{secrets.HERUKU_SECRET_NAME}}
          heroku_email: "asadfe24@gmail.com"
          branch: "main"


```
> This code is for deploy process where it use api key, app name from the github secret name and email.