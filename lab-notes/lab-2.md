# Lab 2 Notes

## Objective
Practice using Git and GitHub to manage a project, track changes, and keep work organized. The goal was to learn how to create and use a repository, connect securely, create branches, stage and commit work, and collaborate using pull requests.

## Commands used
```bash
ls -l
pwd
cd
mkdir
touch
cat
grep
chmod
ssh-keygen -t ed25519
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
ssh -T git@github.com
git clone git@github.com:Blin-35/Lab-Practice.git
git switch -c lab-1-notes
git status
git add .
git commit -m "Add lab notes"
git push origin lab-1-notes
git pull
```

### What these commands were used for
- `ls -l`: showed the files and folders in the current directory.
- `pwd`: confirmed the current working location.
- `cd`: moved between folders.
- `mkdir`: created a new directory.
- `touch`: created new files.
- `cat`: displayed file content.
- `grep`: searched files for text.
- `chmod`: changed file permissions when needed.
- `ssh-keygen -t ed25519`: created an SSH key for secure GitHub access.
- `ssh-add --apple-use-keychain ~/.ssh/id_ed25519`: added the private key to the macOS keychain.
- `ssh -T git@github.com`: tested whether GitHub recognized the SSH connection.
- `git clone ...`: copied the repository to my local machine.
- `git switch -c ...`: created a new working branch.
- `git status`: checked which files changed and what was staged.
- `git add .`: staged the changes for commit.
- `git commit -m ...`: saved the changes with a message.
- `git push origin ...`: uploaded the branch to GitHub.
- `git pull`: updated the local branch with the newest remote changes.

## Errors encountered
### 1. SSH authentication problems
When I tried to connect to GitHub with SSH, the terminal reported that authentication failed or the key was not accepted.

### 2. Untracked or modified files during work
Some files were not yet staged, so Git showed them as untracked or modified before I was ready to commit.

## Solutions
### SSH authentication fix
I generated a new SSH key using `ssh-keygen -t ed25519`, then added it to the keychain with `ssh-add --apple-use-keychain ~/.ssh/id_ed25519`. After confirming the public key was added to GitHub, I tested the connection with `ssh -T git@github.com` and completed the repo setup.

### File tracking fix
I used `git status` to check what was changed, then used `git add .` to stage the updated files. After that, I created a commit with `git commit -m "Add lab notes"` and pushed the branch with `git push origin lab-1-notes`.

## Lessons learned
- Git keeps a record of file history, which makes it easier to track and revise work.
- Branches help keep separate tasks organized without affecting the main project.
- SSH is a safer way to authenticate with GitHub than using a password every time.
- `git status` is a useful command for checking the state of the repository before committing.
- Pull requests make it easier to review and approve changes before merging them.
- It is important to check file permissions, key setup, and repository status before troubleshooting larger issues.

## Security note
This lab documentation does not include passwords, private keys, or any restricted school information.


## Networking practice — September 21, 2026

### Objective and record of work
Practice diagnosing Windows network problems, configuring DHCP, and verifying the effect of each change. These notes summarize my reported actions and results from today's lab conversations; they are not a verbatim terminal log. Repeated exercises are grouped by topic. Commands run inside the Windows lab are separate from the macOS/Git commands above.

### Windows commands I used
| Command | Why I used it | Observed result or lesson |
| --- | --- | --- |
| `ipconfig /all` | Inspect the active adapter's IPv4 address, subnet mask, gateway, DHCP status/server, and DNS servers. | Revealed incorrect gateways, failed DHCP addressing, and a workstation using manual settings. I also used it after repairs. |
| `ipconfig /renew` | Renew DHCP configuration after a server-side repair. | Clients received the corrected gateway and regained reported internet connectivity. This renews a lease; it does not reboot the computer. |
| `ping <local-device-IP>` | Test another device on the same LAN. | Local tests succeeded in the wrong-gateway case even while external tests failed. |
| `ping <default-gateway-IP>` | Check reachability of the configured router. | The incorrect gateway failed to respond; the corrected gateway responded after renewal in the later troubleshooting exercise. |
| `ping <external-test-IP>` | Test IP connectivity beyond the local network. | Failed before repairs and succeeded in several completed verification exercises. |
| `ping <hostname>` | Test a named device, including the local workstation and a server. | A successful self-ping did not prove that other devices or the internet were reachable. |
| `tracert <destination-IP>` | Inspect the route toward a server or an external test destination. | I saw both timed-out attempts and a successful external trace with four displayed hops. The result depends on the source workstation and its configuration. |

Angle-bracket values are placeholders, not literal commands to paste. Use the intended lab destination. `ipconfig /release` was also discussed; the conversation does not clearly establish that I ran it. It releases DHCP configuration and can interrupt connectivity, so it is not a required first step for every renewal.

Command references: [ipconfig](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig), [ping](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ping), and [tracert](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tracert).

### Troubleshooting cases and results

#### Incorrect default gateway supplied by DHCP
- **Evidence:** Affected clients could reach local devices but failed external connectivity tests. They received the same gateway from DHCP, and that gateway did not match the router shown in the network diagram.
- **Change:** Corrected DHCP scope option **003 Router**, then renewed client configuration.
- **Verification:** In an earlier exercise, I checked the updated gateway and reported restored connectivity on both affected clients and a 100% lab score. In a later variation, I reported successful gateway pings and restored connectivity on both clients; its final score was not recorded.
- **Lesson:** Compare received settings with the intended network design. A shared configuration error can originate at the DHCP server.

