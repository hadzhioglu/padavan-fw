SRC_NAME=tor-0.3.3.X

CFLAGS +=$(COPT) -ffunction-sections -fdata-sections
LDFLAGS += -Wl,--gc-sections

all: config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./configure \
		--prefix=/usr \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) \
		--prefix=/usr \
		--sysconfdir=/etc/storage \
		--disable-android \
		--disable-tool-name-check \
		--disable-gcc-hardening \
		--disable-asciidoc \
		--disable-systemd \
		--disable-lzma; \
	)

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) distclean ; \
	fi ; \
	rm -f config_done GeoLite2-Country.mmdb*

romfs:
	$(ROMFSINST) $(SRC_NAME)/src/or/tor /usr/sbin/tor
	$(ROMFSINST) -p +x /usr/bin/tor.sh
	mkdir -p $(INSTALLDIR)/usr/share/tor
ifeq ($(CONFIG_FIRMWARE_INCLUDE_TOR_GEOIP),y)
	$(ROMFSINST) /usr/share/tor/geoip
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_TOR_GEOIPV6),y)
ifeq ($(CONFIG_FIRMWARE_ENABLE_IPV6),y)
	$(ROMFSINST) /usr/share/tor/geoip6
endif
endif
