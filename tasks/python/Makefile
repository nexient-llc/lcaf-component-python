.PHONY: python/venv
python/venv: .venv/touchfile

.venv/touchfile:
	test -d .venv || python3 -m venv .venv
	source .venv/bin/activate; pip install -q -r requirements.txt;
	touch .venv/touchfile

.PHONY: python/tests/requirements
python/tests/requirements: python/venv
	@if [ -f requirements.txt ]; then \
		echo "Installing from requirements.txt"; \
		pip install -q -r requirements.txt; \
	fi
	@if [ -f requirements_test.txt ]; then \
		echo "Installing from requirements_test.txt"; \
		pip install -q -r requirements_test.txt; \
	fi

.PHONY: python/tests
python/tests: python/tests/requirements python/tests/unit

.PHONY: python/tests/full
tests/full: python/tests/unit python/tests/integration

.PHONY: python/tests/unit
python/tests/unit: python/tests/requirements
	@if [ -d tests/unit ]; then \
		echo "Running unit tests"; \
		pytest tests/unit -ra -vv; \
	fi

.PHONY: python/tests/integration
python/tests/integration: python/tests/requirements
	@-$(MAKE) python/tests/integration/setup;
	@if [ -d tests/integration ]; then \
		pytest tests/integration --tb=no -v; \
	fi
	@-$(MAKE) python/tests/integration/teardown;

.PHONY: python/clean
python/clean:
	@rm -fr .pytest_cache
	@rm -f .venv/touchfile