#### Inactive DHCP scope
- **Evidence:** Clients were configured for DHCP but showed `169.254.x.x` link-local/APIPA addresses and no usable default gateway.
- **Change:** Activated the relevant DHCP scope.
- **Verification:** In the earlier exercise, both clients regained connectivity and I reported successful server/external pings and route checks. In the final exercise of the day, I confirmed one client had a normal DHCP address, a /24 mask, a gateway, DNS settings, and restored connectivity. I said I would check the other client next, but that final check is not recorded.
- **Lesson:** APIPA on a DHCP client is a clue to investigate lease acquisition. It does not, by itself, prove which server or network component failed.

#### Workstation using incorrect manual settings
- **Evidence:** `ipconfig /all` showed DHCP disabled on a workstation that was intended to use DHCP. Its subnet mask differed from the working configuration; self-ping worked while other tests failed.
- **Change:** Set the adapter's IPv4 and DNS settings to obtain their configuration automatically.
- **Verification:** I reported DHCP enabled, a corrected /24 mask, supplied DNS settings, and successful pings after the change.
- **Lesson:** Diagnose whether the fault is on one client or in a shared service before choosing where to make the repair.

### DHCP and adapter configuration practiced
These were GUI changes in Windows management tools, not additional terminal commands.

| Work performed | What I did and learned | Recorded outcome |
| --- | --- | --- |
| IPv4 scopes | Used **IPv4 → New Scope**, entered the required pool and network options, then activated the scope. Repeated the workflow for another subnet. | Reported successful client checks after one scope exercise and 100% scores for two later scope-creation exercises. |
| Server and scope options | Worked with **006 DNS Servers**, **015 DNS Domain Name**, and scope-specific **003 Router**. Learned to distinguish server-wide settings from settings for one scope. | Reported completion and a 100% score for the options exercise. |
| Exclusions | Practiced locating **Address Pool** and excluding addresses from the dynamic pool. | Reported the exercise done; no explicit score is preserved in the text. |
| Reservations | Created reservations using the required name, IP address, and client identifier/MAC address. | Encountered identifier/conflict warnings and a misspelled reservation name. After correcting the name, reported 100%. |
| DHCP relay | Added a DHCP Relay Agent, selected its interface, configured the lab's boot threshold, and entered the destination DHCP server address. | Renewed the remote client's configuration and reported restored internet connectivity. |
| DHCP failover | Worked through the failover wizard and distinguished the current server from its existing partner. Practiced load-balanced and hot-standby configurations. | The conversation records setup and discussion of completion screens; no failover lab score or simulated outage test was independently confirmed here. |
| Split scope | Added an existing second server to the DHCP console, used the Split-Scope wizard, configured the requested distribution and target-server delay, then activated the second scope. | Reported a 100% score after activation. |
| Alternate Wi-Fi addressing | Enabled automatic IPv4/DNS settings and entered the specified fallback settings under **Alternate Configuration → User configured**. | Reported saving the configuration; a final score or test of both environments was not recorded. |

### Errors, corrections, and lessons learned
- **Wrong device or console:** I sometimes confused the host, a virtual machine, the domain controller, and the DHCP server. Check the selected machine and console title before changing settings.
- **Wrong source for a test:** Record which workstation ran each command. A result from a working server does not establish that an affected workstation is fixed.
- **Reservation spelling and identifiers:** A reservation name typo affected grading. Inspect the actual saved entry and check names, IPs, and identifiers carefully when warnings or duplicates appear.
- **Gateway versus switch:** In these labs, the router interface was the default gateway. A switch's management address was not the route to external networks.
- **Renew versus reboot:** Renewing DHCP requests updated configuration; restarting Windows is a different action.
- **DHCP status versus autoconfiguration:** Read the DHCP status, address, gateway, and server together. The word “autoconfiguration” alone is not enough to identify how a usable address was obtained.
- **Trace limits:** Thirty timed-out attempts do not establish that a destination is thirty hops away. Some routers do not answer trace probes.
- **Verification limits:** A successful IP ping does not by itself prove DNS resolution or application access. Record what each test actually demonstrates.
- **Failover versus split scope:** Failover partners share lease information; a split-scope design divides address allocation between servers. They are distinct approaches. See [Microsoft's DHCP failover overview](https://learn.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-failover).
- **Reading instructions:** Identify the machine, action, setting, and required values before clicking. “Add an existing server to the console” is different from creating a server.
- **Before and after:** Preserve the original symptoms as well as the repaired state, especially when a question asks about the original condition.

### Verification still to record
- The final inactive-scope exercise: the second affected client's post-fix configuration and connectivity.
- Final scores or explicit completion checks for exercises where the conversation only records the configuration changes.
- Exact terminal output and timestamps were not retained, so this document should not be treated as a complete command transcript.

This networking summary omits credentials, DHCP shared secrets, client identifiers, screenshots, private conversation text, and copied assessment questions.
