SHAFE=shafe
INSTALL_DIR=/usr/local/bin
INSTALL_SHAFE=$(INSTALL_DIR)/$(SHAFE)

.PHONY: test
test: test/podman
.PHONY: test/podman
test/podman:
	@podman run --rm -v "$$PWD:/mnt:Z" koalaman/shellcheck:stable $(SHAFE) \
	&& echo "All good!"
.PHONY: test/docker
test/docker:
	@docker run --rm -v "$$PWD:/mnt" koalaman/shellcheck:stable $(SHAFE) \
	&& echo "All good!"

install:
	@install -m 755 "$(SHAFE)" "$(INSTALL_DIR)"

uninstall:
	@if [ -f "$(INSTALL_SHAFE)" ]; then rm -i "$(INSTALL_SHAFE)"; else echo "file not found: $(INSTALL_SHAFE)"; fi
