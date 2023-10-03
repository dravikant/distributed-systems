### why failure detection is important

Mean Time To Failure (MTTF) is the average amount of time that a device or system will operate before failing. It is calculated by dividing the total operating time of all devices or systems by the number of failures that occur during that time.

The MTTF of a system is inversely proportional to the number of components in the system. This is because the more components you have, the more likely it is that one of them will fail.

If you have one server with a 10-year failure rate, then the MTTF of the system is 10 years.
If you have two servers with a 10-year failure rate, then the MTTF of the system is 5 years.
If you have 12,000 servers with a 10-year failure rate, then the MTTF of the system is 7.2 hours.

MTTF_system = 10 years / 12000 servers = 0.00083 years

MTTF_system = 0.00083 years * 365 days/year * 24 hours/day = 7.2 hours


so as number of servers increase, it is important to build program to auto detect failures

- Server may have failure, and we need to implement the failure detectors.

- Process "group-based" system
    
    - Clouds/Datacenters

    - Replicated servers

    - Distributed databases

- Crash-stop/ Failure-stop  failures (and do not recover)

- Each process in group of processes, we have a membership list which contains the process in your system and not-yet failed(non-faulty processes)


- Membership protocol:
    
    - Keep the membership list up to date

        - as the processes join the group

        - as the processes leave the group (they update while leaving)

        - as the processes failed silently (do not update)

- Sub-protocols

   

    - Failue Detectors -- detect failures

     - Disseminations -- spread information (join/leave)



We are looking at algo which will eventually be consistent.