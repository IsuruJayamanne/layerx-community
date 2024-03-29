# The AI Data Platform

![LayerX.ai](images/Layerx_logo_purple.svg)
### Annotate, Manage and Deploy Training Data  
End-to-end AI data management platform that helps ML teams to annotate, manage and deploy training data at scale.  
<br/><br/>
![projects](images/Layerx_projects.png?raw=true)
<br/><br/>
<br/><br/>
![annotationtool](images/Layerx_tool.png?raw=true)
<br/><br/>
LayerX is on a mission to accelerate AI application development by empowering ML Team with modern tools.
<br/><br/>
## Features
* Image and video annotations with multiple annotations types.  Just drag and drop any image or video file and start annotating in a minutes.
* Class and Attribute level annotations. For example, class can be Vehicle, attributes can be car, van, truck.
* Annotation task management. Byte size tasks make it easy to annotate large volumes of data at scale.
* Dataset management. Create, manage and deploy training datasets from annotated data with version control in place.
* Data Augmentation. Increase your dataset size by adding slightly modified copies via the built-in augmentation functions.
* Export Dataset to the training machine with annotations easily using the dataset sync tool.

<br/><br/>
Install Open Source version using below instructions. Try LayerX cloud version from here [LayerX Cloud](https://layerx.ai)
<br/><br/>
## High Level System Architecture

![Component Structure diagram](images/Layerx_components.png?raw=true  "Component Structure")

**Backend - annotation manager (NodeJS) :**
* REST API endpoint for Annotation tool frontend
* Communicate with Python backend (Flask App) to offload background tasks such as annotation task generation and dataset creation
<br/><br/>

**Backend - data processor (Python Flask) :**
* Create annotation tasks from uploaded videos or images
* Create Datasets and augment images
<br/><br/>

**Frontend- (Angular Web) :**
* User interface to manage annotation projects and data sets
* Rich web interface for annotating objects
<br/><br/>

# Deploy LayerX-ai with docker

## Pre-requirements

Tested OS : Ubuntu 20.04.2 LTS

**Install git**
```bash
apt install git-all
```

**Install Docker** - <https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository>

**Install Docker Compose** - <https://docs.docker.com/compose/install/#install-compose-on-linux-systems>

[Configure to manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/)

**Create an AWS S3 bucket** - <https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html>

### Useful
[How to find AWS S3 Access key / Secret key](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)


## Clone Repository
### [layerx-community](https://github.com/LayerX-AI/layerx-community)
```bash
git clone https://github.com/LayerX-AI/layerx-community.git
```


## Environment Specific Configurations
**.env** file (at the root of local repository)


### URL which system is hosted
```
BASE_URL = <server  url>
Note: if hosted in local, then put this as "http://localhost"
```

### AWS S3 bucket configurations
```
AWS_ACCESS_KEY = <AWS_ACCESS_KEY>
AWS_SECRET_KEY = <AWS_SECRET_KEY>
AWS_REGION = <AWS_REGION  eg:us-east-1>
AWS_BUCKET_NAME = <S3 Bucket name>
```

### Support email sending config with sendgrid (optional)
```
SENDGRID_API_KEY = <SENDGRID_API_KEY>
SUPPORT_EMAIL = <YOUR_EMAIL_ADDRESS_FOR_SUPPORT_EMAIL_SENDING>
```

### google drive configuration for content upload (optional)
```
GOOGLE_API_KEY = <GOOGLE_API_KEY>
GOOGLE_CLIENT_ID = <GOOGLE_CLIENT_ID.apps.googleusercontent.com>
GOOGLE_CLIENT_SECRET = <GOOGLE_CLIENT_SECRET>
GOOGLE_REFRESH_TOKEN = <GOOGLE PLAYGROUND REFRESH TOKEN>
```

## Run Configure script to update configurations of each components
```bash
./configure.sh
```
---

## Run the system
```bash
docker-compose up
```

<br/><br/>
### LayerX system is now ready to use
<br/><br/>

#### Default LayerX Credentials
* Username: 	admin@layerx.local.ai
* Password:	YourPassWord123

<br/><br/>

## Additional Notes

### Directory structure looks like
```bash
.
+-- layerX-enterprise/
	---.env
	---default.env
	---docker-compose.yml
	+--contents/
	+--uploads/
	+--mongoData/
	+--DB_initial_data/
	---nginxData/
		+--nginx/
	+--layerx-angular-frontend/
	+--layerx-python-backend/
	+--layerx-nodejs-backend/
	+--layerx-sync-tool
```

### Services and ports
* mongodb - 1521
* python_app - 8081
* node_backend - 8080
* frontend - 8085
* nginx - 80

## Other Commands
Start the system
```bash
docker-compose up
```
Stop the system
```bash
docker-compose stop
```
Restart the system
```bash
docker-compose restart
```
Start a single service
```bash
docker-compose up <service name>
eg: docker-compose up node_backend
```
Build a container service (node_backend, python_app and frontend)
```bash
docker-compose build <service name>
eg: docker-compose build frontend
```
Build a service from image (mongodb and nginx)
```bash
docker-compose up --force-recreate <service name>
eg: docker-compose up --force-recreate nginx
```


