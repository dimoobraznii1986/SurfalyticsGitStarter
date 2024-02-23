# SurfalyticsGitStarter


## Git commands

1. Clone the code from repo

```bash
git clone https://github.com/<your user>/<repo name>.git
```

2. Check the status of git repo

```bash
git status
```

3. Create new branch


```bash
git checkout -b dmitry/modify-files
```

4. Download objects and refs from another repository

```bash
git fetch
```

5. Fetch from and integrate with another repository or a local branch

git pull

```bash
git pull
```

6. Check list of branches

```bash
git branch -a
```

7. Checkout main

```bash
git checkout main
```

8. Index new and modified files

```bash
git add .
```

## Docker

We can start from creating Virtual Environment:

```bash
python3 -m venv venv
```

Then we can activate it:

```bash
source venv/bin/activate
```

Install the libraries we want:

```bash
pip install flask
```

And create the `requirements.txt` file for future needs:

```bash
pip freeze > requirements.txt
```

Let's create a new file in the folder web-app:

```bash

mkdir web-app

cd web-app

touch app.py

vim app.py
```

And paste this little code snippet:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```

We can test this app:

```bash
pwd

python app.py
```

We can access this app in browser [http://localhost:80](http://localhost:80)

Next we can create the docker file (difinition of what should happen)

```bash
touch Dockerfile

vim Docekrfile
```

And put the information:

```bash
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

Now we can test that our Docker file can start:

Some of docker commands:

Docker

```bash

docker build .

docker build -t web-app-container .

docker build -t web-app-container:v0.1 .

docker run -p 80:80 --name web-app-container web-app

docker run --name web-app-container web-app

docker ps

docker rm web-app-container

docker run -p 80:80 --rm --name web-app-container web-app

docker run -p 80:80 --rm -d --name web-app-container web-app

docker ps

docker exec -it 82a63468910a bash

```

What if we should have multiple containers work together? We should use Docker Compose:

Let's create an example:

```bash
cd ..

touch docker-compose.yaml

vim docker-compose.yaml
```

We can copy-paste:

```yaml
version: '3'
services:
  web:
    build: ./web-app
    ports:
      - "80:80"
    depends_on:
      - redis
  redis:
    image: "redis:6.0"
```

Docker compose commands:

```bash
docker-compose build

docker-compose build --no-cache

docker-compose up
```
