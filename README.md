Veta Client
===========

Python novaclient extension for Veta (https://github.com/gridcentric/veta).

Installation
------------

To install the Veta novaclient extension, clone the repository and run:

    sudo python setup.py install

Use
---

To see a list of Veta commands, use `nova help`:

    $ nova help |grep backup-schedule
    backup-schedule-add
    backup-schedule-clear
    backup-schedule-delete
    backup-schedule-disable
    backup-schedule-enable
    backup-schedule-list
    backup-schedule-list-backups
    backup-schedule-update

Each command has contextual help:

    $ nova help backup-schedule-add
    usage: nova backup-schedule-add <server> <frequency> <retention>

    Add a backup schedule rule to this instance.

    Positional arguments:
      <server>     ID or name of the instance
      <frequency>  Frequency with which to perform backups (e.g. 10m, 1h, 1d
      <retention>  Number of backups to retain (e.g. 1h, 1d, 1w)

To add a backup schedule to an instance, use the `nova backup-schedule-add` command:

    $ nova backup-schedule-add test 1h 1d
    +------------+------------+------------------+--------+
    | ID         | Frequency  | Retention        | Active |
    +------------+------------+------------------+--------+
    | b-3xn7n87k | Every hour | For the last day | True   |
    +------------+------------+------------------+--------+

To list backup schedules for an instance, use the `nova backup-schedule-list` command:

    $ nova backup-schedule-list test
    +------------+------------+------------------+--------+
    | ID         | Frequency  | Retention        | Active |
    +------------+------------+------------------+--------+
    | b-3xn7n87k | Every hour | For the last day | True   |
    +------------+------------+------------------+--------+

To list backups of an instance, use the `nova backup-schedule-list-backups` command:

    $ nova backup-schedule-list-backups test
    +--------------------------------------+----------------------------+----------------+
    | ID                                   | Timestamp                  | Schedules      |
    +--------------------------------------+----------------------------+----------------+
    | 87a1b15b-7acc-4fe4-a6ad-2df4f2415bcd | 2013-10-15T23:56:00.000000 | ["b-3xn7n87k"] |
    | c928dad2-cdbb-4b73-9d91-437f63e703d5 | 2013-10-16T00:56:00.000000 | ["b-3xn7n87k"] |
    +--------------------------------------+----------------------------+----------------+

To delete a backup schedule, and all associated backups, use the `nova backup-schedule-delete` command:

    $ nova backup-schedule-delete test b-3xn7n87k

To delete all backup schedules for an instance, use the `nova backup-schedule-clear` command:

    $ nova backup-schedule-clear test

Backup schedules can be disabled, enabled, and updated using the `backup-schedule-disable`, `backup-schedule-enable`, and `backup-scehdule-update` commands, respectively.
