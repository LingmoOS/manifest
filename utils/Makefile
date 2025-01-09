# Makefile to build packages from directories containing a 'debian' folder

# Define the build directory
BUILD_DIR := build

# Find all directories containing a 'debian' folder
DEBIAN_DIRS := $(shell find . -type d -name 'debian' -exec dirname {} \;)

# Define a target for each directory
.PHONY: all $(DEBIAN_DIRS)

all: $(DEBIAN_DIRS)

$(DEBIAN_DIRS):
	@echo "Processing directory: $@"
	@cp -r $@ $(BUILD_DIR)/
	@cd $(BUILD_DIR)/$@ && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

# Clean up the build directory
clean:
	rm -rf $(BUILD_DIR)

# Default target
pkg: all

