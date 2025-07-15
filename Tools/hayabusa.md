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
## Some commands that I found most interesting and useful:
- ### $hayabusa update-rules
Updates detection rules(necessary)

- ### $hayabusa csv-timeline --file something.evtx -o timeline.csv
This creates a DFIR timeline in CSV format 

- ### $hayabusa json-timeline --file something.evtx -o timeline.json
Same, but in JSON format

- ### $hayabusa eid-metrics --file something.evtx
Summarize events by ID

- ### $hayabusa log-metrics --file something.evtx
Check log file Metadata

- ### $hayabusa search --file something.evtx --keyword powershell
Search by keyword

- ### $hayabusa logon-summary --file something.evtx
Get Logon activity summary

