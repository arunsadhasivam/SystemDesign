System Design - Dropbox:
========================


Requirement: (10 min)
=====================

1)Functional Requirement:
==========================

     -Cloud Storage  (upload & Download)
     -Share
     -search
     -sync.
     -versioning.
     -collaboration
     
2)Non-Functional Requirement:
==============================
    
     -Availability of document all time (e.g 99% available) .
     -scalable(add or remove ram without restart server node).
     -durable( upload a file it will be available )
     
     durable vs availablity:
     =======================
     
      - Availability -upload a file it will be availble 99% -availability
           but durable even it is down can download file once server up.
      - durability - but 1% if down we can get the file once server available so durable.

3)Estimates:
============

     4 things company need to allocate for the resource or need to buy.

           -compute (cores) 
           -storage (tera or peta bytes)
           -memory. (gb/tb)
           -network. (bps - always bits per second not bytes per second).

       NOTE:
       =====
          -for dropbox storage & network is important.
          -for video edit,block chain or cpu intensive app compute is important.


     Input from interviewer:
     ========================

              Total users: 500M
              monthly active users : 100M.

       estimates based on input:
       =========================
       
          1)request per sec:
          ==================
                1 month = 2.5 m seconds
                1 day = 100k
                10 pow 3  = 1 KB
                10 pow 6 = 1 MB.
                10 pow 9 = 1Gb.
                10 pow 12 = 1 TB.
                
                Avg File size = 100 KB.
                No of Files = 100 Files
                
                 request = (no of users * no of files per month) / uploads per sec.
                request = 100M Users * 100 /2.5 M
                        = 4000 rps ( requests per second  )
             
             
            2)Storage:
            ==========
            
                   = 100 m X100 X 100 KB.
                   =100 * 10pow 6 * 10 pow2 * 100 * 10 pow 3
                   1 month = +/- (1 PB)/month
                   =12 PB year
                   
           3)Network:
           ==========
    
           Egres  - out from datacenter(get) 
           ingres - Ingress is traffic that enters the boundary of a network. In to data center(PUT) 
           n/w = 4000 rps * 100 * 100 KB* 8
               = 32* 10pow 3 * 100 * 10 pow 3 
               = 32 GBPS (giga bytes per sec)
 
 
 4)Architecture- End to End flow (one request flow):
 ====================================================
 
 
             user - >  server ---> File system. -> Disk.
                              \
                                DB  
               
    user - > request for a file -> webserver -> makes call to db -> starts downloading the file from file system.
                                               (get the path)
   
    user request for a file get the path from db and return the path to the server and
    the webserver stream the bytes from the file system.
     
     API :
     ====
        GET - getFP() - return filePath
        GET - getFile( String filePath);
      
      
5)Detailed  System Design Diagram:
==================================
   

                           Edge DataCenter
                                |      |           proxy -> AWS S3
                                |      |         / 
                 client -> pop -> LB -> upload  -----------------> DB
                    |           |      |     \    \
                   DNS          |      |      Queue \   (upward flow)                  
                                |      |         \   \
                                |      |          \ -->Preview 
                                |      |           \   \
                                |      |            \ __ Indexing -> DB
                                |      |            
                                |      |------------- Data Center   -------------->                   

     client ->call to dns to get the nearest Point of presence.


    AWS S3 - Object Store 
    
    Reverse Proxy vs Load Balancer
    ==============================
    
    Reverse Proxy:
    ==============
    A reverse proxy accepts a request from a client, forwards it to a server that can fulfill it,
    and returns the server’s response to the client.

     load balancer:
     ==============
     
     A load balancer distributes incoming client requests among a group of servers, 
     in each case returning the response from the selected server to the appropriate client.

    
6)Data base Design:
===================

       +user 
        - userid

       +file
         -fid(pk)
         -uid(fk)

       +version
          -vid(pk)
          -fid(pk)
 
 
 NOTE:
 =====
 
    Need to design distributed cache to improve the speed and horizontal scalling.
    
    sharding - mechanism to improve the scalability to share loading in databse side.
    distributed cache - for application side and horizontal scalling to improve the scalability.
    
          
