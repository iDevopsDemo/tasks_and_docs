# Checklist for Contributions to Siemens Inner Source Projects

Please ensure that you are familiar with the current **Licensing, IPR, Privacy
Policy and ECC** [documentation](README.md).

Every planned contribution to Siemens Inner Source projects has to be audited
with the following checklist to ensure that the **business interests of the BU
and the reputation of the contributors are protected**.

> This checklist introduces general contribution guidelines and is not meant to be used in any "clearing" related
processes. Each Siemens legal entity might implement its own Inner Source contribution process according to
domain-specific practices and legal requirements, make sure you follow this process first.

* **Do not "release"** any code or other material without having received
  permission from the person with the proper authority within Siemens.

* **Do not "release"** any code or other material without review from an
  experienced developer. _"release" means that the code will be integrated in a
  product or delivered to a customer._

* **Do not contribute** any code from 3rd parties to Siemens Inner Source
  projects, i.e. do not copy code from code sharing sites (stackoverflow,
  codeguru,...), open source projects, commercial code available in source code
  form, books, journals, etc.).

* **Do not remove** copyrights and/or license references and/or license texts.

* If an entire package will be contributed, ensure that the text of the [Siemens
  Inner Source License](https://code.siemens.com/licenses/Siemens_Inner_Source_License)
  is provided in the file `LICENSE.md` in the root directory of the project.

* Additionally, create a file `COPYING.md` with an appropriate copyright notice. E.g.:

  ```txt
  Copyright YEAR Siemens AG
  Licensed under the Siemens Inner Source License 1.4 or at your option any later version
  ```

* Include a link to the files `LICENSE.md` and `COPYING.md` in the `README.md` of your project

* Ensure that the comments and file headers **do not contain**:
  * product and/or project names, release numbers and their release dates
  * inappropriate language
  * any words and/or phrases like "stolen from" or "copied from". A
    contribution is a serious matter and not the place for jokes. If you have
    the need to provide information like "derived from" ensure that you also
    provide the "license information" of the code you derived from.

* Ensure that files to **do not contain**:
  * configuration information
  * credentials for real IT-environments, like server names, IP-addresses,
    login information, or passwords.

* Write code in accordance with the applicable **coding style**.

* **Do notify** the authors/maintainers of projects under the Siemens Inner
  Source License if you find code or other parts failing to fulfill the
  requirements of the license or this checklist.

* Apply this checklist also to contributions based on code from other Inner
  Source Projects.
