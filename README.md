# NCA Test Data

This repository houses a variety of publications for testing out [NCA][1]
(Newspaper Curation App).

All issues are separated into "scans" or "sftp" and their directory names are
always `[MOC-]LCCN-YYMMDDEE`. The "MOC" is required for scanned titles, and
must not be present for born-digital (sftp) issues. This is based on the NCA
testing setup (see that repository's "test" subdirectory for a deeper
explanation).

Most titles and issues are just test data that don't have anything "special"
about them, but some information is important to note, as there are issues
which are here specifically for the purpose of failing NCA's ingest.

- `scans/food-sn12345678-1913050801`: this issue begins with the MOC "food", a
  fake MOC meant to trigger an error in the NCA UI.
- `scans/oru-sn83008376-2017011301` (Daily Astorian): this issue is missing
  TIFFs and NCA won't allow it to be processed. Scanned issues, unlike
  born-digital issues, are required to have TIFFs.
  - It's also a duplicate of an issue which is live on oregonnews.uoregon.edu,
    so it should show that warning as well, though that isn't really relevant
    to devs loading test issues / testing NCA.
  - This is to a degree testing what happens if an upload goes into the "scan"
    location in NCA when it should have gone into the "born digital" location.
- `sftp/sn83008376-2017011301` (Daily Astorian): this simulates properly
  uploading the above "missing TIFFs" issue into the born-digital location. It
  will still display the "duplicate of a live issue" warning. It can be queued
  manually, but not automatically.
- `sftp/sn99063854-*` (Vernonia Eagle): All these are duplicates of live issues
  and will display that warning in the "uploaded issues" section. They have no
  other errors and therefore can be queued manually. They should *not*
  automatically queue up for ingest.
- `sftp/snfakeyfake-2001030501`: Invalid LCCN will trigger a title-level error
  in the uploads view.
- `sftp/2018252080-2015071701`: Issue containing invalid unicode characters
  which ONI can't ingest when older versions of NCA process the issue. Newer
  NCA will strip the broken unicode.

*In case it's not obvious: duplicate issues will only show their warnings if
NCA is configured such that UO's Historic Oregon Newspapers is the production
site. Duplicate detection is based on the configured production site.*

[1]: <https://github.com/uoregon-libraries/newspaper-curation-app>
