System Design - Dropbox:
========================


Requirement: (10 min)
=====================

1) Functional Requirement.
     -Cloud Storage  (upload & Download)
     -Share
     -search
     -sync.
     -versioning.
     -collaboration
     
2) Non-Functional Requirement.
     
     -Availability of document all time (e.g 99% available) .
     -scalable(add or remove ram without restart server node).
     -durable( upload a file it will be available )
     
     durable vs availablity:
     =======================
      - Availability -upload a file it will be availble 99% -availability
           but durable even it is down can download file once server up.
      - durability - but 1% if down we can get the file once server available so durable.
