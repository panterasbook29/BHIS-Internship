--- general
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ED65462EC8D5E4C5
sudo apt update && sudo apt full-upgrade -y
cd ~/Desktop
sudo apt install python3-venv
sudo python3 -m venv ~/Desktop/venv
source ~/Desktop/venv/bin/activate
pip3 install Cython
pip3 install setuptools
pip3 install pyyaml
pip3 install boto3

--- dionaea (on Desktop)
sudo git clone https://github.com/DinoTools/dionaea.git + cd dionaea
mkdir build && cd build
sudo nano ../modules/CMakeLists.txt - comment out anything emu related like this
<pre>#if(WITH_MODULE_EMU)
#  if(LIBEMU_FOUND)
#    add_subdirectory(emu)
#  else()
#    message(FATAL_ERROR "You have selected the emu module, but libemu could not be found")
#  endif()
#endif()
</pre>
nano ~/Desktop/dionaea/build/modules/python/setup.py - make sure you have: version = "0.11.0"
source ~/Desktop/venv/bin/activate
mkdir -p venv/lib/python3.12/site-packages/distutils && cd venv/lib/python3.12/site-packages/distutils && for f in __init__ archive_util cmd config core debug dep_util dir_util dist errors extension fancy_getopt file_util log spawn util; do curl -sLO https://raw.githubusercontent.com/python/cpython/3.10/Lib/distutils/$f.py; done
cmake ..
make -j$(nproc)
sudo make install
sudo nano /usr/local/etc/dionaea/dionaea.cfg - Delete anything emu related from modules and processors, should have 4 references from the start


--- hayabusa (on desktop)
sudo apt install -y git curl build-essential pkg-config libssl-dev perl
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
git clone https://github.com/Yamato-Security/hayabusa.git
cd hayabusa
cargo build --release

--- elastic
sudo apt update && sudo apt install openjdk-21-jdk -y
sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
sudo apt update
sudo apt install elasticsearch -y
sudo systemctl enable --now elasticsearch
sudo apt install kibana -y
sudo systemctl enable --now kibana
sudo apt install filebeat -y
sudo systemctl enable --now filebeat
