
---
name: Triage for Release
about: Checklist for upgrading to Learning Center 2.0
title: Triage for [Project Title] Release [X.X.X]
labels: 2.0 Release
assignees: ''

---

This is a checklist issue. As we review each repo we should check the following
items.

### 1. Check on file versions (all files below should have a version comment in the first line of the file)

- [ ] `misc/static/cyverse.css` is version 2.0
- [ ] `misc/static/cyverse.js` is version 2.0
- [ ] `misc/static/detail-expand.css` is version 2.0
- [ ] `misc/static/detail-expand.js` is version 2.0
- [ ] `misc/static/intercom-script-for-learning.js` is version 2.0
- [ ] `misc/static/question-answer.js` is version 2.0
- [ ] `misc/static/jquery.tablesorter.min.js` is version 2.0
- [ ] `misc/cyverse_spinx_conf.py` is version 2.0
- [ ] `conf.py` is version 2.0 and you have updated the name of the documentation (check the project =' line, your `index.rst` should have
the appropriate name)
- [ ] `cyverse_rst_defined_substitutions.txt` is version 2.0
- [ ] `License.md` is version 2.0

### 2. Check on the following required formatting for all pages

- [ ] All `.rst` pages begin with the following
    ````
    .. include:: cyverse_rst_defined_substitutions.txt
    .. include:: custom_urls.txt

     |CyVerse_logo|_

    |Home_Icon|_
    `Learning Center Home <http://learning.cyverse.org/>`_
    ````
- [ ] Documentation contains maintainer info on `index.rst` or the appropriate
  first page. This should be placed directly before the table of contents.

    ````
    Manual Maintainer(s)
    ------------------------

    Who to contact if this manual needs fixing. You can also email
    `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

    .. list-table::
        :header-rows: 1

        * - Maintainer
          - Institution
          - Contact
       * - Your Name
          - CyVerse / UA
          - Yourname@email.com
    ````

- [ ]  Documentation contains the fix/improve instructions on all `.rst` pages
    ````
    **Fix or improve this documentation**

    - Search for an answer:
       |CyVerse Learning Center|
    - Ask us for help:
      click |Intercom| on the lower right-hand side of the page
    - Report an issue or submit a change:
      |Github Repo Link|
    - Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_
    ````

- [ ] All hyperlinks in documentation are on the repo's `custom_urls.txt` or `cyverse_rst_defined_substitutions.txt`
 **Note**:  We want to avoid:
    -  Best practice is to AVOID inline hyperlinks
    -  Where possible links should NOT be on the `.rst` page but on a single
        document that is included. (e.g. `custom_urls.txt` or `cyverse_rst_defined_substitutions.txt`)
    - `custom_urls.txt` should be for URLS specific to that repo
    - `cyverse_rst_defined_substitutions.txt` is a list of generic links to
       other CyVerse and Learning Center pages
    - Links should have the form below and open in a new tab:
        ````
            .. |Link Title| raw:: html

           <a href="https://LINK.URL" target="blank">Link Title</a>

        ````
- [ ] Check the |Github Repo Link| on each .rst page and ensure it links to the correct GitHub repository for this documentation.       


### 3. Overall quality  

- [ ] Maintainer is assigned and has approved the content
- [ ] Editor has checked for quality (spelling, formatting, etc.)
- [ ] Sample/test data is available with anonymous/public read access
      in the appropriate directory at `/iplant/home/shared/cyverse_training`
