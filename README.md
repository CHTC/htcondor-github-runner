# HTCondor-based GitHub Runners

This repo implements the logic necessary to run GitHub runners as virtual machines managed by a [HTCondor](https://htcondor.org) system.

From an HTCondor access point, one can run:

```
htcondor-gh-runner -org chtc --repo pelican --token-file token_file --working-dir working_dir1 --group ghrunner-1
```

The script will generate a DAG and maintain a workforce of GitHub runners.  The `--max-idle` argument (default 3) controls the maximum number of idle runners allowed at a given time;
the number of runners will be decreased if there are too many idle.  The `--max-runners` argument (default 10) controls the maximum total number of runners.

Notes:
- The runner can be attached to either a repository or an entire organization.
- The token_file should contain a GitHub personal access token.  These tokens must have `admin` read/write rights to the repository or organization specified.
- Only one DAG can be running for a runner "group".  If you start multiple sets of runners, ensure they all use unique group names.
- The VM image is taken from the OSDF; the current default is `osdf:///chtc/PUBLIC/bbockelm/alma_9.2-v4.qcow2`.
