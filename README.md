# twrp_j5nlte
Treble twrp tree for j5nlte

# Build instructions

```
#Install dependencies
sudo apt update&&sudo apt install git-core gnupg flex bison gperf zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip default-jdk build-essential git fastboot adb python python3 rsync

#Install latest repo
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

#Install Android SDK Platform Tools
wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip -d ~
cat >> ~/.profile<< EOF
if [ -d "\$HOME/platform-tools" ] ; then
    PATH="\$HOME/platform-tools:\$PATH"
fi
EOF

#Set build cache to 50G
export USE_CCACHE=1
export CCACHE_DIR=~/.ccache
source ~/.bashrc
ccache -M 20G

#Git config
git config --global user.email "you@example.com"
git config --global user.name "Your Name"

#Create twrp root folder
mkdir -p twrp&&cd twrp

#Download and sync TWRP manifest
repo init -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0
repo sync -j$(nproc --all)

#Clone device tree and create device folder
git clone https://github.com/Galaxy-J5-Unofficial-LineageOS-Sources/twrp_j5nlte device/samsung/j5nlte

#Lunch command and build twrp
. build/envsetup.sh
lunch omni_j5nlte-eng
mka recoveryimage

```
