# ucarpha — CARP high availability for FreePBX 17

Downloads for **ucarpha**, a FreePBX 17 module that keeps a floating virtual IP between two stations with
[ucarp](https://github.com/jedisct1/UCarp), checks Asterisk health and fails over automatically.

**Download:** [latest release](../../releases/latest) — `ucarpha-<version>.tgz` (Module Admin archive) and an optional `.deb`.
Checksums are in `SHA256SUMS`.

> **Status: experimental.** Tested on a two-node lab of FreePBX 17.0.33 (Debian 12). The module is unsigned and includes
> root helpers that manage network addresses and services. Try it on a test pair before production.

## Install (on every node)
1. Download `ucarpha-<version>.tgz` and upload it in **Admin → Module Admin → Upload**, then install.
   The module is unsigned; if it is refused run `fwconsole setting SIGNATURECHECK 0` as root.
2. Open **Admin → CARP High Availability**. The page lists the steps still missing and links to the firewall:
   - `apt-get install ucarp` (as root);
   - once, as root: `sh /var/www/html/admin/modules/ucarpha/bin/setup-root.sh` (repeat after every module update);
   - add this node, the other node and the VIP to the firewall *Trusted* zone.
3. Enter the VIP, this node's IP, the peer IP, VHID, password and role, then Save. On the second node use the opposite
   role and the same VIP, VHID and password.

The page also has a built-in **Help** with removal steps and the locations of all files. Nothing is installed or changed
as root automatically.

## Features
Floating VIP · Asterisk health checks (process, CLI, SIP, MariaDB) · automatic restart · hand-over to a healthy peer only ·
pfSense-style *CARP Maintenance* buttons · scheduled hand-over · syslog/e-mail notifications · status JSON for Zabbix.

## License
GPL-3.0-or-later. The archive contains the complete source code of the module.
