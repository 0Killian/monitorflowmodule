# MonitorFlow Module

### Description

This module is used by the application [monitorflow](https://github.com/Kidoly/monitorflow) to monitor multiple servers/computer. It need to be installed on each server.

### Requirements

- Rust (latest stable version recommended)
- xcb

##### For Debian/Ubuntu-based distributions:

```
sudo apt-get update
sudo apt-get install libxcb1-dev
```

##### For Fedora, CentOS, RHEL:

```
sudo dnf install libxcb-devel  # Use dnf on Fedora
# or
sudo yum install libxcb-devel  # Use yum on CentOS/RHEL
```

##### For Arch:

```
sudo pacman -S libxcb
```

### Installation

#### Step 1: Clone the Repository

```
git clone https://github.com/Kidoly/monitorflowmodule.git
cd monitorflowmodule
```

#### Step 2: Build the Program

```
cargo build --release
```

This command compiles your program in release mode. The compiled binary will be located at 'target/release/monitorflowmodule'.

#### Step 3: Configuration

You should modify the .env to your own PASSWORD and API_URL.

```
PASSWORD=YourPassword
API_URL=http://localhost:3000/api/api_receive
INTERVAL=600 # Time in seconds between each execution
```

#### Step 4: Running the Program

To run the program, navigate to the directory and execute it:

```
cargo run
```

### Setting Up Automatic Launch

#### Linux (Using systemd)

1. Create a systemd service file for your program at '/etc/systemd/system/monitorflowmodule.service'. Replace monitorflowmodule and /path/to/ with the actual path to your program:

```
[Unit]
Description=MonitorFlow Module Service

[Service]
ExecStart=/path/to/monitorflowmodule
WorkingDirectory=/path/to/your/program/directory
EnvironmentFile=/path/to/your/program/directory/.env
Restart=always

[Install]
WantedBy=multi-user.target
```

For example if you put the program in your home it should look like this:

```
[Unit]
Description=MonitorFlow Module Service

[Service]
ExecStart=/home/kidoly/monitorflowmodule/target/release/monitorflowmodule
WorkingDirectory=/home/kidoly/monitorflowmodule
EnvironmentFile=/home/kidoly/monitorflowmodule/.env
Restart=always

[Install]
WantedBy=multi-user.target
```

2. Enable and start the service:

```
sudo systemctl enable monitorflowmodule.service
sudo systemctl start monitorflowmodule.service
```

This will set monitorflowmodule to start automatically at boot.
