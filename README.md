quora-backup
============

A syncing approach to backing up Quora answers, questions, votes, and follows. Rather than fetching your entire history of Quora activity all at once, quora-backup checks your recent Quora activity and saves only the new entries. **Run it regularly to maintain a full backup.** This not only allows backups to be performed faster and more frequently, but also makes less requests to Quora's servers and doesn't face request rate-limiting issues like some older backup techniques do. It supports backing up to **JSON and CSV**. More file formats and databases to come.

### Table of Contents
* [Installation](#installation)
* [Usage](#usage)
    * [Backup Formats](#backup-formats)
    * [Specifying an Activity](#specifying-an-activity)

## Installation
You will need [Python 2](https://www.python.org/download/). [pip](http://pip.readthedocs.org/en/latest/installing.html) is recommended for installing dependencies.

    $ git clone https://github.com/csu/quora-backup.git
    $ cd quora-backup
    $ pip install -r requirements.txt

## Usage

    $ python backup.py Christopher-J-Su  # defaults to flat-file json backups

To access the help for the options and arguments:

    $ python backup.py --help
    Usage: backup.py [OPTIONS] USER

    Options:
      -p, --path TEXT                 Specify a path at which to store the
                                      backup files.
      -t, --type [answers|questions|upvotes|question_follows]
                                      Specify only one type of activity to be
                                      backed up.
      -f, --format [json|csv]
      --help                          Show this message and exit.

### Backup Formats
To specify a format for your backup:

    $ python backup.py --format csv Christopher-J-Su

For a list of available backup formats, read the help (see [Usage](#usage) section).

#### JSON Backup Details
Your content will be stored in the following files, in whatever directory you run the above command in:

    answers.json
    questions.json
    upvotes.json
    question_follows.json

#### CSV Backup Details
Your content will be stored in the following files, in whatever directory you run the above command in:

    answers.csv
    questions.csv
    upvotes.csv
    question_follows.csv

The resulting CSV output will have columns (fields/attributes) delimited by commas and rows (entries) delimited by new lines. The first row will be a header row, containing the names of the fields.

### Specifying an Activity
You can also specify only one activity to be backed up. For instance, to only back up answers:

    $  python backup.py --type answers Christopher-J-Su