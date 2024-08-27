# jenkinstoopensift
this flow pipeline 
1. clone code from github
2. analysis code using sonarqube
3. build code to be image on openshift
4. analysis image using trivy
5. push image to image repository
6. deploy image on opensift

post action:
1.  delete all artefact / cache crated by step building
2. make sure application run as container on openshift.