# Anofuss Upload

Upload file(s) from a `source` to a specific `target` on `host` without depending on untrusted/unknown docker images or javascript libraries.

In other words: a no fuss upload action.

## Requirements

Depends on `rsync` and `openssh` (present in ubuntu-latest).

Paste the _private key_ (`SSH_KEY`) and _known_hosts_ (`KNOWN_HOST`) into two specific Actions secrets.

## Usage

### Minimal configuration

```yaml
runs-on: ubuntu-latest
steps:
- name: Deploy
  uses: vacare/anofuss-upload@v2
  with:
    host: example.com
    username: deploy
    key: ${{ secrets.SSH_KEY }}
    known_hosts: ${{ secrets.KNOWN_HOSTS }}
    source: build/lib/app.war
    target: /deploy
```

### Configuration using custom arguments

```yaml
runs-on: ubuntu-latet
steps:
- name: Deploy
  uses: vacare/anofuss-upload@v2
  with:
    host: example.com
    username: deploy
    key: ${{ secrets.SSH_KEY }}
    known_hosts: ${{ secrets.KNOWN_HOSTS }}
    # --delete   delete extraneous files from dest dirs
    # --checksum skip based on checksum, not mod-time & size
    arguments: '--delete --checksum'
    source: build/lib/app.war
    target: /deploy
```
