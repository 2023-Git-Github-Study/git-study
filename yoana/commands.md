# Terminal Commands

- LOCAL DIRECTORY INTO GIT REPO

  - git init

- CLONE EXISTING REPO

  1. Same directory name:
     - `git clone url`
       - git clone https://github.com/yewonyoana/git-study
  2. Different directory name:
     - `git clone url name`
       - git clone https://github.com/yewonyoana/git-study git-study-2023

- STATUS OF GIT FILES

  - `git status`

- TRACK NEW FILES

  1. For all files:
     - `git add .`
  2. For individual files:
     - `git add file_name`
       - git add README.md
  3. For individual folder:
     - `git add folder_name/`
       - git add practice/
  4. For an individual file in a folder:
     - `git add folder_name/ file_name`
       - git add practice/ chapter_one.txt

- COMMIT FILES

  1. Without message:

  - `git commit`

  2. With message:

  - `git commit -m "message"`
    - git commit -m "Updated README.md"

  3. All changes and skipping staging area:

  - `git commit -a`

- REMOVE FILES FROM STAGING AREA

  - `git rm`

- MOVE FILES
  - `git mv file_from file_to`
    - git mv REAME.md README
