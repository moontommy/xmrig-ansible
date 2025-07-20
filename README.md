# xmrig-ansible

An Ansible role for XMRig for modern Linux distros using Systemd.

This repo was created because the alternatives missed 2 things:
- They didn't support Systemd
- They didn't allow to build from source

You can use it stand-alone or integrate into your existing Ansible repo.

The follow functionality is supported by this role:
- Clone the XMRig repo and build it from source
- Download the binary to your system
- Create a Systemd service and configure it to run at boot

Currently the role only supports rpm-based distros (like Fedora, Centos-stream, RHEL, ...)

Support for Debian-based distros is planned for the future.

## Getting started

Create a new inventory file or edit an existing one.

### Required variables

Set the following variables in your host_vars or group_vars:

If you are mining on Unmineable, you only need to set your wallet:

```
xmrig_pool_wallet: "<your_wallet_address>"
```

If you want to use a different pool, set the url and potentially, the password:

```
xmrig_pool_url: "<your_pool_url>"
xmrig_pool_pass: "<your_password>"
```

You may also want to set a name for your worker and a referral if your pool supports it:

```
xmrig_pool_worker: "<your_worker_name>"
xmrig_pool_referral: "<your_referral>"
```

Use Unmineable with the default referral to support this project. (See `Sponsor Pool` below)

### Download instead of build from source

This role was originally created to support building XMRig from scratch but can also download the binary directly to save time.

To have it download the binary directly, set the following variables:

```
xmrig_build_source: false
xmrig_version: "<xmrig_version_you_want_to_use>"
```

### Running the playbook

Run the `mine.yml` playbook as user with sudo permissions:
```
ansible-playbook -u <sudo_user> -i <inventory_path> mine.yml
```

The playbook does not need to be run as root but does require sudo permissions to clone build and configure XMRig.

## Fedora dnf dependency error

The Ansible dnf module requires a Python library which might not be installed on a recent Fedora installation.

Run the following command to install it in case of dependency errors:
`sudo dnf install python3-libdnf5`

## Sponsor Pool

If you're still looking for an XMR pool to join, you can support this project by joining [Unminable](https://www.unmineable.com/?ref=sewz-utf5) via this affiliate link: <https://www.unmineable.com/?ref=sewz-utf5>
Or set xmrig_pool_referral to `sewz-utf5` (this is the default value) to lower your mining fee and support us.
