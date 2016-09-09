# Easy Mac OS X setup with Ansible

My own OS X setup, shamelessly copied from [Joeri](https://github.com/jverdeyen), modified to my own needs.

## Requirements

- Xcode `xcode-select --install`
- Homebrew `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" && export PATH=/usr/local/bin:$PATH`
- Git `brew install ansible git`

## Installation

Before you (can) run the playbooks, you should (need) to configure them.

### Configuration

Start by duplicating `vars.yml.dist` to `vars.yml` and adjust it to your own needs.

```
cp vars.yml.dist vars.yml
```

### Running playbooks

Run all playbooks:

```
ansible-playbook setup.yml --ask-sudo-pass
```

Or run specific tagged roles:

```
ansible-playbook setup.yml --tags osx --ask-sudo-pass
```

### Application Settings

Application settings are synced with dropbox using [Mackup](https://github.com/lra/mackup).
Once the playbooks finished running, wait until dropbox is synced and run `mackup restore`.

## Issues

- `ERROR:  While executing gem ... (Gem::FilePermissionError)\n    You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.`

  Change owner of the gem folder `sudo chown -R user:group /Library/Ruby/Gems/2.0.0` ([source](http://stackoverflow.com/a/11644182/705529))

# Inspired by
* [osx-for-hackers.sh](https://gist.github.com/brandonb927/3195465)
* [ideasonpurpose/ansible-playbooks](https://github.com/ideasonpurpose/ansible-playbooks)
* [mackup](https://github.com/lra/mackup)
* [macplan](https://github.com/jverdeyen/macplan)
