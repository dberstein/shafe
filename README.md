# shafe

Better *sh*afe than *sh*orry ...

## Why?

Need to transmit sensitive information to a collegue? `shafe` is here to help:

Tada! A self-decrypting command is printed, which when sourced by collegue prompt for password and spits original content:

    $ echo 'suppose this is sensitive information from PID '$$ > sensitive.txt \
    && cat sensitive.txt | shafe | sh > decrypted.txt \
    && echo && echo "Decoded: $(cat decrypted.txt)"
    enter aes-256-cbc encryption password:
    Verifying - enter aes-256-cbc encryption password:
    enter aes-256-cbc decryption password:

    Decoded: suppose this is sensitive information from PID 17664

## How?

`shafe` wraps AES-256 symmetric encryption in a cat-pipe command to self-decrypt (`openssl enc`):

    $ echo 'suppose this is sensitive information from PID '$$ | shafe
    enter aes-256-cbc encryption password:
    Verifying - enter aes-256-cbc encryption password:
    #!/bin/sh
    cat <<'---EOS.24088.1611129716---' | openssl enc -aes256 -pbkdf2 -a -A -d
    U2FsdGVkX1/FLzyJ/dM//3er3HPOTtnREyMSaUwXfuiRaWpgN7Fg6mQANcvJ7uIIexUzepFHOkpPMl8xwBpdQdcNzagiE2GCsP6M6FT6lJQ=
    ---EOS.24088.1611129716---

## Installation

Place `shafe` somewhere in your `PATH`.

### Requirements

- `openssl enc` command
