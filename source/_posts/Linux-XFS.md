---
title: Linux - XFS
date: 2024-06-09 23:50:00
tags:
---
- Create xfs dump
	- ```shell
	  [root@pplxelas03 backup]# xfsdump -l 0 -f /backup/log.image /dev/vg00/log
	  xfsdump: using file dump (drive_simple) strategy
	  xfsdump: version 3.1.8 (dump format 3.0) - type ^C for status and control
	  
	   ============================= dump label dialog ==============================
	  
	  please enter label for this dump session (timeout in 300 sec)
	   -> log
	  session label entered: "log"
	  
	   --------------------------------- end dialog ---------------------------------
	  
	  xfsdump: level 0 dump of pplxelas03:/log
	  xfsdump: dump date: Tue Dec 12 14:41:45 2023
	  xfsdump: session id: 1d29e5ea-a30b-4e3b-9804-08ca6a08a94a
	  xfsdump: session label: "log"
	  xfsdump: ino map phase 1: constructing initial dump list
	  xfsdump: ino map phase 2: skipping (no pruning necessary)
	  xfsdump: ino map phase 3: skipping (only one dump stream)
	  xfsdump: ino map construction complete
	  xfsdump: estimated dump size: 129555136 bytes
	  
	   ============================= media label dialog =============================
	  
	  please enter label for media in drive 0 (timeout in 300 sec)
	   -> log
	  media label entered: "log"
	  
	   --------------------------------- end dialog ---------------------------------
	  
	  xfsdump: creating dump session media file 0 (media 0, file 0)
	  xfsdump: dumping ino map
	  xfsdump: dumping directories
	  xfsdump: dumping non-directory files
	  xfsdump: ending media file
	  xfsdump: media file size 125576832 bytes
	  xfsdump: dump size (non-dir files) : 125486656 bytes
	  xfsdump: dump complete: 16 seconds elapsed
	  xfsdump: Dump Summary:
	  xfsdump:   stream 0 /backup/log.image OK (success)
	  xfsdump: Dump Status: SUCCESS
	  ```
- Show xfs dump
	- ```shell
	  [root@pplxelas03 backup]# xfsrestore -I
	  file system 0:
	          fs id:          52c8124b-e8f5-4d85-8470-4601f512251f
	          session 0:
	                  mount point:    pplxelas03:/log
	                  device:         pplxelas03:/dev/mapper/vg00-log
	                  time:           Tue Dec 12 14:41:45 2023
	                  session label:  "log"
	                  session id:     1d29e5ea-a30b-4e3b-9804-08ca6a08a94a
	                  level:          0
	                  resumed:        NO
	                  subtree:        NO
	                  streams:        1
	                  stream 0:
	                          pathname:       /backup/log.image
	                          start:          ino 131 offset 0
	                          end:            ino 283520 offset 0
	                          interrupted:    NO
	                          media files:    1
	                          media file 0:
	                                  mfile index:    0
	                                  mfile type:     data
	                                  mfile size:     125576832
	                                  mfile start:    ino 131 offset 0
	                                  mfile end:      ino 283520 offset 0
	                                  media label:    "log"
	                                  media id:       e425c92d-3a30-47c5-ab26-2ab8270e8d31
	  xfsrestore: Restore Status: SUCCESS
	  ```
- Restore xfs dump
	- ```shell
	  [root@pplxelas03 backup]# xfsrestore -v trace -f /backup/log.image /backup/log.restore
	  xfsrestore: using file dump (drive_simple) strategy
	  xfsrestore: version 3.1.8 (dump format 3.0) - type ^C for status and control
	  xfsrestore: searching media for dump
	  xfsrestore: examining media file 0
	  xfsrestore: file 0 in object 0 of stream 0
	  xfsrestore: file 0 in stream, file 0 of dump 0 on object
	  xfsrestore: dump description:
	  xfsrestore: hostname: pplxelas03
	  xfsrestore: mount point: /log
	  xfsrestore: volume: /dev/mapper/vg00-log
	  xfsrestore: session time: Tue Dec 12 14:41:45 2023
	  xfsrestore: level: 0
	  xfsrestore: session label: "log"
	  xfsrestore: media label: "log"
	  xfsrestore: file system id: 52c8124b-e8f5-4d85-8470-4601f512251f
	  xfsrestore: session id: 1d29e5ea-a30b-4e3b-9804-08ca6a08a94a
	  xfsrestore: media id: e425c92d-3a30-47c5-ab26-2ab8270e8d31
	  xfsrestore: using online session inventory
	  xfsrestore: searching media for directory dump
	  xfsrestore: dump session label: "log"
	  xfsrestore: dump session id: 1d29e5ea-a30b-4e3b-9804-08ca6a08a94a
	  xfsrestore: stream 0, object 0, file 0
	  xfsrestore: initializing directory attributes registry
	  xfsrestore: initializing directory entry name registry
	  xfsrestore: initializing directory hierarchy image
	  xfsrestore: reading directories
	  xfsrestore: reading the ino map
	  xfsrestore: reading the directories
	  xfsrestore: directory 128 0 (0): updating
	  xfsrestore: 1 directories and 110 entries processed
	  xfsrestore: number of mmap calls for windows = 1
	  xfsrestore: directory post-processing
	  xfsrestore: dump session label: "log"
	  xfsrestore: dump session id: 1d29e5ea-a30b-4e3b-9804-08ca6a08a94a
	  xfsrestore: stream 0, object 0, file 0
	  xfsrestore: restoring non-directory files
	  xfsrestore: media file 0 in object 0 of stream 0
	  ...
	  ...
	  xfsrestore: truncating PRD-PRI-2023-10-20-1.json.gz from 0 to 697
	  xfsrestore: restore complete: 0 seconds elapsed
	  xfsrestore: Restore Summary:
	  xfsrestore:   stream 0 /backup/log.image OK (success)
	  xfsrestore: Restore Status: SUCCESS
	  ```
