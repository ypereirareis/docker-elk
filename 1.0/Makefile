.PHONY: build remove start stop state bash

cmd=docker-compose
step=----------------

build: remove
	@echo "$(step) Building ELK $(step)"
	@$(cmd) build

remove: stop
	@echo "$(step) Removing ELK $(step)"
	@$(cmd) rm -f

start:
	@echo "$(step) Starting ELK $(step)"
	@$(cmd) up -d elk

stop:
	@echo "$(step) Stopping ELK $(step)"
	@$(cmd) stop

state:
	@$(cmd) ps

bash:
	@$(cmd) run --rm elk bash

logs:
	@$(cmd) logs