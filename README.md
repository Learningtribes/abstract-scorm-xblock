# Abstract Scorm XBlock

XBlock to display SCORM content within the Open edX LMS. Editable within Open edx Studio. Will save student state and report scores to the progress tab of the course.
Currently supports SCORM 1.2 and SCORM 2004 standard.

Block displays SCORM which saved as `File -> Export -> Web Site -> Zip File`
Block displays SCORM which saved as `File -> Export -> SCORM 1.2`

## Installation

Install package

    pip install git+https://github.com/Abstract-Tech/abstract-scorm-xblock.git#egg=abstract_scorm_xblock&subdirectory=abstract_scorm_xblock

**WARNING: This package have to be installed using the `subdirectory` option.**

## Usage

- Add `abstract_scorm_xblock` to the list of advanced modules in the advanced settings of a course.
- Add a `scorm` component to your Unit.
- Upload a zip file containing your content package. **The `imsmanifest.xml` file must be at the root of the zipped package. Make sure you don't have an additional directory at the root of the Zip archive.**
- Publish your content as usual.

## Development

### Setup

To setup the development environment:

- create a Python3 virtualenv. If direnv is installed a `direnv allow` should be enough.
- install derex with `pip install -r requirements.txt`
- setup the derex project. Read https://derex.page/quickstart.html#quickstart for further informations.

### Development and Debugging

In order to be able to develop and debug effectively some steps may be taken:

- get a shell inside the container:

  ```
  cd derex_project
  ddc-project exec cms sh
  ```

- setup the package in editable mode. This will allow for testing changes without the need to reinstall the package:

  `pip install -e /openedx/derex.requirements/abstract_scorm_xblock`

- launch the Django debug server manually and bind it on port `81`:

  `python manage.py cms runserver 0:81`

- on your browser https://studio.scorm.localhost:81 should now be available. You should now be able to insert debug code in both Python and JS files and benefit from Django runserver auto reload feature.

### Running tests

Tests can be run from the derex project directory by running:

    `ddc-project run --rm lms python manage.py lms test abstract_scorm_xblock --keepdb`

The first time this command is run it will initialize the test database. Remove the `--keepdb` flag if you want the test database to be created/destroyed each time.

## TODO

- Update tests
- Delete old SCORM packages

## Caveats

- If a SCORM package is deleted from the course "Files & Uploads" section, the Import/Export functionality will export a course with a broken XBlock.
