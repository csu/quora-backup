# Quora Backup

#### Note: parts of this script may be broken due to changes on Quora's end. Please open issues and make pull requests regarding this at [csu/pyquora](http://github.com/csu/pyquora).

A syncing approach to backing up Quora answers, questions, votes, and follows. Rather than fetching your entire history of Quora activity all at once, quora-backup checks your recent Quora activity and saves only the new entries. **Run it regularly to maintain a full backup.** This not only allows backups to be performed faster and more frequently, but also makes less requests to Quora's servers and doesn't face request rate-limiting issues like some older backup techniques do. It supports backing up to **JSON and CSV**. More file formats and databases to come.

### Table of Contents
* [Installation](#installation)
* [Usage](#usage)
    * [Backup Formats](#backup-formats)
    * [Specifying an Activity](#specifying-an-activity)

## Installation
You will need [Python 2](https://www.python.org/download/). [pip](http://pip.readthedocs.org/en/latest/installing.html) is recommended for installing dependencies.

```bash
$ git clone https://github.com/csu/quora-backup.git
$ cd quora-backup
$ pip install -r requirements.txt
```

### Installing without git
For the less technical users who want to use quora-backup without installing git:

1. [Download quora-backup](https://github.com/csu/quora-backup/archive/master.zip) and extract the files from the `.zip` archive

2. Open a terminal or command prompt window and enter the folder using `cd`

3. Run `pip install -r requirements.txt` (after installing Python and pip)

## Usage
```bash
$ python backup.py Christopher-J-Su  # defaults to flat-file json backups
```

To access the help for the options and arguments:

```bash
$ python backup.py --help
Usage: backup.py [OPTIONS] USER

Options:
  -p, --path TEXT                 Specify a path at which to store the backup
                                  files.
  -t, --type [answers|questions|upvotes|user_follows|review_requests]
                                  Specify only one type of activity to be
                                  backed up.
  -f, --format [json|csv|mongodb]
                                  Specify a format for the backup. Defaults to
                                  JSON.
  -m, --mongodburi TEXT           Specify a MongoDB URI. If not specified,
                                  tries localhost.
  --help                          Show this message and exit.
```

### Backup Formats
To specify a format for your backup:

```bash
$ python backup.py --format csv Christopher-J-Su
```

For a list of available backup formats, read the help (see [Usage](#usage) section).

#### JSON Backup Details
Your content will be stored in the following files, in whatever directory you run the above command in:

    answers.json
    questions.json
    upvotes.json
    user_follows.json
    review_requests.json

#### CSV Backup Details
Your content will be stored in the following files, in whatever directory you run the above command in:

    answers.csv
    questions.csv
    upvotes.csv
    user_follows.csv
    review_requests.csv

The resulting CSV output will have columns (fields/attributes) delimited by commas and rows (entries) delimited by new lines. The first row will be a header row, containing the names of the fields.

### Specifying an Activity
You can also specify only one activity to be backed up. For instance, to only back up answers:

```bash
$  python backup.py --type answers Christopher-J-Su
```
