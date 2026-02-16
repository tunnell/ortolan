# Coin-Flip Password Generator

**[Use it here](https://tunnell.github.io/coin_flip_password_generator/coinflip-password-generation.html)** — works offline, no dependencies.

Generate truly random AES-128 or AES-256 keys using nothing but a fair coin — no electronics, no software RNG, no trust required.

Copyright @tunnell 2026

## What is this?

A printable reference card that lets you generate a cryptographically strong password by flipping a coin. The scheme uses a 32-character alphabet (`a–z` + `0–5`), which maps perfectly to 5-bit groups with zero waste (2⁵ = 32). Dot separators are inserted every 5 characters for readability and carry no entropy.

| Mode    | Flips | Password Length | Output Example                          |
|---------|-------|-----------------|-----------------------------------------|
| 128-bit | 128   | 26 characters   | `j0nkt.rw2fm.ahplq.s31ux.bcedy.g`      |
| 256-bit | 256   | 52 characters   | `j0nkt.rw2fm.ahplq.s31ux.bcedy.(...)`  |

## Why?

- **Verifiably random**: A coin flip is the simplest physical source of unbiased entropy. No CSPRNG, no `/dev/urandom`, no hardware RNG to trust.
- **Air-gapped**: The entire process happens on paper. No computer touches the key material until you type it in.
- **Auditable**: The procedure is simple enough to verify by hand. Anyone can check that the mapping is a bijection and that no entropy is lost.

## Files

| File | Purpose |
|------|---------|
| `coinflip-password-generation.html` | The printable reference card with lookup tables, procedures, worksheets, and security notes. Open in any browser. |
| `README.md` | This file. |
| `LICENSE` | License. |

## Usage

1. Open `coinflip-password-generation.html` in a browser (works fully offline — no JavaScript dependencies, no network requests).
2. Print it out, or use it on-screen.
3. Pick 128-bit or 256-bit mode.
4. Flip a coin, look up each 5-bit group in Table A, write down the character.
5. Insert a `.` every 5 characters for readability.
6. Enter the password (dots included) into your software.

## Security Considerations

The reference card includes detailed, research-backed security notes with full academic citations. Key points:

### Coin bias is negligible
- **Bartoš et al. (2023)**: 350,757 flips by 48 people — measured same-side bias of **50.8%**. Heads-vs-tails: 50.0% (no bias). Entropy cost: 0.018 bits over 128 flips.
- **Diaconis, Holmes & Montgomery (2007)**: Identified the precession mechanism causing same-side bias. Predicted ~51%, confirmed by Bartoš.
- **No coin type matters**: 46 different coins tested, no denomination or country showed heads-tails bias when flipped.
- **Von Neumann extractor**: Optional debiasing technique that produces perfectly unbiased output at ~4 flips per fair bit.

### Why coins, not dice or digital RNGs
- **Coins can't be tampered with**: A coin from your pocket has no supply chain to intercept. Dice must be purchased, creating an interception point.
- **Digital RNGs have been catastrophically compromised**: Dual_EC_DRBG (NSA backdoor, 2006–2013), Debian OpenSSL (CVE-2008-0166, 20 months of ~15-bit entropy), Intel RDRAND (unauditable, CrossTalk vulnerability).
- **Physical randomness is observable and verifiable**: You can see every flip. No firmware, no trust required.

### Critical: Always FLIP, never SPIN
- Spinning coins on a surface introduces large biases (US pennies: ~55% tails, Belgian €1: ~56% heads when spun).
- Flip with your thumb and catch in hand.

### Physical security
- **Paper impressions**: ESDA recovers writing through 7+ pages, persisting 60+ years. Write on isolated sheets; shred 8 pages if you used a notepad.
- **Electromagnetic emanations**: Keyboard EM radiation recoverable at 20m through walls (Vuagnoux & Pasini, 2009). Use interior rooms and auditable hardware.
- **Shoulder surfing**: 100% success rate in unprotected scenarios. Use a "bedsheet SCIF" for visual privacy during generation and entry.
- **Destruction**: Cross-cut shredding minimum (DIN P-4). For high security: wet pulping or burning to complete ash.

### Cryptographic strength
- **AES-128**: NIST-approved, classically secure. ~64-bit effective under Grover's quantum algorithm.
- **AES-256**: ~128-bit post-quantum security. NIST recommendation for long-term data.
- **KDF required**: Software must apply PBKDF2/Argon2/HKDF (standard in VeraCrypt, LUKS, KeePass).

### Prior art
Builds on Diceware (Reinhold, 1995), EFF wordlists (Bonneau, 2016), Glacier Protocol, ColdCard dice rolls, BlueWallet manual entropy, Sia Foundation's coins-in-a-cup method (Vorick, 2020), and ICANN DNSSEC key ceremonies.

## Contributing

Issues and PRs welcome. This is a simple reference card — the main value is in correctness and clarity. If you spot an error in the mapping tables or security guidance, please open an issue.

## License

See [LICENSE](LICENSE).
