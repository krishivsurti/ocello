# Security

## Reporting a vulnerability

Please **do not open a public issue** for security problems. Use GitHub's private reporting instead: **Security → Report a vulnerability** on this repository. Include the Ocello version, both platforms involved, and steps to reproduce. You can expect a reply within a few days, and a fix in the next release for confirmed issues.

## Supported versions

| Version | Supported |
|---|---|
| 3.2.1 | ✅ |
| 3.2.0 | ⚠️ Update to 3.2.1 |
| Earlier (Transti, Saffro, Mayur builds) | ❌ Update to the latest release |

## How Ocello protects transfers

Ocello is built for transfers between your own devices on a hotspot or Wi-Fi network. The threat it defends against is someone else on the same network.

**Encryption and identity**
- Every connection uses TLS. Each device creates its own P-256 key and certificate on first launch, stored in app-private storage.
- Senders pin the receiver's certificate by SHA-256 fingerprint; no certificate authority or internet access is involved, and plain HTTP is refused.
- When pairing, both screens show a six-digit verification code derived from the receiver's key and a random value from the sender. A device in the middle has a different key, so the codes would not match.
- Paired devices are remembered. The device list marks them **Paired**, marks unknown keys **New**, and warns when a device uses a paired device's name with a different key.

**Access control**
- Nothing is saved until you accept on the receiver, or the sender knows the six-digit pairing code shown on the receiver.
- 10 wrong pairing codes from one address lock it out for 10 minutes. The code changes after repeated guessing or after you cancel an incoming transfer.
- Session tokens are tied to the sender's address and expire after 5 idle minutes; cancelling revokes them.
- Only one approval prompt can be open at a time, with a 30-second cooldown after a decline. The prompt shows the sender's IP address.
- Only private IPv4 addresses (10.x, 172.16–31.x, 192.168.x) can connect.

**Safe saving**
- File names are cleaned up: characters Windows cannot store become `_`, device names such as `CON` are renamed, and `..` is refused.
- Every write is checked to stay inside the save folder, even through symbolic links or junctions.
- Programs, scripts, shortcuts, installers and archives received on Windows get the "downloaded from the internet" mark, so SmartScreen checks them before they run.
- Interrupted files are removed; completed files are kept.

## Known limitations

- **Connecting by address** (instead of picking a nearby device) trusts the key that answers at that address on first contact, without a verification code.
- **Discovery** checks the local subnet every 15 seconds and shows this device's name to others on the network. Turn off *Automatic discovery* and *Allow incoming transfers* on networks you do not trust.
- **The Windows app is not code-signed**, so SmartScreen shows "Unknown publisher" on first run. Check downloads against `SHA256SUMS.txt` in each release.
- **All files access** on Android is requested only if you choose a save folder outside Downloads.

See also the [privacy policy](PRIVACY.md).
