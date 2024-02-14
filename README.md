# AEV Reference Deployment

This project includes a Docker Compose template to deploy [Alfresco Enterprise Viewer](https://docs.alfresco.com/enterprise-viewer/latest/install/) (AEV).

* [.env](.env) specifies Alfresco Content Services version to be used by Docker Compose
* [compose.yaml](compose.yaml) describes Docker Compose deployment

>> Note this is a sample deployment designed for education purposes. When using Alfresco Enterprise Viewer in real world, additional requirements should impact in the design of the final deployment.

A valid license, named `TextLicense.l4j`, must be obtained to use this project. Please ensure that this file is located in the `alfresco/license` folder before initiating the project. If you are an Enterprise Customer or Partner, feel free to reach out to [Alfresco Hyland Support](https://community.hyland.com) to acquire the necessary license.

## Prepare the environment

Download `alfresco-enterprise-viewer-package-3.6.0.zip` from https://community.hyland.com/Products/alfresco/release-notes/release-notes/Alfresco-Enterprise-Viewer-Releases/alfresco-enterprise-viewer-360 using customer or partner credentials for Hyland Community.

Unzip `alfresco-enterprise-viewer-package-3.6.0.zip` to local `resources` folder:

```bash
$ mkdir resources && unzip alfresco-enterprise-viewer-package-3.6.0.zip -d resources
$ ls -l resources
Alfresco Artifacts
Collaboration
Docker Compose Example
Share Artifacts
Third Party
Web Applications
empty
```

Copy required resources to `alfresco/resources` folder for Alfresco Repository configuration:

```bash
$ cp resources/Alfresco\ Artifacts/oa-alfresco.amp alfresco/resources
$ cp resources/Alfresco\ Artifacts/tsgrp-opencontent-3.6.0-for-acs7.4.amp alfresco/resources
$ cp resources/Web\ Applications/*.war alfresco/resources
$ cp resources/Third\ Party/pdfium.tar.gz alfresco/resources
```

Verify that a valid `TextLicense.l4j` file for AEV has been copied to `alfresco/licenses` folder

If you want to use also an ACS license, copy `alfresco.lic` file to `alfresco/licenses` folder. In addition following line from `compose.yaml` must be uncommented:

```yaml
#      - ./alfresco/license/alfresco.lic:/usr/local/tomcat/webapps/alfresco/WEB-INF/classes/alfresco/extension/license/alfresco.lic   
```

Copy required resources to `share/resources` folder for Alfresco Share configuration:

```
$ cp resources/Share\ Artifacts/*.amp share/resources
```

## Using

```
docker-compose up --build --force-recreate
```

## Service URLs

Share App 
* URL: http://localhost:8080/share
* Credentials: admin / admin