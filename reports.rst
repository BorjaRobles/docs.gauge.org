.. _gauge_reports:

Reports
=======

The test results report should be easy to comprehend and should be
useful for all the stakeholders.

HTML Reports
------------

Reports are generated using ``html-report`` plugin. By default html-report is added to the project.

When the specs are executed, the html report is generated in ``reports`` directory in the project by default.

**Notes**

-  A comprehensive test results report template prepared in a html
   format providing the overall summary with drill down of the test
   cases executed and effort spent during the testing for each stage and
   feature.
-  It provides the details for the defects found during the run.
-  It indicates the tests by color code - failed(red), passed(green) and
   skipped(grey).
-  The failure can be analyzed with the stacktrace and
   screenshot(captures unless overwritten not to).
-  The skipped tests can be analyzed with the given reason.
-  :ref:`reports_custom_messages` allows users to add messages at runtime.


Configuration
^^^^^^^^^^^^^

The HTML report plugin can be configured by the properties set in the
``env/default.properties`` file in the project.

The configurable properties are:

**gauge_reports_dir**

-  Specifies the path to the directory where the execution reports will
   be generated.

-  Should be either relative to the project directory or an absolute
   path. By default it is set to ``reports`` directory in the project

**overwrite_reports**

-  Set to ``true`` if the reports **must be overwritten** on each
   execution maintaining only the latest execution report.

-  If set to ``false`` then a **new report** will be generated on each
   execution in the reports directory in a nested time-stamped
   directory.

Default value is ``true``

**GAUGE_HTML_REPORT_THEME_PATH**

-  Specifies the path to the custom reports directory.

-  Should be either relative to the project directory or an absolute
   path. 

By default, ``default`` theme shipped with gauge is used.

Report re-generation
^^^^^^^^^^^^^^^^^^^^

If report generation fails due to some reason, we don't have to re-run the tests again.

The html-report plugin now generates a last_run_result.json file in the root of the reports directory.
There is also a symlink to the html-report executable in the same location.

**To regenerate the report**

- Navigate to the reports directory
- run ./html-report --input=last_run_result.json --output="/some/path"

**Note:** The output directory is created. Take care not to overwrite an existing directory

While regenerating a report, the default theme is used. A custom can be used if ``--theme`` flag is specified with the path to the custom theme.

XML Report
----------

XML Report plugin creates JUnit XML test result document that can be
read by tools such as Go, Jenkins. When the specs are executed, the xml
report is generated in reports directory in the project. The format of
XML report is based on `JUnit XML Schema <https://windyroad.com.au/dl/Open%20Source/JUnit.xsd>`__

**Sample XML Report Document** :

.. code-block:: xml

    <testsuites>
        <testsuite id="1" tests="1" failures="0" package="specs/hello_world.spec" time="0.002" timestamp="2015-09-09T13:52:00" name="Specification Heading" errors="0" hostname="INcomputer.local">
            <properties></properties>
            <testcase classname="Specification Heading" name="First scenario" time="0.001"></testcase>
            <system-out></system-out>
            <system-err></system-err>
        </testsuite>
    </testsuites>

Installation
^^^^^^^^^^^^

To install XML Report plugin :

.. code-block:: console

    gauge --install xml-report

To install a specific version of XML report plugin use the ``--plugin-version`` flag.

.. code-block:: console

    gauge --install xml-report --plugin-version 0.0.2

**Offline Installation** :

If plugin should be installed from a zipfile instead of downloading from
plugin repository, use the ``--file`` or ``-f`` flag.

.. code-block:: console

    gauge --install xml-report --file ZIP_FILE_PATH

Download the plugin zip from the `Github Releases <https://github.com/getgauge/xml-report/releases>`__

Configuration
^^^^^^^^^^^^^

To add XML report plugin to your project, run the following command :

.. code-block:: console

    gauge --add-plugin xml-report

The XML report plugin can be configured by the properties set in the
``env/default.properties`` file in the project.

The configurable properties are:

**gauge_reports_dir**

Specifies the path to the directory where the execution reports will be generated.

-  Should be either relative to the project directory or an absolute
   path. By default it is set to ``reports`` directory in the project

**overwrite_reports**

Set to ``true`` if the reports **must be overwritten** on each execution hence maintaining only the latest
execution report.

-  If set to ``false`` then a **new report** will be generated on each
   execution in the reports directory in a nested time-stamped
   directory.

Default value is ``true``

Spectacle
---------

This is a Gauge plugin that generates static HTML from
Specification/Markdown files. Ability to filter specifications and
scenarios are available.

Installation
^^^^^^^^^^^^

To install:

.. code-block:: console

    gauge --install spectacle

To install a specific version of spectacle plugin use the ``--plugin-version`` flag.

.. code-block:: console

    gauge --install spectacle --plugin-version 0.0.2

**Offline Installation**:

If plugin should be installed from a zip file instead of downloading
from plugin repository, use the ``--file`` or ``-f`` flag.

.. code-block:: console

    gauge --install spectacle --file ZIP_FILE_PATH

Download the plugin zip from the `Github Releases <https://github.com/getgauge/spectacle/releases>`__

Usage
^^^^^

Run the following command to export to HTML in a Gauge project

.. code-block:: console

    gauge --docs spectacle <path to specs dir>

**Sample Spectacle Report**

.. figure:: images/spectacle.png
   :alt: Sample spectacle report

   Sample spectacle report

**Filter Specification/Scenario based on Tags**

Tags allow you to filter the specs and scenarios. Add the tags to the
textbox in the report to view all the specs and scenarios which are
labeled with certain tags. Tag expressions with operators ``|``, ``&``,
``!`` are supported.

In the following image, the specs/scenarios are filtered using a tag expression(\ ``refactoring & !api``).

.. figure:: images/filter.png
   :alt: Filter Specification/Scenario

   Filter Specification/Scenario

Flash
-----

Real-time execution reporting plugin! Watch test runs go green or red.
Install it in your CI/CD setup and connect to Flash using your browser to see what your test suites are doing.

Installation
^^^^^^^^^^^^

To install Flash plugin :

.. code-block:: console

    gauge --install flash

To install a specific version of the plugin use the ``--plugin-version`` flag.

.. code-block:: console

    gauge --install flash --plugin-version 0.0.1

**Offline Installation** :

If plugin should be installed from a zipfile instead of downloading from
plugin repository, use the ``--file`` or ``-f`` flag.

.. code-block:: console

    gauge --install flash --file ZIP_FILE_PATH

Download the plugin zip from the `Github Releases <https://github.com/getgauge/flash/releases>`__

Usage
^^^^^
To add Flash plugin to your project, run the following command :

.. code-block:: console

    gauge --add-plugin flash

Execute specs and open the URL in browser shown in console output.

Configuration
^^^^^^^^^^^^^

The Flash plugin can be configured by the properties set in the
``env/default.properties`` file in the project.

The configurable properties are:

**FLASH_SERVER_PORT**

To use a specific port, set ``FLASH_SERVER_PORT={port}`` as environment variable or in ``env/default/flash.properties`` file.