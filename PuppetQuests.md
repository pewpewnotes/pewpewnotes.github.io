```text


 ____                         _      ___                  _       
|  _ \ _   _ _ __  _ __   ___| |_   / _ \ _   _  ___  ___| |_ ___ 
| |_) | | | | '_ \| '_ \ / _ \ __| | | | | | | |/ _ \/ __| __/ __|
|  __/| |_| | |_) | |_) |  __/ |_  | |_| | |_| |  __/\__ \ |_\__ \
|_|    \__,_| .__/| .__/ \___|\__|  \__\_\\__,_|\___||___/\__|___/
            |_|   |_|                                             


```

### == Welcome ==

```text
[vagrant@learning ~]$ quest begin welcome
Please wait a moment while the welcome quest is set up...
You have started the welcome quest.
[vagrant@learning ~]$ quest --help
NAME
    quest - Track the status of quests and tasks.

SYNOPSIS
    quest [global options] command [command options] [arguments...]

GLOBAL OPTIONS
    --help - Show this message

COMMANDS
    begin  - Begin a quest
    help   - Shows a list of commands or help for one command
    list   - List available quests
    status - Show status of the current quest
[vagrant@learning ~]$ quest status
Quest: welcome
X Task 1: View the options for the quest tool
X Task 2: View the list of available quests
[vagrant@learning ~]$ quest status
Quest: welcome
X Task 1: View the options for the quest tool
X Task 2: View the list of available quests
[vagrant@learning ~]$ 
```
### == Hello Bolt ==

