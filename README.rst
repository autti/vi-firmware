=================================
OpenXC Vehicle Interface Firmware
=================================

.. image:: /docs/_static/logo.png

:Version: 7.2.1-dev
:Web: http://openxcplatform.com
:Documentation: http://vi-firmware.openxcplatform.com
:Source: http://github.com/openxc/vi-firmware
:Keywords: vehicle, openxc, embedded

.. image:: https://travis-ci.org/openxc/vi-firmware.svg?branch=master
    :target: https://travis-ci.org/openxc/vi-firmware

.. image:: https://coveralls.io/repos/openxc/vi-firmware/badge.png?branch=master
    :target: https://coveralls.io/r/openxc/vi-firmware?branch=master

.. image:: https://readthedocs.org/projects/openxc-vehicle-interface-firmware/badge
    :target: http://vi-firmware.openxcplatform.com
    :alt: Documentation Status

The OpenXC vehicle interface (VI) firmware runs on a microcontroller connected
to one or more CAN buses. It receives either all CAN messages or a filtered
subset, performs any unit conversion or factoring required and outputs a generic
version to a USB interface.

For more documentation, see the `vehicle interface`_ section on the `OpenXC
website`_ or the `vehicle interface documentation`_.

.. _`OpenXC website`: http://openxcplatform.com
.. _`vehicle interface`: http://openxcplatform.com/vehicle-interface/firmware.html
.. _`vehicle interface documentation`: http://vi-firmware.openxcplatform.com

Installation
=============

For the full build instructions, see the `documentation
<http://vi-firmware.openxcplatform.com>`_.


Releasing
=========

- Make sure you release the Python library first if there are any updates

- Update ``script/bootstrap/ci-requirements.txt`` to use released version at PyPI
  (i.e. the requirement should be ``openxc==<latestversion>``)

- Make sure you release the openxc-message-format library first if there are any updates

- Update the src/libs/openxc-message-format with ``git submodule update --remote``

- Checkout next branch and make edits.

- Bump the version using `semantic versioning`_ in
  - ``CHANGELOG.mkd``
  - ``README.rst``
  - ``src/config.cpp``
  - ``docs/index.rst``
  - ``docs/conf.py``

- Checkout master, merge in next

- Run 'fab release', say yes to the tag and use the format ``v0.9.1``

  - This will run the test suite, tag, and push to GitHub

- Checkout the next branch, and edit the same files to change the version to the
  next development release (one patch release up with the ``-dev`` suffix, e.g.
  ``v0.9.2-dev``

- Go to https://github.com/openxc/vi-firmware/releases and promote the tag you
  just created to a new release - copy and paste the changelog into the
  description.

  - Attach the ``openxc-vi-firmware-*.zip`` from the ``releases`` directory to
    the release on GitHub

.. _`semantic versioning`: http://semver.org

License
=======

Copyright (c) 2012-2014 Ford Motor Company

Licensed under the BSD license.

This repository includes links to other source code repositories (as git
submodules) that may be distributed under different licenses. See those
individual repositories for more details.

Brillo
======

openxc-generate-firmware-code -m src/fusion.json >> src/signals.cpp

MSD_ENABLE=0 TEST_MODE_ONLY=0 TRANSMITTER=0 DEFAULT_ALLOW_RAW_WRITE_UART=1 DEFAULT_POWER_MANAGEMENT=SILENT_CAN DEFAULT_METRICS_STATUS=0 DEFAULT_CAN_ACK_STATUS=0 DEFAULT_ALLOW_RAW_WRITE_NETWORK=1 DEBUG=0 DEFAULT_LOGGING_OUTPUT=OFF BOOTLOADER=1 DEFAULT_USB_PRODUCT_ID=1 NETWORK=0 DEFAULT_OUTPUT_FORMAT=JSON DEFAULT_FILE_GENERATE_SECS=180 ENVIRONMENT_MODE=default_mode DEFAULT_RECURRING_OBD2_REQUESTS_STATUS=0 PLATFORM=FORDBOARD DEFAULT_ALLOW_RAW_WRITE_USB=1 DEFAULT_EMULATED_DATA_STATUS=0 DEFAULT_OBD2_BUS=1 make -j4
