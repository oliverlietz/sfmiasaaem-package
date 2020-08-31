# Scanning for Malware in Apache Sling and Adobe Experience Manager – Package for AEM 6.5.5

This package (*SfMiASaAEM*) contains all bundles and sample configurations to run [Apache Sling Clam](https://github.com/apache/sling-org-apache-sling-clam) on AEM 6.5.5.

## Docker (for Clam AV)

**Install [Docker](https://www.docker.com/) (on Mac OS with [Homebrew](https://brew.sh/))**

    brew install docker

**Start Docker application (daemon)**

## Clam AV Daemon

**Start Clam daemon**

    docker run -d -p 3310:3310 mkodockx/docker-clamav:alpine

## Adobe Experience Manager

**Start AEM** (set `admin` password to `admin` to use the below commands unchanged)

    java -jar cq-quickstart-6.5.0.jar

**Install Service Pack 6.5.5**

    curl -u admin:admin -F file=@"aem-service-pkg-6.5.5.zip" -F install=true http://localhost:4502/crx/packmgr/service.jsp

**Build and install _SfMiASaAEM Package_**

    git clone git@github.com:/oliverlietz/sfmiasaaem-package.git
    cd sfmiasaaem-package
    mvn clean package
    curl -u admin:admin -F file=@"target/sfmiasaaem-package-1-SNAPSHOT.zip" -F install=true http://localhost:4502/crx/packmgr/service.jsp

Set up [Apache Sling Commons Crypto](https://sling.apache.org/documentation/bundles/commons-crypto.html) and [Apache Sling Commons Messaging Mail](https://github.com/apache/sling-org-apache-sling-commons-messaging-mail) for use with `MailSendingScanResultHandler` (requires SMTP account with SSL/TLS enabled).

