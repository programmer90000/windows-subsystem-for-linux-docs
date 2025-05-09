Run:
```
sudo apt update
```

Run:
```
sudo apt install openjdk-17-jdk
```

Confirm it is installed by running:
```
java -version
```
Expected output is something similar to:
```
openjdk version "17.0.15" 2025-04-15
OpenJDK Runtime Environment (build 17.0.15+6-Ubuntu-0ubuntu124.04)
OpenJDK 64-Bit Server VM (build 17.0.15+6-Ubuntu-0ubuntu124.04, mixed mode, sharing)
```
Ensure you are using `openjdk version 17`
Run:
```
javac -version
```
Expected output is something similar tot:
```
javac 17.0.15
```
Ensure you are using `javac version 17`

Run:
```
sudo apt install libglu1-mesa libgl1 libxi6 libxrender1 libxrandr2
```

Download the `.tar.gz` installation file of Android Studio from the [official website](https://developer.android.com/studio/).

Ensure the Android Studio installation file is in an area the WSL machine can access

Run: 
```
tar -xzvf android-studio-2024.3.2.14-linux.tar.gz
```

Ensure the file name you type matches the file you downloaded

If needed, move the android-studio directory into a new directory:
```
mkdir -p ~/programs
mv ~/programming/android-studio ~/programs/
```

Download the `.zip` installation file of Android Command Line Tools from the [official website](https://developer.android.com/studio/).
Ensure the Android Command Line Tools installation file is in an area the WSL machine can access

Run:
```
sudo apt install unzip
unzip commandlinetools-linux-13114758_latest.zip -d ~/apps/Sdk/
```

Ensure the file name you type matches the file you downloaded

Run the following command to move the contents of the `cmdline-tools` directory into the `latest` directory:
```
mkdir -p ~/apps/Sdk/cmdline-tools/latest
mv ~/apps/Sdk/cmdline-tools/* ~/apps/Sdk/cmdline-tools/latest/
```

Run the following commands to add the `bin` directory to the PATH variable:
```
export PATH=$PATH:~/apps/Sdk/cmdline-tools/latest/bin
export PATH=$PATH:~/apps/android-studio/bin
export ANDROID_SDK_ROOT=~/apps/Sdk
export PATH=$ANDROID_SDK_ROOT/emulator:$ANDROID_SDK_ROOT/platform-tools:$PATH
source ~/.bashrc
```

Run Android Studio by running:
```
studio


# Troubleshooting
### Installing OpenJDK 11:
Run before installing:
```
sudo apt clean
sudo apt update
```

If this still doesn't work:
```
sudo rm -f /var/cache/apt/archives/openjdk-11-jdk-headless_*.deb
sudo rm -rf /var/lib/apt/lists/*
sudo apt update
sudo apt install --fix-missing openjdk-11-jdk
```

Clean any extra files using:
```
sudo apt autoremove --purge
sudo apt clean
```