# Makefile to build packages from directories containing a 'debian' folder

# Define the build directory
BUILD_DIR := build
OUTPUT := out

# Find all directories containing a 'debian' folder
SHELL_DIRS := $(shell find shell -type d -name 'debian' -exec dirname {} \;)
LIB_DIRS := $(shell find lib -type d -name 'debian' -exec dirname {} \;)
EXTRA_PKG := $(shell find system -type d -name 'debian' -exec dirname {} \;)
PKG_DEB := $(shell find out/ -name '*.deb')

# Define a target for each directory
.PHONY: all config pkg-base $(SHELL_DIRS) $(LIB_DIRS) $(EXTRA_PKG) $(IMAGE_BUILD)

all: 
	@mkdir -p $(OUTPUT)
	@echo "Nothing doing."


config:
	@$(foreach dir,$(SHELL_DIRS) $(LIB_DIRS) $(EXTRA_PKG) init,mkdir -p $(OUTPUT)/$(dir);)
	@$(foreach dir,$(SHELL_DIRS),cp -r $(dir)/* $(OUTPUT)/$(dir)/;)
	@$(foreach dir,$(LIB_DIRS),cp -r $(dir)/* $(OUTPUT)/$(dir)/;)
	@$(foreach dir,$(EXTRA_PKG),cp -r $(dir)/* $(OUTPUT)/$(dir)/;)
	@$(foreach dir,init,cp -r $(dir)/* $(OUTPUT)/$(dir)/;)

image:
	@$(foreach dir,images build_img,mkdir -p $(OUTPUT)/$(dir);)
	@$(foreach dir,$(BUILD_DIR)/*,cp -rv $(dir) $(OUTPUT)/build_img/;)
	@echo "Building System Image(ISO)"
	@cd $(OUTPUT)/build_img/ && mv config .getopt.sh
	@mkdir -p $(OUTPUT)/build_img/lingmo-config/common/packages.chroot
	@$(foreach dir,$(PKG_DEB),cp -v $(dir) $(OUTPUT)/build_img/lingmo-config/common/packages.chroot/;)
	@cd $(OUTPUT)/build_img && bash build.sh
	@cd -

pkg-shell: $(SHELL_DIRS)
pkg-libs: $(LIB_DIRS)
pkg-extra: $(EXTRA_PKG)
pkg-base:
	@echo "Processing directory: init"
	@cd $(OUTPUT)/init/ && sudo apt build-dep . -y && dpkg-buildpackage -b -uc -us -j8
	@cd -

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

