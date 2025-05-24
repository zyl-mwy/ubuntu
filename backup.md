# backup
* sudo apt install timeshift
* sudo timeshift --create --comments "Initial Snapshot" --tags D
* sudo timeshift --list
* sudo timeshift --delete --snapshot "2024-11-11_17-23-52"
* sudo timeshift --restore --snapshot "2024-11-11_17-23-52"
