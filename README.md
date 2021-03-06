Advanced Python Based Job Scheduler Utility
==============
Components which need to run periodically will depend on job scheduler. It consists of three parts. 
The first one is a self-made job command line executer. Like shell command, Some commands like help, schedule, run once and some other commands which are used to run actual components are already implemented. 
When the user is typing the wrong command, it will print out the help information for user. 
When user try to schedule a job, if schedule success, it will call another part of job scheduler which is job daemon. 
Job daemon is a separate part of the system. User can start, stop or restart job daemon to operate job daemon just like the command of other service. I am using apscheduler, which is an enterprise job scheduler API. 
The third part is job framework which is the basic of the other parts mentioned. It contains some common python based interfaces. If other components developed by others wants to run their component periodically, he only need to implement these interface. After that in order to run on job scheduler, he only need to put their project packaged into specific folder and run command.
This Python based job scheduler is composed by two parts:

Job daemon
=====================
1. Start job daemon:
`python JobDaemon.py`

2. Stop job daemon:
`kill <pid>`

3. View job daemon log:
`tail -f <stdout>`


Python based command line tool (CLI)
==================
Current supported command:

1. List all job (command: `jobs> listjob`)
2. List all scheduled job (command: `jobs> listscheduledjob`)
3. Run job once (command: `jobs> runonce -j <job name>`)
4. Schedule periodical job (command: `jobs> schedule -j <job name> -i <interval>`)
5. Un-schedule periodical job (command: `jobs> unschedule -j <job name>`)
6. Exit command line tool (command: `jobs> exit`)
7. Exit command line tool (command: `jobs> quit`)

Job Scheduler Framework
==================
Framework:
```
|--- Commands (can be implemented)
|       |----- list_job.py
|       |----- list_scheduled_job.py
|       |----- runonce.py      
|       |----- schedule.py
|       |----- unschedule.py
|       |----- quit.py
|       |----- exit.py
|--- Job Files (can be implemented by user)
|       |----- jobs-simple.py (Sample job)
|       |----- other_job.py
|--- Command.py (command interface)
|--- CommandParser.py (module for parsing command)
|--- JobConsole.py (Command line tool)
|--- JobDaemon.py (Job Daemon module)
|--- tester.py (Test file)
```
