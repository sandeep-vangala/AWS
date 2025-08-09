# AWS
AWS scenario based questions
AWS migration evaluator
**AWS Application Migration Service (AWS MGN) benefits:**
**Flexible**
1) migrate from any source
2) wide range of OS, application and database support
3) suitable for large scale migration
**Reliable**
1) Robust, predictable, non-disruptive continuous replication
2) short cutover windows with minimal downtime
3) highly secure
**Highly Automated**
1) Minimal skill set required to operate.
2) Easy, non-disruptive tests prior to cutover.
3) Easily plugs into migration factories and cloud COEs.

1) we install AWS replication agent on the on-prem server, upon installation agent performs authentication handshake against AWS MGN API enpoint which is encrypted with TLS1.3 which registers agent with service which inturn automatically provision staging area resources. Every source disk replicated MGN creates identical EBS volumes in the staging area subnet for the data sysnchronization to occur. After EBS is created, data is encrypted and replicated from source servers to the staging area EBS volumes. The service automatically created scaling of the resources. After that review the launch settings, wd can chose test and cutover settings and launch instances, the service automatically spins up a conversion server(specifically used during launch process and immediatley terminated).
2) After the conversion is complete, after the launch, newly created volumes volumes won't be in sync with the source servers. any changes made to the source servers will be replicated to the staging servers, but the changes are not appliede to the launched instances. whenever you create a test/cutover ec2 instance, it will reflect the most recent state of the data replicated from the satging area subnet. with this design, we can test spun up instances without disrupting the source servers/replication process.

<img width="2880" height="1646" alt="image" src="https://github.com/user-attachments/assets/06367091-677c-4247-ba53-0981264b14ba" />



3) <img width="576" height="888" alt="image" src="https://github.com/user-attachments/assets/588ba154-fe10-4bdc-af64-3367a1978f25" />

<img width="2896" height="1608" alt="image" src="https://github.com/user-attachments/assets/64f3f540-76d6-4dd6-bb42-95feff473797" />

4) To establish the connectivity between source servers and AWS MGN endpoints, allow for connectivity on Port 443 AWS replication agent on source servers and AWS MGN endpoint, this connectivity used for authentication, connectivity and monitoring purpose.
5) AWS replication agent sends data directly from source servers to replication servers on port 1500.
6) replication replication servers should be coonected to MGN enpoints for authentication, connectivity and monitoring purpose as long as replication is in progress.

7) <img width="2884" height="1626" alt="image" src="https://github.com/user-attachments/assets/b94a56b6-9a5d-4247-8808-b01b645d7b3c" />