```text
[vagrant@learning ~]$ rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
error: can't create transaction lock on /var/lib/rpm/.rpm.lock (Permission denied)
[vagrant@learning ~]$ sudo rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:puppet6-release-6.0.0-1.el7      ################################# [100%]
[vagrant@learning ~]$ sudo yum install puppet-bolt
Loaded plugins: fastestmirror, priorities
Repository 'local' is missing name in configuration, using id
Determining fastest mirrors
local                                                                          | 2.9 kB  00:00:00     
puppet6                                                                        | 2.5 kB  00:00:00     
puppet6/x86_64/primary_db                                                      | 322 kB  00:00:00     
87 packages excluded due to repository priority protections
Resolving Dependencies
--> Running transaction check
---> Package puppet-bolt.x86_64 0:1.14.0-1.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                   Arch                 Version                     Repository           Size
======================================================================================================
Installing:
 puppet-bolt               x86_64               1.14.0-1.el7                local                27 M

Transaction Summary
======================================================================================================
Install  1 Package

Total download size: 27 M
Installed size: 91 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Warning: RPMDB altered outside of yum.
  Installing : puppet-bolt-1.14.0-1.el7.x86_64                                                    1/1 
  Verifying  : puppet-bolt-1.14.0-1.el7.x86_64                                                    1/1 

Installed:
  puppet-bolt.x86_64 0:1.14.0-1.el7                                                                   

Complete!
[vagrant@learning ~]$ bolt --help
Usage: bolt <subcommand> <action> [options]

Available subcommands:
  bolt command run <command>       Run a command remotely
  bolt file upload <src> <dest>    Upload a local file
  bolt script run <script>         Upload a local script and run it remotely
  bolt task show                   Show list of available tasks
  bolt task show <task>            Show documentation for task
  bolt task run <task> [params]    Run a Puppet task
  bolt plan show                   Show list of available plans
  bolt plan show <plan>            Show details for plan
  bolt plan run <plan> [params]    Run a Puppet task plan
  bolt apply <manifest>            Apply Puppet manifest code
  bolt puppetfile install          Install modules from a Puppetfile into a Boltdir
  bolt puppetfile show-modules     List modules available to Bolt

Run `bolt <subcommand> --help` to view specific examples.

where [options] are:
    -n, --nodes NODES                Identifies the nodes to target.
                                     Enter a comma-separated list of node URIs or group names.
                                     Or read a node list from an input file '@<file>' or stdin '-'.
                                     Example: --nodes localhost,node_group,ssh://nix.com:23,winrm://windows.puppet.com
                                     URI format is [protocol://]host[:port]
                                     SSH is the default protocol; may be ssh, winrm, pcp, local, docker, remote
                                     For Windows nodes, specify the winrm:// protocol if it has not be configured
                                     For SSH, port defaults to `22`
                                     For WinRM, port defaults to `5985` or `5986` based on the --[no-]ssl setting
    -q, --query QUERY                Query PuppetDB to determine the targets
        --noop                       Execute a task that supports it in noop mode
        --description DESCRIPTION    Description to use for the job
        --params PARAMETERS          Parameters to a task or plan as json, a json file '@<file>', or on stdin '-'
Authentication:
    -u, --user USER                  User to authenticate as
    -p, --password [PASSWORD]        Password to authenticate with. Omit the value to prompt for the password.
        --private-key KEY            Private ssh key to authenticate with
        --[no-]host-key-check        Check host keys with SSH
        --[no-]ssl                   Use SSL with WinRM
        --[no-]ssl-verify            Verify remote host SSL certificate with WinRM
Escalation:
        --run-as USER                User to run as using privilege escalation
        --sudo-password [PASSWORD]   Password for privilege escalation. Omit the value to prompt for the password.
Run context:
    -c, --concurrency CONCURRENCY    Maximum number of simultaneous connections (default: 100)
        --compile-concurrency CONCURRENCY
                                     Maximum number of simultaneous manifest block compiles (default: number of cores)
    -m, --modulepath MODULES         List of directories containing modules, separated by ':'
        --boltdir FILEPATH           Specify what Boltdir to load config from (default: autodiscovered from current working dir)
        --configfile FILEPATH        Specify where to load config from (default: ~/.puppetlabs/bolt/bolt.yaml)
    -i, --inventoryfile FILEPATH     Specify where to load inventory from (default: ~/.puppetlabs/bolt/inventory.yaml)
Transports:
        --transport TRANSPORT        Specify a default transport: ssh, winrm, pcp, local, docker, remote
        --connect-timeout TIMEOUT    Connection timeout (defaults vary)
        --[no-]tty                   Request a pseudo TTY on nodes that support it
        --tmpdir DIR                 The directory to upload and execute temporary files on the target
Display:
        --format FORMAT              Output format to use: human or json
        --[no-]color                 Whether to show output in color
    -h, --help                       Display help
    -v, --verbose                    Display verbose logging
        --debug                      Display debug logging
        --trace                      Display error stack traces
        --version                    Display the version
[vagrant@learning ~]$ bolt --version
1.14.0
[vagrant@learning ~]$ bolt command run 'free -th' --nodes localhost
Started on localhost...
Finished on localhost:
  STDOUT:
                  total        used        free      shared  buff/cache   available
    Mem:           3.7G        1.3G        1.3G         42M        1.1G        2.0G
    Swap:          1.0G          0B        1.0G
    Total:         4.7G        1.3G        2.3G
Successful on 1 node: localhost
Ran on 1 node in 0.40 seconds
[vagrant@learning ~]$ rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
^C
[vagrant@learning ~]$ ^C
[vagrant@learning ~]$ bolt command run hostname --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Failed on bolt.puppet.vm:
  Failed to connect to docker://bolt.puppet.vm: Permission denied - connect(2) for /var/run/docker.sock (Errno::EACCES)
Failed on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.04 seconds
[vagrant@learning ~]$ sudo bolt command run hostname --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Finished on bolt.puppet.vm:
  STDOUT:
    bolt.puppet.vm
Successful on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.35 seconds
[vagrant@learning ~]$ sudo bolt command run 'cat /etc/hosts' --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Finished on bolt.puppet.vm:
  STDOUT:
    127.0.0.1	localhost
    ::1	localhost ip6-localhost ip6-loopback
    fe00::0	ip6-localnet
    ff00::0	ip6-mcastprefix
    ff02::1	ip6-allnodes
    ff02::2	ip6-allrouters
    172.18.0.1	learning.puppetlabs.vm puppet
    172.18.0.2	bolt.puppet.vm bolt
Successful on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.31 seconds
[vagrant@learning ~]$ sudo bolt --format json command run 'cat /etc/hosts' --nodes docker://bolt.pup>
{ "items": [
{"node":"docker://bolt.puppet.vm","status":"success","result":{"stdout":"127.0.0.1\tlocalhost\n::1\tlocalhost ip6-localhost ip6-loopback\nfe00::0\tip6-localnet\nff00::0\tip6-mcastprefix\nff02::1\tip6-allnodes\nff02::2\tip6-allrouters\n172.18.0.1\tlearning.puppetlabs.vm puppet\n172.18.0.2\tbolt.puppet.vm bolt\n","stderr":"","exit_code":0}}
],
"node_count": 1, "elapsed_time": 0 }
[vagrant@learning ~]$ which jq                                                                            
/usr/bin/jq
[vagrant@learning ~]$ sudo bolt --format json command run 'cat /etc/hosts' --nodes docker://bolt.puppet.vm | jq .
{
  "items": [
    {
      "node": "docker://bolt.puppet.vm",
      "status": "success",
      "result": {
        "stdout": "127.0.0.1\tlocalhost\n::1\tlocalhost ip6-localhost ip6-loopback\nfe00::0\tip6-localnet\nff00::0\tip6-mcastprefix\nff02::1\tip6-allnodes\nff02::2\tip6-allrouters\n172.18.0.1\tlearning.puppetlabs.vm puppet\n172.18.0.2\tbolt.puppet.vm bolt\n",
        "stderr": "",
        "exit_code": 0
      }
    }
  ],
  "node_count": 1,
  "elapsed_time": 0
}
[vagrant@learning ~]$ quest status
Quest: hello_bolt
√ Task 1: Install bolt
X Task 2: Verify the bolt tool installation
X Task 3: Execute bolt commands
[vagrant@learning ~]$ bolt --version
1.14.0
[vagrant@learning ~]$ quest status  
Quest: hello_bolt
√ Task 1: Install bolt
X Task 2: Verify the bolt tool installation
X Task 3: Execute bolt commands
[vagrant@learning ~]$     status - Show status of the current quest
r
-bash: status: command not found
[vagrant@learning ~]$ ^C
-bash: :s^C: substitution failed
[vagrant@learning ~]$ [vagrant@learning ~]$ ^C

-bash: [vagrant@learning: command not found
[vagrant@learning ~]$ [vagrant@learning ~]$ ^C
 
-bash: [vagrant@learning: command not found
[vagrant@learning ~]$ [vagrant@learning ~]$ ^C
 
-bash: [vagrant@learning: command not found
[vagrant@learning ~]$ [vagrant@learning ~]$ rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
-bash: [vagrant@learning: command not found
d
[vagrant@learning ~]$ Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
-bash: Retrieving: command not found
n
[vagrant@learning ~]$ error: can't create transaction lock on /var/lib/rpm/.rpm.lock (Permission denied)
[vagrant@learning ~]$ sudo rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:puppet6-release-6.0.0-1.el7      ################################# [100%]
[vagrant@learning ~]$ sudo yum install puppet-bolt
Loaded plugins: fastestmirror, priorities
Repository 'local' is missing name in configuration, using id
Determining fastest mirrors
local                                                                          | 2.9 kB  00:00:00     
puppet6                                                                        | 2.5 kB  00:00:00     
puppet6/x86_64/primary_db                                                      | 322 kB  00:00:00     
87 packages excluded due to repository priority protections
Resolving Dependencies
--> Running transaction check
---> Package puppet-bolt.x86_64 0:1.14.0-1.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

======================================================================================================
 Package                   Arch                 Version                     Repository           Size
======================================================================================================
Installing:
 puppet-bolt               x86_64               1.14.0-1.el7                local                27 M

Transaction Summary
======================================================================================================
Install  1 Package

Total download size: 27 M
Installed size: 91 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Warning: RPMDB altered outside of yum.
  Installing : puppet-bolt-1.14.0-1.el7.x86_64                                                    1/1 
  Verifying  : puppet-bolt-1.14.0-1.el7.x86_64                                                    1/1 

Installed:
  puppet-bolt.x86_64 0:1.14.0-1.el7                                                                   

Complete!
[vagrant@learning ~]$ bolt --help
Usage: bolt <subcommand> <action> [options]

Available subcommands:
  bolt command run <command>       Run a command remotely
  bolt file upload <src> <dest>    Upload a local file
  bolt script run <script>         Upload a local script and run it remotely
  bolt task show                   Show list of available tasks
  bolt task show <task>            Show documentation for task
  bolt task run <task> [params]    Run a Puppet task
  bolt plan show                   Show list of available plans
  bolt plan show <plan>            Show details for plan
  bolt plan run <plan> [params]    Run a Puppet task plan
  bolt apply <manifest>            Apply Puppet manifest code
  bolt puppetfile install          Install modules from a Puppetfile into a Boltdir
  bolt puppetfile show-modules     List modules available to Bolt

Run `bolt <subcommand> --help` to view specific examples.

where [options] are:
    -n, --nodes NODES                Identifies the nodes to target.
                                     Enter a comma-separated list of node URIs or group names.
                                     Or read a node list from an input file '@<file>' or stdin '-'.
                                     Example: --nodes localhost,node_group,ssh://nix.com:23,winrm://windows.puppet.com
                                     URI format is [protocol://]host[:port]
                                     SSH is the default protocol; may be ssh, winrm, pcp, local, docker, remote
                                     For
                           
                        
    -q, --query QUERY   
        --noop                       Execute a task that supports it in noop mode
        --d
        --params PARAMETERS          Parameters to a task or plan as json
Authentication:
    -u, --user USER                  User to authenticate as
    -p, --password [PASSWORD]        Password to authenticate with. Omit the value to prompt for the password.
        --private-key KEY            Private ssh key to authenticate with
        --[no-]host-key-check        Check host keys with SSH
        --[no-]ssl                   Use SSL with WinRM
        --[no-]ssl-verify            Verify remote host SSL certificate with WinRM
Escalation:
        --run-as USER                User to run as using privilege escalation
        --sudo-password [PASSWORD]   Password for privilege escalation. Omit the value to prompt for the password.
Run context:
    -c, --concurrency CONCURRENCY    Maximum number of simultaneous connections (default: 100)
        --compile-concurrency CONCURRENCY
                                     Maximum number of simultaneous manifest block compiles (default: number of cores)
    -m, --modulepath MODULES         List of directories containing modules, separated by ':'
        --boltdir FILEPATH           Specify what Boltdir to load config from (default: autodiscovered from current working dir)
        --configfile FILEPATH        Specify where to load config from (default: ~/.puppetlabs/bolt/bolt.yaml)
    -i, --inventoryfile FILEPATH     Specify where to load inventory from (default: ~/.puppetlabs/bolt/inventory.yaml)
Transports:
        --transport TRANSPORT        Specify a default transport: ssh, winrm, pcp, local, docker, remote
        --connect-timeout TIMEOUT    Connection timeout (defaults vary)
        --[no-]tty                   Request a pseudo TTY on nodes that support it
        --tmpdir DIR                 The directory to upload and execute temporary files on the target
Display:
        --format FORMAT              Output format to use: human or json
        --[no-]color                 Whether to show output in color
    -h, --help                       Display help
    -v, --verbose                    Display verbose logging
        --debug                      Display debug logging
        --trace                      Display error stack traces
        --version                    Display the version
[vagrant@learning ~]$ bolt --version
1.14.0
[vagrant@learning ~]$ bolt command run 'free -th' --nodes localhost
Started on localhost...
Finished on localhost:
  STDOUT:
                  total        used        free      shared  buff/cache   available
    Mem:           3.7G        1.3G        1.3G         42M        1.1G        2.0G
    Swap:          1.0G          0B        1.0G
    Total:         4.7G        1.3G        2.3G
Successful on 1 node: localhost
Ran on 1 node in 0.40 seconds
[vagrant@learning ~]$ rpm -Uvh https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
Retrieving https://yum.puppet.com/puppet6/puppet6-release-el-7.noarch.rpm
^C
[vagrant@learning ~]$ ^C
[vagrant@learning ~]$ bolt command run hostname --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Failed on bolt.puppet.vm:
  Failed to connect to docker://bolt.puppet.vm: Permission denied - connect(2) for /var/run/docker.sock (Errno::EACCES)
Failed on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.04 seconds
[vagrant@learning ~]$ sudo bolt command run hostname --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Finished on bolt.puppet.vm:
  STDOUT:
    bolt.puppet.vm
Successful on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.35 seconds
[vagrant@learning ~]$ sudo bolt command run 'cat /etc/hosts' --nodes docker://bolt.puppet.vm
Started on bolt.puppet.vm...
Finished on bolt.puppet.vm:
  STDOUT:
    127.0.0.1localhost
    ::1localhost ip6-localhost ip6-loopback
    fe00::0ip6-localnet
    ff00::0ip6-mcastprefix
    ff02::1ip6-allnodes
    ff02::2ip6-allrouters
    172.18.0.1learning.puppetlabs.vm puppet
    172.18.0.2bolt.puppet.vm bolt
Successful on 1 node: docker://bolt.puppet.vm
Ran on 1 node in 0.31 seconds
[vagrant@learning ~]$ sudo bolt --format json command run 'cat /etc/hosts' --nodes docker://bolt.pup>
{ "items": [
00::0\tip6-localnet\nff00::0\tip6-mcastprefix\nff02::1\tip6-allnodes\nff02::2\tip6-allrouters\n172.18.0.1\tlearning.puppetlabs.vm puppet\n172.18.0.2\tbolt.puppet.vm bolt\n","stderr":"","exit_code":0}}       
],
"node_count": 1, "elapsed_time": 0 }
[vagrant@learning ~]$ which jq                                                                            
/usr/bin/jq
[vagrant@learning ~]$ sudo bolt --format json command run 'cat /etc/hosts' --nodes docker://bolt.puppet.vm | jq .
{
  "items": [
    {
      "node": "docker://bolt.puppet.vm",
      "status": "success",
      "result": {
ip6-loopback\nfe00::0\tip6-localnet\nff00::0\tip6-mcastprefix\nff02::1\tip6-allnodes\nff02::2\tip6-allrouters\n172.18.0.1\tlearning.puppetlabs.vm puppet\n172.18.0.2\tbolt.puppet.vm bolt\n",                  
        "stderr": "",
        "exit_code": 0
      }
    }
  ],
  "node_count": 1,
  "elapsed_time": 0
}
[vagrant@learning ~]$ quest status
Quest: hello_bolt
√ Task 1: Install bolt
X Task 2: Verify the bolt tool installation
X Task 3: Execute bolt commands
[vagrant@learning ~]$ bolt --version
1.14.0
[vagrant@learning ~]$ quest status  
Quest: hello_bolt
√ Task 1: Install bolt
X Task 2: Verify the bolt tool installation
X Task 3: Execute bolt commands
[vagrant@learning ~]$ 

``` 
### == Hello Puppet ==
```text
[vagrant@learning ~]$ quest begin hello_puppet
Please wait a moment while the hello_puppet quest is set up...
-You have started the hello_puppet quest.
[vagrant@learning ~]$ ls
[vagrant@learning ~]$ sudo bolt format json command run "sh -c 'curl -k https://learning.puppetlabs.vm:8140/packages/current/install.bash | sudo bash'" --nodes docker://hello.puppet.vm
Expected subcommand 'format' to be one of command, script, task, plan, file, puppetfile, apply
[vagrant@learning ~]$ sudo bolt json command run "sh -c 'curl -k https://learning.puppetlabs.vm:8140/packages/current/install.bash | sudo bash'" --nodes docker://hello.puppet.vm
Expected subcommand 'json' to be one of command, script, task, plan, file, puppetfile, apply
[vagrant@learning ~]$ sudo bolt command run "sh -c 'curl -k https://learning.puppetlabs.vm:8140/packages/current/install.bash | sudo bash'" --nodes docker://hello.puppet.vm
Started on hello.puppet.vm...
Finished on hello.puppet.vm:
  STDERR:
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0curl: (7) Failed connect to learning.puppetlabs.vm:8140; Connection refused
Successful on 1 node: docker://hello.puppet.vm
Ran on 1 node in 0.40 seconds
[vagrant@learning ~]$ sudo bolt command run "sh -c 'curl -k https://learning.puppetlabs.vm:8140/packages/current/install.bash | sudo bash'" --nodes docker://hello.puppet.vm
Started on hello.puppet.vm...
Finished on hello.puppet.vm:
  STDERR:
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0curl: (7) Failed connect to learning.puppetlabs.vm:8140; Connection refused
Successful on 1 node: docker://hello.puppet.vm
Ran on 1 node in 0.26 seconds
[vagrant@learning ~]$ service pe-puppetserver restart
Redirecting to /bin/systemctl restart pe-puppetserver.service
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to manage system services or units.
Authenticating as: root
Password: 
polkit-agent-helper-1: pam_authenticate failed: Authentication failure
==== AUTHENTICATION FAILED ===
Failed to restart pe-puppetserver.service: Access denied
See system logs and 'systemctl status pe-puppetserver.service' for details.
[vagrant@learning ~]$ sudo service pe-puppetserver restart
Redirecting to /bin/systemctl restart pe-puppetserver.service


[vagrant@learning ~]$ 
[vagrant@learning ~]$ 
[vagrant@learning ~]$ sudo bolt command run "sh -c 'curl -k https://learning.puppetlabs.vm:8140/packages/current/install.bash | sudo bash'" --nodes docker://hello.puppet.vm
Started on hello.puppet.vm...

Finished on hello.puppet.vm:
  STDOUT:
    bulk downloading plugins
    extracting plugins
    Loaded plugins: fastestmirror, ovl
    Cleaning repos: pe_repo
    Cleaning up list of fastest mirrors
    Other repos take up 113 M of disk space (use --verbose for details)
    Loaded plugins: fastestmirror, ovl
    Loaded plugins: fastestmirror, ovl
    Determining fastest mirrors
    Resolving Dependencies
    --> Running transaction check
    ---> Package puppet-agent.x86_64 0:6.0.5-1.el7 will be installed
    --> Finished Dependency Resolution
    
    Dependencies Resolved
    
    ================================================================================
     Package              Arch           Version              Repository       Size
    ================================================================================
    Installing:
     puppet-agent         x86_64         6.0.5-1.el7          pe_repo          22 M
    
    Transaction Summary
    ================================================================================
    Install  1 Package
    
    Total download size: 22 M
    Installed size: 93 M
    Downloading packages:
    Public key for puppet-agent-.0.5-1.el7.x86_64.rpm is not installed
    Retrieving key from https://learning.puppetlabs.vm:8140/packages/GPG-KEY-puppetlabs
    Retrieving key from https://learning.puppetlabs.vm:8140/packages/GPG-KEY-puppet
    Running transaction check
    Running transaction test
    Transaction test succeeded
    Running transaction
      Installing : puppet-agent-6.0.5-1.el7.x86_64                              1/1 
      Verifying  : puppet-agent-6.0.5-1.el7.x86_64                              1/1 
    
    Installed:
      puppet-agent.x86_64 0:6.0.5-1.el7                                             
    
    Complete!
    service { 'puppet':
      ensure => 'stopped',
    }
    Notice: /Service[puppet]/ensure: ensure changed 'stopped' to 'running'
    service { 'puppet':
      ensure => 'running',
      enable => 'true',
    }
    Notice: /File[/usr/local/bin/facter]/ensure: created
    file { '/usr/local/bin/facter':
      ensure => 'link',
      target => '/opt/puppetlabs/puppet/bin/facter',
    }
    Notice: /File[/usr/local/bin/puppet]/ensure: created
    file { '/usr/local/bin/puppet':
      ensure => 'link',
      target => '/opt/puppetlabs/puppet/bin/puppet',
    }
    Notice: /File[/usr/local/bin/pe-man]/ensure: created
    file { '/usr/local/bin/pe-man':
      ensure => 'link',
      target => '/opt/puppetlabs/puppet/bin/pe-man',
    }
    Notice: /File[/usr/local/bin/hiera]/ensure: created
    file { '/usr/local/bin/hiera':
      ensure => 'link',
      target => '/opt/puppetlabs/puppet/bin/hiera',
    }
  STDERR:
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
100 25627  100 25627    0     0  44249      0 --:--:-- --:--:-- --:--:-- 44337
    Repository 'local' is missing name in configuration, using id
    + yum list installed puppet-agent
    Repository 'local' is missing name in configuration, using id
    Error: No matching Packages to list
    + yum install -y puppet-agent-6.0.5
    Repository 'local' is missing name in configuration, using id
    warning: /var/cache/yum/x86_64/7/pe_repo/packages/puppet-agent-6.0.5-1.el7.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID ef8d349f: NOKEY
    Importing GPG key 0x4BD6EC30:
     Userid     : "Puppet Labs Release Key (Puppet Labs Release Key) <info@puppetlabs.com>"
     Fingerprint: 47b3 20eb 4c7c 375a a9da e1a0 1054 b7a2 4bd6 ec30
     From       : https://learning.puppetlabs.vm:8140/packages/GPG-KEY-puppetlabs
    Importing GPG key 0xEF8D349F:
     Userid     : "Puppet, Inc. Release Key (Puppet, Inc. Release Key) <release@puppet.com>"
     Fingerprint: 6f6b 1550 9cf8 e59e 6e46 9f32 7f43 8280 ef8d 349f
     From       : https://learning.puppetlabs.vm:8140/packages/GPG-KEY-puppet
    + set +x
Successful on 1 node: docker://hello.puppet.vm
Ran on 1 node in 201.67 seconds
[vagrant@learning ~]$ 
[vagrant@learning ~]$ quest list
welcome
portfolio_introduction
hello_bolt
hello_puppet
agent_run
manifests_and_classes
package_file_service
variables_and_templates
class_parameters
facts
conditional_statements
the_forge
roles_and_profiles
hiera
defined_resource_types
control_repository
puppetfile
[vagrant@learning ~]$ quest status
Quest: hello_puppet
√ Task 1: Install the Puppet agent
X Task 2: Investigate the /tmp/test file resource
X Task 3: Create the /tmp/test file resource
X Task 4: Change the content of the /tmp/test file resource
X Task 5: Investigate the package provider
[vagrant@learning ~]$ ssh learning@hello.puppet.vm
Warning: Permanently added 'hello.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@hello.puppet.vm's password: 
[~]
learning@hello: $ ls
[~]
learning@hello: $ sudo puppet resource /tmp/test
Error: Could not run: Could not find type /tmp/test
[~]
learning@hello: $ sudo puppet resource file /tmp/test
file { '/tmp/test':
  ensure => 'absent',
}
[~]
learning@hello: $ touch /tmp/test
[~]
learning@hello: $ sudo puppet resource file /tmp/test
file { '/tmp/test':
  ensure  => 'file',
  content => '{md5}d41d8cd98f00b204e9800998ecf8427e',
  ctime   => '2020-08-26 12:32:22 +0000',
  group   => 1000,
  mode    => '0664',
  mtime   => '2020-08-26 12:32:22 +0000',
  owner   => 1000,
  type    => 'file',
}
[~]
learning@hello: $ sudo puppet resource file /tmp/test content='Hello Puppet!'
Notice: /File[/tmp/test]/content: content changed '{md5}d41d8cd98f00b204e9800998ecf8427e' to '{md5}6fa6ce40c758db2a5b07537feb98f8e1'
file { '/tmp/test':
  ensure  => 'file',
  content => '{md5}6fa6ce40c758db2a5b07537feb98f8e1',
}
[~]
learning@hello: $ sudo puppet resource package httpd
package { 'httpd':
  ensure => 'purged',
}
[~]
learning@hello: $ https://www.youtube.com/watch?v=pEaBqiLeCu0
-bash: https://www.youtube.com/watch?v=pEaBqiLeCu0: No such file or directory
[~]
learning@hello: $ sudo puppet resource package bogus-package ensure=present
Error: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
Error: /Package[bogus-package]/ensure: change from 'purged' to 'present' failed: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
package { 'bogus-package':
  ensure => 'purged',
}
[~]
learning@hello: $ sudo puppet resource package bogus-package ensure=present
Error: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
Error: /Package[bogus-package]/ensure: change from 'purged' to 'present' failed: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
package { 'bogus-package':
  ensure => 'purged',
}
[~]
learning@hello: $ sudo puppet resource package bogus-package ensure=present
Error: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
Error: /Package[bogus-package]/ensure: change from 'purged' to 'present' failed: Execution of '/bin/yum -d 0 -e 0 -y install bogus-package' returned 1: Error: Nothing to do
package { 'bogus-package':
  ensure => 'purged',
}
[~]
learning@hello: $ sudo puppet resource package httpd ensure=present
Notice: /Package[httpd]/ensure: created
package { 'httpd':
  ensure => '2.4.6-89.el7.centos',
}
[~]
learning@hello: $ exit
6

```
This one had an issue, had to restart the service to resolve it.

