# Solana Validator Identity Transition
During a software upgrade, or for any other reason warranting a failover to a secondary node, you can use these Ansible playbooks to move your voting identity from a Primary Node to a Backup Node, and vice versa. These scripts are modeled after mvine's [original guide](https://github.com/mvines/validator-Identity-transition-demo) on Validator Identity Transition Demo

## Disclaimers
- SINGLE IP ADDRESS \
  As of now, we have only tested this on two nodes running behind the same public facing IP. If your public node IPs are different, that may cause unexpected behavior.

- RELIABLE CONNECTION \
  These scripts will work assuming you have a reliable and fast connection (10 mbps or better) from your Ansible host to both Primary and Secondary validator hosts. Slower/unreliable connection might cause corruption in the moved tower file resulting in unexpected validator behavior and possibly accidental slashing if network doesn't agree with the tower file content.

## Variables (change per env)
Make sure below variables are set according to your setup.

In the `hosts` file, replace below:
- `solana-host-primary` is a placeholder for your primary node IP/Host Name
- `solana-host-secondary` is a placeholder for your secondary node IP/Host Name
- `solana_user` is a placeholder for the user on both primary/secondary nodes where Ansible host has access to (via ssh keys)

In both `*.yml` files, *for both hosts*, replace below:
- `solana_cli_path` is the path to solana installation. If you installed [following the official doc](https://docs.solana.com/cli/install-solana-cli-tools#macos--linux), it would be located at:
  ```shell
  /home/solana/.local/share/solana/install/active_release/bin
  ```
- `solana_keys_path` is the path to where these keys are stored:
  - staked-identity.json (On Primary Node)
  - primary-unstaked-identity.json (On Primary Node)
  - secondary-unstaked-identity.json (On Secondary Node)
- `ledger_path` is the path to the ledger dir (where tower is stored on the voting node)
