# Makefile to build packages from directories containing a 'debian' folder

# Define the build directory
BUILD_DIR := build
OUTPUT := out

# Find all directories containing a 'debian' folder
SHELL_DIRS := $(shell find shell -type d -name 'debian' -exec dirname {} \;)
LIB_DIRS := $(shell find lib -type d -name 'debian' -exec dirname {} \;)
EXTRA_PKG := $(shell find system -type d -name 'debian' -exec dirname {} \;)

# Define a target for each directory
.PHONY: all $(SHELL_DIRS) $(LIB_DIRS) $(EXTRA_PKG) $(IMAGE_BUILD)

all: 
	@echo "Nothing doing."

config: 
	@mkdir -p $(OUTPUT)/{$(SHELL_DIRS),$(LIB_DIRS),$(EXTRA_PKG)}
	@cp -rv $(SHELL_DIRS)/* $(OUTPUT)/$(SHELL_DIRS)/
	@cp -rv $(LIB_DIRS)/* $(OUTPUT)/$(LIB_DIRS)/
	@cp -rv $(EXTRA_PKG)/* $(OUTPUT)/$(EXTRA_PKG)/

pkg-shell: $(SHELL_DIRS)
pkg-libs: $(LIB_DIRS)
pkg-extra: $(EXTRA_PKG)

$(SHELL_DIRS):
	@echo "Processing directory: $@"
	@cd $(OUTPUT)/$@ && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

$(LIB_DIRS):
	@echo "Processing directory: $@"
	@cd $(OUTPUT)/$@ && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

$(EXTRA_PKG):
	@echo "Processing directory: $@"
	@cd $(OUTPUT)/$@ && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

# Clean up the build directory
clean:
	rm -rf $(BUILD_DIR)

# Default target
pkg: all

