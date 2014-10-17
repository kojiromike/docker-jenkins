# Jenkins Docker Automation

## Goals

### Reverse Proxy with Dynamic Naming

A reverse proxy server is on a Docker container with ports 80 and 443 published. When it receives an HTTP(s) request, the reverse proxy will map the HOST of the request to another Docker container. For example, a request to `foo.domain` would be forwarded to the container named _foo_.

- Jenkins itself is on a Docker Container.
- Jenkins can run Docker commands, so HTTPd, PHP-FPM, MySQL and other dependent services can be started and orchestrated on demand by Docker commands run in Jenkins.
- Jenkins jobs that require transient Magento installs can create and orchestrate the necessary containers to run tests without exposing any services to the outside world.
- But Jenkins jobs can also be used to build human-reachable test and demo environments. Such environments would be reachable through the aforementioned reverse proxy.

```
\o/                                       
 |  --  GET http://xyzzy.domain/
/ \    -----------------------------------                                   
dev   | vSphere                           |                                    
      |                                   |
      |  -------------------------------  |
      | | Docker Host                   | |
      | |                               | |
      | |  ---------------     -------  | |
      | | | Reverse Proxy | - | xyzzy | | |
      | |  ---------------     -------  | |
      | |     |       |    \            | |
      | |  ------     |      ------     | |
      | | | www2 |    |     | www3 |    | |
      | |  ------     |      ------     | |
      | |       ------+------           | |
      | |      |             |          | |
      | |    -----         ------       | |
      | |   | ... |       | wwwN |      | |
      | |    -----          -----       | |
      |  -------------------------------  |
       -----------------------------------
```