### == Agent Run ==
```text
[vagrant@learning manifests]$ tmux
open terminal failed: missing or unsuitable terminal: xterm-termite
[vagrant@learning manifests]$ export TERM=xterm
[vagrant@learning manifests]$ tmux
[detached]
[vagrant@learning manifests]$ ssh learning@agent.puppet.vm
Warning: Permanently added 'agent.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@agent.puppet.vm's password: 
pPermission denied, please try again.
learning@agent.puppet.vm's password: 
Permission denied, please try again.
learning@agent.puppet.vm's password: 
Last failed login: Wed Aug 26 14:39:31 UTC 2020 from learning.puppetlabs.vm on ssh:notty
There were 2 failed login attempts since the last successful login.
Last login: Wed Aug 26 14:39:04 2020 from learning.puppetlabs.vm
[~]
learning@agent: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Error: Could not retrieve catalog from remote server: Error 500 on SERVER: Server Error: Could not parse for environment production: Syntax error at '' (file: /etc/puppetlabs/code/environments/production/manifests/site.pp, line: 37, column: 1) on node agent.puppet.vm
Warning: Not using cache on failed catalog
Error: Could not retrieve catalog; skipping run
[~]
learning@agent: $ clear

[~]
learning@agent: $ ls
[~]
learning@agent: $ exit
logout
Connection to agent.puppet.vm closed.
[vagrant@learning manifests]$ sudo vim site.pp 
[vagrant@learning manifests]$ ssh learning@agent.puppet.vm
Warning: Permanently added 'agent.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@agent.puppet.vm's password: 
Last login: Wed Aug 26 14:39:34 2020 from learning.puppetlabs.vm
[~]
learning@agent: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for agent.puppet.vm
Info: Applying configuration version '1598452885'
Notice: hello pupppet!
Notice: /Stage[main]/Main/Node[agent.puppet.vm]/Notify[hello pupppet!]/message: defined 'message' as 'hello pupppet!'
Notice: Applied catalog in 0.70 seconds
[~]
learning@agent: $ exit

```

