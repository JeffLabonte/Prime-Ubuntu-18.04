install: mode=$(shell /usr/bin/prime-select query)
install:
	@echo "Current Mode is '$(mode)'"
	@if [ $(mode) =  "nvidia" ]; then \
		make nvidia; \
	else	\
		echo "Make sure you set the display to 'nvidia' mode, by running 'sudo /usr/bin/prime-select nvidia' first";	\
	fi

nvidia:
	echo "Making now"
	#sudo cp 10-monitor.conf /usr/share/X11/xorg.conf.d/
	cd .. && sudo cargo build
	sudo cp nvidia-prime-boot.service /etc/systemd/system/
	sudo cp prime-socket.service /etc/systemd/system/
	sudo cp prime-select /usr/local/bin
	sudo cp turnoff_nvidia_at_boot /usr/local/bin
	sudo rm -f /usr/local/bin/prime_socket
	sudo cp ../target/debug/prime_socket /usr/local/bin
	sudo chmod +x /usr/local/bin/prime-select
	sudo chmod +x /usr/local/bin/prime_socket
	sudo chmod +x /usr/local/bin/turnoff_nvidia_at_boot
	sudo systemctl enable prime-socket.service
	sudo systemctl start prime-socket.service
