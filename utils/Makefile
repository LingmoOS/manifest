# Makefile to build packages from directories containing a 'debian' folder

# Define the build directory
BUILD_DIR := build

# Find all directories containing a 'debian' folder
SHELL_DIRS := $(shell find shell -type d -name 'debian' -exec dirname {} \;)
LIB_DIRS := $(shell find lib -type d -name 'debian' -exec dirname {} \;)

# Define a target for each directory
.PHONY: all

all: 
	@echo "Nothing doing."

pkg-shell:
	@echo "Processing directory: $(SHELL_DIRS)"
	@cp -r $(SHELL_DIRS) $(BUILD_DIR)/
	@cd $(BUILD_DIR)/$(SHELL_DIRS) && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

# Clean up the build directory
clean:
	rm -rf $(BUILD_DIR)

# Default target
pkg: all