### == Manifests and stuffs ==
```text
[vagrant@learning manifests]$ tmux
open terminal failed: missing or unsuitable terminal: xterm-termite
[vagrant@learning manifests]$ export TERM=xterm
[vagrant@learning manifests]$ tmux
[detached]
[vagrant@learning manifests]$ ssh learning@agent.puppet.vm
Warning: Permanently added 'agent.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@agent.puppet.vm's password: 
pPermission denied, please try again.
learning@agent.puppet.vm's password: 
Permission denied, please try again.
learning@agent.puppet.vm's password: 
Last failed login: Wed Aug 26 14:39:31 UTC 2020 from learning.puppetlabs.vm on ssh:notty
There were 2 failed login attempts since the last successful login.
Last login: Wed Aug 26 14:39:04 2020 from learning.puppetlabs.vm
[~]
learning@agent: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Error: Could not retrieve catalog from remote server: Error 500 on SERVER: Server Error: Could not parse for environment production: Syntax error at '' (file: /etc/puppetlabs/code/environments/production/manifests/site.pp, line: 37, column: 1) on node agent.puppet.vm
Warning: Not using cache on failed catalog
Error: Could not retrieve catalog; skipping run
[~]
learning@agent: $ clear

[~]
learning@agent: $ ls
[~]
learning@agent: $ exit
logout
Connection to agent.puppet.vm closed.
[vagrant@learning manifests]$ sudo vim site.pp 
[vagrant@learning manifests]$ ssh learning@agent.puppet.vm
Warning: Permanently added 'agent.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@agent.puppet.vm's password: 
Last login: Wed Aug 26 14:39:34 2020 from learning.puppetlabs.vm
[~]
learning@agent: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for agent.puppet.vm
Info: Applying configuration version '1598452885'
Notice: hello pupppet!
Notice: /Stage[main]/Main/Node[agent.puppet.vm]/Notify[hello pupppet!]/message: defined 'message' as 'hello pupppet!'
Notice: Applied catalog in 0.70 seconds
[~]
learning@agent: $ exit



[vagrant@learning]/opt/puppetlabs/puppet/modules% ls
facter_task   pe_concat          pe_install     pe_puppet_authorization  pe_staging         service
package       pe_hocon           pe_java_ks     pe_r10k                  pe_support_script
pe_accounts   pe_infrastructure  pe_nginx       pe_razor                 puppet_conf
pe_bootstrap  pe_inifile         pe_postgresql  pe_repo                  puppet_enterprise
[vagrant@learning]/opt/puppetlabs/puppet/modules% clear
[vagrant@learning]/opt/puppetlabs/puppet/modules% exit
[vagrant@learning modules]$ ls
facter_task   pe_concat		 pe_install	pe_puppet_authorization  pe_staging	    service
package       pe_hocon		 pe_java_ks	pe_r10k			 pe_support_script
pe_accounts   pe_infrastructure  pe_nginx	pe_razor		 puppet_conf
pe_bootstrap  pe_inifile	 pe_postgresql	pe_repo			 puppet_enterprise
[vagrant@learning modules]$ puppet config print modulepath
/opt/puppetlabs/puppet/modules
[vagrant@learning modules]$ cd /opt/puppetlabs/puppet/
[vagrant@learning puppet]$ ls
bin  cache  etc  include  lib  modules	share  ssl  vendor_modules  VERSION
[vagrant@learning puppet]$ cd modules
[vagrant@learning modules]$ ls
facter_task   pe_concat		 pe_install	pe_puppet_authorization  pe_staging	    service
package       pe_hocon		 pe_java_ks	pe_r10k			 pe_support_script
pe_accounts   pe_infrastructure  pe_nginx	pe_razor		 puppet_conf
pe_bootstrap  pe_inifile	 pe_postgresql	pe_repo			 puppet_enterprise
[vagrant@learning modules]$ mkdir -p cowsay/manifests
mkdir: cannot create directory ‘cowsay’: Permission denied
[vagrant@learning modules]$ sudo mkdir -p cowsay/manifests
[vagrant@learning modules]$ cd cowsay/
[vagrant@learning cowsay]$ ls
manifests
[vagrant@learning cowsay]$ cd manifests/
[vagrant@learning manifests]$ ls
[vagrant@learning manifests]$ sudo vim init.pp
[vagrant@learning manifests]$ puppet parser validate init.pp 
[vagrant@learning manifests]$ cd ..
[vagrant@learning cowsay]$ ls
manifests
[vagrant@learning cowsay]$ cd ..
[vagrant@learning modules]$ ls
cowsay	      pe_concat		 pe_java_ks		  pe_razor	     puppet_enterprise
facter_task   pe_hocon		 pe_nginx		  pe_repo	     service
package       pe_infrastructure  pe_postgresql		  pe_staging
pe_accounts   pe_inifile	 pe_puppet_authorization  pe_support_script
pe_bootstrap  pe_install	 pe_r10k		  puppet_conf
[vagrant@learning modules]$ ls
cowsay	      pe_concat		 pe_java_ks		  pe_razor	     puppet_enterprise
facter_task   pe_hocon		 pe_nginx		  pe_repo	     service
package       pe_infrastructure  pe_postgresql		  pe_staging
pe_accounts   pe_inifile	 pe_puppet_authorization  pe_support_script
pe_bootstrap  pe_install	 pe_r10k		  puppet_conf
[vagrant@learning modules]$ cd /etc/puppetlabs/c
client-tools/     code/             code-staging/     console-services/ 
[vagrant@learning modules]$ cd /etc/puppetlabs/c
client-tools/     code/             code-staging/     console-services/ 
[vagrant@learning modules]$ cd /etc/puppetlabs/code
[vagrant@learning code]$ ls
environments  hieradata  modules
[vagrant@learning code]$ cd modules/
[vagrant@learning modules]$ cd ..
[vagrant@learning code]$ cd environments/
[vagrant@learning environments]$ ls
production
[vagrant@learning environments]$ cd production/
[vagrant@learning production]$ ls
data  environment.conf	hiera.yaml  manifests  modules
[vagrant@learning production]$ cd manifests/
[vagrant@learning manifests]$ ls
site.pp
[vagrant@learning manifests]$ sudo vim site.pp 
[vagrant@learning manifests]$ ssh learning@cowsay.puppet.vm
Warning: Permanently added 'cowsay.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@cowsay.puppet.vm's password: 
Last login: Wed Aug 26 15:01:57 2020 from learning.puppetlabs.vm
[~]
learning@cowsay: $ sudo puppet agent -t --noop
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Applying configuration version '1598456464'
Notice: /Stage[main]/Cowsay/Package[cowsay]/ensure: current_value 'absent', should be 'present' (noop)
Notice: Class[Cowsay]: Would have triggered 'refresh' from 1 event
Notice: Stage[main]: Would have triggered 'refresh' from 1 event
Notice: Applied catalog in 1.98 seconds
[~]
learning@cowsay: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for cowsay.puppet.vm
Info: Applying configuration version '1598456546'
Notice: /Stage[main]/Cowsay/Package[cowsay]/ensure: created
Notice: Applied catalog in 3.20 seconds
[~]
learning@cowsay: $ cowsay hi
 ____ 
| hi |
 ---- 
      \   ^__^
       \  (oo)\_______
          (__)\       )\/\
              ||----w |
              ||     ||
[~]
learning@cowsay: $ 

Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Applying configuration version '1598456464'
Notice: /Stage[main]/Cowsay/Package[cowsay]/ensure: current_value 'absent', should be 'present' (noop)
Notice: Class[Cowsay]: Would have triggered 'refresh' from 1 event
Notice: Stage[main]: Would have triggered 'refresh' from 1 event
Notice: Applied catalog in 1.98 seconds
[~]
learning@cowsay: $ sudo puppet agent -t
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for cowsay.puppet.vm
Info: Applying configuration version '1598456546'
Notice: /Stage[main]/Cowsay/Package[cowsay]/ensure: created
Notice: Applied catalog in 3.20 seconds
[~]
learning@cowsay: $ cowsay hi
 ____ 
| hi |
 ---- 
      \   ^__^
       \  (oo)\_______
          (__)\       )\/\
              ||----w |
              ||     ||
[~]
learning@cowsay: $ exit
logout
Connection to cowsay.puppet.vm closed.
[vagrant@learning manifests]$ puppet config print modulepath
/opt/puppetlabs/puppet/modules
[vagrant@learning manifests]$ cd /opt/puppetlabs/puppet/
[vagrant@learning puppet]$ ls
bin  cache  etc  include  lib  modules	share  ssl  vendor_modules  VERSION
[vagrant@learning puppet]$ cd modules/
[vagrant@learning modules]$ ls
cowsay	      pe_concat		 pe_java_ks		  pe_razor	     puppet_enterprise
facter_task   pe_hocon		 pe_nginx		  pe_repo	     service
package       pe_infrastructure  pe_postgresql		  pe_staging
pe_accounts   pe_inifile	 pe_puppet_authorization  pe_support_script
pe_bootstrap  pe_install	 pe_r10k		  puppet_conf
[vagrant@learning modules]$ cler
-bash: cler: command not found
[vagrant@learning modules]$ clear

[vagrant@learning modules]$ cd cowsay/
[vagrant@learning cowsay]$ ls
manifests
[vagrant@learning cowsay]$ vim fortune.pp
[vagrant@learning cowsay]$ sudo vim fortune.pp
[vagrant@learning cowsay]$ puppet parser validate fortune.pp 
Error: Could not parse for environment production: Unacceptable location. The name 'cowsay::fortune' is unacceptable in file '/opt/puppetlabs/puppet/modules/cowsay/fortune.pp' (file: /opt/puppetlabs/puppet/modules/cowsay/fortune.pp, line: 1, column: 1)
[vagrant@learning cowsay]$ ls
fortune.pp  manifests
[vagrant@learning cowsay]$ cd manifests/
[vagrant@learning manifests]$ ls
init.pp
[vagrant@learning manifests]$ cd ..
[vagrant@learning cowsay]$ ls
fortune.pp  manifests
[vagrant@learning cowsay]$ sudo rm fortune.pp 
[vagrant@learning cowsay]$ cd manifests/
[vagrant@learning manifests]$ ls
init.pp
[vagrant@learning manifests]$ sudo vim fortune.pp
[vagrant@learning manifests]$ puppet parser validate fortune.pp 
[vagrant@learning manifests]$ ls
fortune.pp  init.pp
[vagrant@learning manifests]$ sudo vim init.pp 
[vagrant@learning manifests]$ puppet parser validate init.pp 
[vagrant@learning manifests]$ ssh learning@cowsay.puppet.vm
Warning: Permanently added 'cowsay.puppet.vm,172.18.0.2' (ECDSA) to the list of known hosts.
learning@cowsay.puppet.vm's password: 
Last login: Wed Aug 26 15:39:57 2020 from learning.puppetlabs.vm
[~]
learning@cowsay: $ sudo puppet agent -t --noop
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Applying configuration version '1598457830'
Notice: /Stage[main]/Cowsay::Fortune/Package[fortune-mod]/ensure: current_value 'purged', should be 'present' (noop)
Notice: Class[Cowsay::Fortune]: Would have triggered 'refresh' from 1 event
Notice: Stage[main]: Would have triggered 'refresh' from 1 event
Notice: Applied catalog in 3.49 seconds
[~]
learning@cowsay: $ sudo puppet agent -t 
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for cowsay.puppet.vm
Info: Applying configuration version '1598457966'
Notice: /Stage[main]/Cowsay::Fortune/Package[fortune-mod]/ensure: created
Notice: Applied catalog in 8.48 seconds
[~]
learning@cowsay: $ fortune | cowsay
 _______________________________________________ 
| Several years ago, an international chess     |
| tournament was being held in a swank          |
| hotel in New York. Most of the major          |
| stars of the chess world were there,          |
| and after a grueling day of chess, the        |
| players and their entourages retired          |
| to the lobby of the hotel for a little        |
| refreshment. In the lobby, some players       |
| got into a heated argument about who          |
| was the brightest, the fastest, and the       |
| best chess player in the world. The argument  |
| got quite loud, as various players claimed    |
| that honor. At that point, a security         |
| guard in the lobby turned to another          |
| guard and commented, "If there's anything     |
| I just can't stand, it's chess nuts boasting  |
| in an open foyer."                            |
 ----------------------------------------------- 
      \   ^__^
       \  (oo)\_______
          (__)\       )\/\
              ||----w |
              ||     ||
[~]
learning@cowsay: $ exit
logout
Connection to cowsay.puppet.vm closed.
[vagrant@learning manifests]$ 

```
### == Package File Service ==

```text


```


