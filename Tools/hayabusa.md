Being the first time I have heard of it, I was pretty sure it wasn't the motorcycle, I had to search hayabusa event log to find the repo:
[Hayabusa-Repo](https://github.com/Yamato-Security/hayabusa)
# What I used to install on a fedora OS:
- sudo dnf install git rust cargo
- git clone https://github.com/Yamato-Security/hayabusa.git
- cd hayabusa
- cargo build --release
- sudo cp target/release/hayabusa /usr/local/bin/  (so I can use it from anywhere)
