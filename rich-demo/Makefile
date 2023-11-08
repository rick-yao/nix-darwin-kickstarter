#
#  NOTE: Makefile's target name should not be the same as one of the file or directory in the current directory, 
#    otherwise the target will not be executed!
#


############################################################################
#
#  Darwin related commands
#
############################################################################

#  NOTE: Feel free to remove this target if you don't need a proxy to speed up the build process
darwin-set-proxy:
	sudo python3 scripts/darwin_set_proxy.py

darwin: darwin-set-proxy
	# NOTE: update hostname here!
	nix build .#darwinConfigurations.ricks-Virtual-Machine.system \
		--extra-experimental-features 'nix-command flakes'

	./result/sw/bin/darwin-rebuild switch --flake .#ricks-Virtual-Machine

darwin-debug: darwin-set-proxy
	# NOTE: update hostname here!
	nix build .#darwinConfigurations.ricks-Virtual-Machine.system --show-trace --verbose \
		--extra-experimental-features 'nix-command flakes'

	./result/sw/bin/darwin-rebuild switch --flake .#ricks-Virtual-Machine --show-trace --verbose

############################################################################
#
#  nix related commands
#
############################################################################


update:
	nix flake update

history:
	nix profile history --profile /nix/var/nix/profiles/system

gc:
	# remove all generations older than 7 days
	sudo nix profile wipe-history --profile /nix/var/nix/profiles/system  --older-than 7d

	# garbage collect all unused nix store entries
	sudo nix store gc --debug


fmt:
	# format the nix files in this repo
	nix fmt

.PHONY: clean  
clean:  
	rm -rf result
