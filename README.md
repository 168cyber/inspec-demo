# Demo

## Basic Use
For simplicity I will use Chef's Learn Inspec Environment

1. Download Docker Compose file for demo environment  
`curl -o docker-compose.yml https://raw.githubusercontent.com/learn-chef/inspec/master/docker-compose.yml`  
2. Start the environment  
`docker-compose up -d`
3. Connect to the "workstation" container  
`docker exec -it workstation bash`
4. Verify that the auditd package is not installed.  
`dpkg -s auditd | grep Status`
5. Clone the basic profile  
`git clone https://github.com/learn-chef/auditd.git`  
`tree auditd`  
`cat auditd/controls/example.rb`   
6. Run the profile against the system. This will return a failure from Inspec.  
`inspec exec /root/auditd`  
7. Remediate this issue by installing auditd  
`apt-get install -y auditd`
8. Rerun the profile. This will return 1 success from Inspec.  
`inspec exec /root/auditd` 
9. Run it on a remote system.  
`inspec exec auditd -t ssh://root:password@target`  
10. Change the output to json  
`inspec exec auditd -t ssh://root:password@target --reporter=json | jq .`
11. Run a more complex profile directly from GitHub  
`inspec exec https://github.com/dev-sec/linux-baseline.git -t ssh://root:password@target`# inspec-demo
