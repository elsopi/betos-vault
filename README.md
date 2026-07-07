# Betos Vault

Encrypted backups of critical prod secrets. Files are encrypted
with age (`brew install age`) and safe to commit to a private git
repo — the ciphertext is useless without the private key.

## Encryption recipient (safe to publish)

Public age recipient: `age1abc...def456`  ← replace with your actual pubkey

To encrypt a new file for this vault:

    age -r age1abc...def456 -o secret.age plaintext-file
    git add secret.age && git commit -m "add secret" && git push

To decrypt (requires the private key, stored in Keychain +
paper backup):

    age -d -i ~/.age-key.txt secret.age > plaintext-file

## Recovery of private key

- macOS Keychain: `security find-generic-password -a "$USER" -s "betos-age-key" -w`
- Paper backup: in [where you stored it]
