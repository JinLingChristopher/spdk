#
#  BSD LICENSE
#
#  Copyright (c) Intel Corporation.
#  All rights reserved.
#
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions
#  are met:
#
#    * Redistributions of source code must retain the above copyright
#      notice, this list of conditions and the following disclaimer.
#    * Redistributions in binary form must reproduce the above copyright
#      notice, this list of conditions and the following disclaimer in
#      the documentation and/or other materials provided with the
#      distribution.
#    * Neither the name of Intel Corporation nor the names of its
#      contributors may be used to endorse or promote products derived
#      from this software without specific prior written permission.
#
#  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
#  "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
#  LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
#  A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
#  OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
#  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
#  LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
#  DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
#  THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
#  (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
#  OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#

SPDK_ROOT_DIR := $(abspath $(CURDIR)/../..)
include $(SPDK_ROOT_DIR)/mk/spdk.common.mk

SO_VER := 6
SO_MINOR := 0

CFLAGS += $(ENV_CFLAGS)
C_SRCS = env.c memory.c pci.c init.c threads.c
C_SRCS += pci_ioat.c pci_virtio.c pci_vmd.c pci_idxd.c
LIBNAME = env_dpdk

SPDK_MAP_FILE = $(abspath $(CURDIR)/spdk_env_dpdk.map)

include $(SPDK_ROOT_DIR)/mk/spdk.lib.mk

LIBDPDK_PKGCONFIG = $(call pkgconfig_filename,spdk_dpdklibs)

$(LIBDPDK_PKGCONFIG): $(PKGCONFIG)
	$(Q)$(SPDK_ROOT_DIR)/scripts/pc_libs.sh \
		"-L$(DPDK_ABS_DIR)/lib $(DPDK_LIB_LIST:%=-l%)" "" DPDK spdk_dpdklibs > $@
	$(Q)echo Requires: spdk_dpdklibs >> $(PKGCONFIG)

all : $(LIBDPDK_PKGCONFIG)
