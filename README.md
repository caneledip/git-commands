## Using Git

[Basics](#basics)  
[Adding and Changing Things](#adding-and-changing-things)  
[Undo Changes and Recover Files](#undo-changes-and-recover-files)  
[Viewing Commits](#viewing-commits)  
[Branch and Merge](#branch-and-merge)  
[Commands for Remotes](remote-commands.md)  
[Favorites](#favorites)  
[Resources](#resources)

#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.

## Basics

1. When using Git locally, what are these? Define each one in a sentence

   - Staging area - An in between area that store a to-be commit files
   - Working copy - File that has been check out and modifies, but not yet commited
   - master - A main branch that is always deployable
   - HEAD - The pointer to the branch current reference

2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email. These values are used in commits that you make:

   ```
   # Git configuration commands for a new account
      git config --global user.name "your name"
      git config --global user.email your.email
   ```

3. There are 2 ways to create a local Git repository. Briefly descibe each one:
   - Create local repo : git init
   - Clone the existing repo : git clone url localDirectory name

## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:

```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```

1. Add README.md and _everything_ in the `src` directory to the git staging area.

   ```
   git add README.md
   git add src
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).

   ```
   git add test/test_a.py
   ```

3. List the names of files in the staging area.

   ```
   git status
   ```

4. Remove `README.md` from the staging area. This is **very useful** if you accidentally add something you don't want to commit.

   ```
   git rm README.md
   ```

5. Commit everything in the staging area to the repository.

   ```
   git commit -m "commit all file in stageing area"
   ```

6. In any project, there are some files and directories that you **should not** commit to git.  
   For a Python project, name _at least_ files or directories that you should not commit to git:

   - Packaging files
   - Unit test files
   - \_\_pycache\_\_

7. Command to move all the .py files from the `src` dir to the top-level directory of this repository. This command moves them in your working copy _and_ in the git repo (when you commit the change):

   ```
   git mv src/*
   ```

8. In this repository, create your own `.gitignore` file that you can reuse in other Python projects. Add everything that you think is relevant.

   ```
   # Byte-compiled / optimized / DLL files
   __pycache__/
   *.py[cod]
   *$py.class

   # C extensions
   *.so

   # Distribution / packaging
   .Python
   build/
   develop-eggs/
   dist/
   downloads/
   eggs/
   .eggs/
   lib/
   lib64/
   parts/
   sdist/
   var/
   wheels/
   share/python-wheels/
   *.egg-info/
   .installed.cfg
   *.egg
   MANIFEST

   # PyInstaller
   #  Usually these files are written by a python script from a template
   #  before PyInstaller builds the exe, so as to inject date/other infos into it.
   *.manifest
   *.spec

   # Installer logs
   pip-log.txt
   pip-delete-this-directory.txt

   # Unit test / coverage reports
   htmlcov/
   .tox/
   .nox/
   .coverage
   .coverage.*
   .cache
   nosetests.xml
   coverage.xml
   *.cover
   *.py,cover
   .hypothesis/
   .pytest_cache/
   cover/

   # Translations
   *.mo
   *.pot

   # Django stuff:
   *.log
   local_settings.py
   db.sqlite3
   db.sqlite3-journal

   # Flask stuff:
   instance/
   .webassets-cache

   # Scrapy stuff:
   .scrapy

   # Sphinx documentation
   docs/_build/

   # PyBuilder
   .pybuilder/
   target/

   # Jupyter Notebook
   .ipynb_checkpoints

   # IPython
   profile_default/
   ipython_config.py

   # pyenv
   #   For a library or package, you might want to ignore these files since the code is
   #   intended to run in multiple environments; otherwise, check them in:
   # .python-version

   # pipenv
   #   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
   #   However, in case of collaboration, if having platform-specific dependencies or dependencies
   #   having no cross-platform support, pipenv may install dependencies that don't work, or not
   #   install all needed dependencies.
   #Pipfile.lock

   # poetry
   #   Similar to Pipfile.lock, it is generally recommended to include poetry.lock in version control.
   #   This is especially recommended for binary packages to ensure reproducibility, and is more
   #   commonly ignored for libraries.
   #   https://python-poetry.org/docs/basic-usage/#commit-your-poetrylock-file-to-version-control
   #poetry.lock

   # pdm
   #   Similar to Pipfile.lock, it is generally recommended to include pdm.lock in version control.
   #pdm.lock
   #   pdm stores project-wide configurations in .pdm.toml, but it is recommended to not include it
   #   in version control.
   #   https://pdm.fming.dev/#use-with-ide
   .pdm.toml

   # PEP 582; used by e.g. github.com/David-OConnor/pyflow and github.com/pdm-project/pdm
   __pypackages__/

   # Celery stuff
   celerybeat-schedule
   celerybeat.pid

   # SageMath parsed files
   *.sage.py

   # Environments
   .env
   .venv
   env/
   venv/
   ENV/
   env.bak/
   venv.bak/

   # Spyder project settings
   .spyderproject
   .spyproject

   # Rope project settings
   .ropeproject

   # mkdocs documentation
   /site

   # mypy
   .mypy_cache/
   .dmypy.json
   dmypy.json

   # Pyre type checker
   .pyre/

   # pytype static type analyzer
   .pytype/

   # Cython debug symbols
   cython_debug/

   # PyCharm
   #  JetBrains specific template is maintained in a separate JetBrains.gitignore that can
   #  be found at https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore
   #  and can be added to the global gitignore or merged into this file.  For a more nuclear
   #  option (not recommended) you can uncomment the following to ignore the entire idea folder.
   #.idea/
   ```

## Undo Changes and Recover Files

1. Display the differences between your _working copy_ of `a.py` and the `a.py` in the _local repository_ (HEAD revision):

   ```
   git diff
   ```

2. Display the differences between your _working copy_ of `a.py` and the version in the _staging area_. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):

   ```
   git diff --staged
   ```

3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.)

   ```
   git diff --cached
   ```

4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:

   ```
   git restore --staged main.py
   ```

5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository. This also works if you have deleted your working copy of this file.

   ```
   git restore a.py
   ```

6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit) Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)

   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   ```

   The command to reset HEAD and master to the commit id `bbbb`: git reset --hard head~2

7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   git reset aaaa
   ```
   Note:
   - Git won't let you do this if you have uncommitted changes to any "tracked" files.
   - Untracked files are ignored, so after doing this command they will still be in your working copy.

## Viewing Commits

1. Show the history of commits, using one line per commit:

   ```
   git log --oneline
   ```

   Some versions of git have an _alias_ "log1" for this (`git log1`).

2. Show the history (as above) including _all_ branches in the repository and include a graph connecting the commits:

   ```
   git log
   ```

3. List all the files in the current branch of the repository:
   ```
   git ls -files
   ```
   Example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```

## Branch and Merge

1. Create a new branch named `dev-foo`:
   ```
   git branch dev-foo
   ```
2. Display the name of your current branch:
   ```
   git branch
   ```
3. List the names of **all** branches, including remote branches:
   ```
   git branch -a
   ```
4. Switch your working copy to the branch named `dev-foo`:
   ```
   git checkout dev-foo
   ```
5. **Merge:** To merge the work from `dev-foo` into the master branch, perform these steps:

   1. step one : checkout to master branch
      ```
      git checkout master
      ```
   2. step two : merge dev-foo branch into master
      ```
      git merge dev-foo
      ```

6. **Extra:** Under what conditions a merge may fail.
   ```
   git can fail to merge when merging can overwritten your file or your merging is in conflicted with other user merge
   ```

## Favorites

1. Task of pushing code to github.

   ```
   git add -u filename
   git commit -m "comment"
   git push
   ```

---

## Resources

- [Git SCM](https://git-scm.com/) Free and open source for learning git.

- [Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable e-book is available, too.
- [Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.
- [Markdown Cheatsheet][markdown-cheatsheet] summary of Markdown commands.
- [Github Markdown][github-markdown] some differences in the way Github handles markdown and special Markdown for repos.

Learn Git Visually:

- [Learn Git Interactive Tutorial][LearnGitInteractive] great visual tutorial
- [Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
