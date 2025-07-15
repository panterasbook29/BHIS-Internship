Being the first time I have heard of it, I was pretty sure it wasn't the motorcycle, I had to search hayabusa event log to find the repo:
[Hayabusa-Repo](https://github.com/Yamato-Security/hayabusa)
# What I used to install on a fedora OS:
- $sudo dnf install git rust cargo
- $git clone https://github.com/Yamato-Security/hayabusa.git
- $cd hayabusa
- $cargo build --release
- ### I got an error on the build and had to install PerlCore: $sudo dnf install perl-core + $cargo clean + again $cargo build --release
- $sudo cp target/release/hayabusa /usr/local/bin/  (so I can use it from anywhere)

### FYI 'dnf' is the same as 'apt' and 'cargo' is pretty much 'make' from kali

# Using the actual tool
## Some commands that I found most interesting and usefull:
- ### $hayabusa csv-timeline -l something.evtx -o timeline.csv
This creates a DFIR timeline in CSV format 
- ### $hayabusa json-timeline -l something.evtx -o timeline.json
Same, but in JSON format
- ### $hayabusa eid-metrics -l something.evtx
Summarize events by ID
- ### $hayabusa log-metrics -l something.evtx
Check log file Metadata
- ### $hayabusa search -l something.evtx -k powershell
Search by keyword
- ### $hayabusa logon-summary -l something.evtx
Get Logon activity summary
- ### $hayabusa update-rules
Pull the detection logs from github
