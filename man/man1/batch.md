---
# vim: nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb
revision            : none yet
title               :
author              :
language            : en
lang                : en_UK
---

+--------------------------------------------------------------------------+
|     AT(1)              Linux Programmer's Manual             AT(1)       |
|                                                                          |
|                                                                          |
|                                                                          |
|     NAME                                                                 |
|            at, batch, atq, atrm - queue, examine or delete jobs for la |
| ter execu-                                                               |
|            tion                                                          |
|                                                                          |
|     SYNOPSIS                                                             |
|            at [-V] [-q queue] [-f file] [-mMlbv] TIME                    |
|            at [-V] [-q queue] [-f file] [-mMlbv] -t time_arg             |
|            at -c job [job...]                                            |
|            at [ -rd ] job [job...]                                       |
|            atq [-V] [-q queue]                                           |
|            atrm [-V] job [job...]                                        |
|            batch                                                         |
|                                                                          |
|     DESCRIPTION                                                          |
|            at and batch read commands from standard  input  or  a  speci |
| fied  file                                                               |
|            which are to be executed at a later time. |
|                                                                          |
|            at      executes commands at a specified time. |
|                                                                          |
|            atq     lists  the  user's  pending  jobs, unless the user is |
|  the supe-                                                               |
|                ruser; in that case, everybody's jobs are listed. The   |
| format                                                                   |
|                of  the  output  lines (one for each job) is: Job number, |
|  date, |
|                hour, queue, and username. |
|                                                                          |
|            atrm    deletes jobs, identified by their job number. |
|                                                                          |
|            batch   executes commands when system  load  levels  permit; |
|  in  other                                                               |
|                words, when  the  load  average  drops below 0.8, or the |
|  value                                                                   |
|                specified in the invocation of atd. |
|                                                                          |
|            At allows fairly complex time  specifications, extending  th |
| e  POSIX.2                                                               |
|            standard. It  accepts  times of the form HH:MM to run a job |
|  at a spe-                                                               |
|            cific time of day. (If that time is already  past, the  nex |
| t  day  is                                                               |
|            assumed.)   You  may  also specify midnight, noon, or teatime |
|  (4pm) and                                                               |
|            you can have a time-of-day suffixed with AM or PM for  runnin |
| g  in  the                                                               |
|            morning or the evening. You can also say what day the job wi |
| ll be run, |
|            by giving a date in the form month-name day with an optional  |
|  year, or                                                               |
|            giving a date of the form MMDDYY or MM/DD/YY or DD.MM.YY or Y |
| YYY-MM-DD. |
|            The specification of a date must follow the specification of  |
|  the  time                                                               |
|            of day. You can also give times like now + count time-units, |
|  where the                                                               |
|            time-units can be minutes, hours, days, or weeks and you can  |
| tell at to                                                               |
|            run  the  job today by suffixing the time with today and to r |
| un the job                                                               |
|            tomorrow by suffixing the time with tomorrow. |
|                                                                          |
|            For example, to run a job at 4pm three days from now, you wou |
| ld  do  at                                                               |
|            4pm  + 3 days, to run a job at 10:00am on July 31, you would  |
| do at 10am                                                               |
|            Jul 31 and to run a job at 1am tomorrow, you would do at 1am  |
|  tomorrow. |
|                                                                          |
|            The  exact  definition  of  the  time  specification  can  be |
|   found in                                                               |
|            /usr/share/doc/at-3.1.10/timespec. |
|                                                                          |
|            For both at and batch, commands are read from  standard  inpu |
| t  or  the                                                               |
|            file specified with the -f option and executed. The working  |
| directory, |
|            the environment (except for the variables TERM, DISPLAY and _ |
| ) and  the                                                               |
|            umask  are  retained  from  the time of invocation. An at -  |
| or batch -                                                               |
|            command invoked from a su(1) shell will retain the current us |
| erid. The                                                               |
|            user  will  be  mailed standard error and standard output fro |
| m his com-                                                               |
|            mands, if any. Mail will be sent using the command /usr/sbin |
| /sendmail. |
|            If at is executed from a su(1) shell, the owner of the login  |
| shell will                                                               |
|            receive the mail. |
|                                                                          |
|            The superuser may use these commands in any  case. For  oth |
| er  users, |
|            permission  to  use  at  is  determined  by the files /etc/at |
| .allow and                                                               |
|            /etc/at.deny. |
|                                                                          |
|            If the file /etc/at.allow exists, only usernames mentioned  i |
| n  it  are                                                               |
|            allowed to use at. |
|                                                                          |
|            If  /etc/at.allow  does not exist, /etc/at.deny is checked, e |
| very user-                                                               |
|            name not mentioned in it is then allowed to use at. |
|                                                                          |
|            If neither exists, only the superuser is allowed use of at. |
|                                                                          |
|            An empty /etc/at.deny means that every user is allowed use  t |
| hese  com-                                                               |
|            mands, this is the default configuration. |
|                                                                          |
|     OPTIONS                                                              |
|            -V      prints the version number to standard error. |
|                                                                          |
|            -q queue                                                      |
|                uses  the  specified  queue. A queue designation consist |
| s of a                                                                   |
|                single letter; valid queue designations range from a to z |
| . and                                                                   |
|                A  to Z. The a queue is the default for at and the b que |
| ue for                                                                   |
|                batch. Queues with higher letters run with increased nic |
| eness. |
|                The  special queue "=" is reserved for jobs which are cur |
| rently                                                                   |
|                running. |
|                                                                          |
|            If a job is submitted to a queue designated with an  uppercas |
| e  letter, |
|            the  job is treated as if it were submitted to batch at the t |
| ime of the                                                               |
|            job. Once the time is reached, the batch processing rules wi |
| th respect                                                               |
|            to  load average apply. If atq is given a specific queue, it |
|  will only                                                               |
|            show jobs pending in that queue. |
|                                                                          |
|            -m      Send mail to the user when the job has completed even |
|  if  there                                                               |
|                was no output. |
|                                                                          |
|            -M      Never send mail to the user. |
|                                                                          |
|            -f file Reads the job from file rather than standard input. |
|                                                                          |
|            -l      Is an alias for atq. |
|                                                                          |
|            -r      Is an alias for atrm. |
|                                                                          |
|            -d      Is an alias for atrm. |
|                                                                          |
|                                                                          |
|            -v      Shows  the  time the job will be executed before read |
| ing                                                                      |
|                the job. |
|                                                                          |
|            Times displayed will be in  the  format  "Thu  Feb  20  14:50 |
| :00                                                                      |
|            1997". |
|                                                                          |
|            -c     cats the jobs listed on the command line to standard o |
| ut-                                                                      |
|               put. |
|                                                                          |
|            -t time_arg                                                   |
|               Submit the job to be run at the  time  specified  by  the  |
|               time_arg option argument, which must have the same format  |
|               as specified for the touch(1) utility's  -t  time  option  |
|               argument ([[CC]YY]MMDDhhmm). |
|                                                                          |
|     ENVIRONMENT                                                          |
|            SHELL   The  value of the SHELL environment variable at the t |
| ime                                                                      |
|                of at invocation will determine which shell is  used  to  |
|                execute  the  at job commands. If SHELL is unset when at  |
|                is invoked, the user's login shell will be used; other-  |
|                wise, if  SHELL  is  set  when  at  is invoked, it must  |
|                contain the path of a shell interpreter executable  that  |
|                will  be used to run the commands at the specified time. |
|                                                                          |
|            at will record the values of environment  variables  present  |
|  at                                                                      |
|            time  of at invocation. When the commands are run at the  spe |
| ci-                                                                      |
|            fied time, at will restore these  variables  to  their  recor |
| ded                                                                      |
|            values  . These variables are excluded from this processing  |
| and                                                                      |
|            are never set by at when the commands are run : |
|            TERM, DISPLAY, SHELLOPTS, _, PPID, BASH_VERSINFO, EUID, U |
| ID, |
|            GROUPS. |
|            If  the  user submitting the at job is not the super-user, va |
| ri-                                                                      |
|            ables that alter the behaviour of the loader ld.so(8), such  |
|  as                                                                      |
|            LD_LIBRARY_PATH , cannot be recorded and restored by at . |
|                                                                          |
|                                                                          |
|     FILES                                                                |
|            /var/spool/at                                                 |
|            /var/spool/at/spool                                           |
|            /proc/loadavg                                                 |
|            /var/run/utmp                                                 |
|            /etc/at.allow                                                 |
|            /etc/at.deny                                                  |
|                                                                          |
|     SEE ALSO                                                             |
|            cron(1), nice(1), sh(1), umask(2), atd(8). |
|                                                                          |
|     BUGS                                                                 |
|            The correct operation of batch for Linux depends on the prese |
| nce                                                                      |
|            of a proc- type directory mounted on /proc. |
|                                                                          |
|            If the file /var/run/utmp is not available or corrupted, or  |
|  if                                                                      |
|            the user is not logged on at the time at is invoked, the mail |
|  is                                                                      |
|            sent to the userid found in the  environment  variable  LOGNA |
| ME. |
|            If that is undefined or empty, the current userid is assumed. |
|                                                                          |
|            At  and  batch  as  presently  implemented are not suitable w |
| hen                                                                      |
|            users are competing for resources. If this is the case for y |
| our                                                                      |
|            site, you  might want to consider another batch system, such |
|  as                                                                      |
|            nqs. |
|                                                                          |
|     AUTHOR                                                               |
|            At  was  mostly  written  by  Thomas  Koenig, ig25@rz.uni-ka |
| rl-                                                                      |
|            sruhe.de. |
|                                                                          |
|                                                                          |
|                                                                          |
|     local                  Nov 1996              AT(1)                   |
+--------------------------------------------------------------------------+


