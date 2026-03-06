# Physical Entropy Password Generator

**[Use it here](https://tunnell.github.io/physical_entropy_password_generator/physical-entropy-password-generator.html)** — works offline, no dependencies.

Generate truly random 256-bit keys using coins or dice — no electronics, no software RNG, no trust required.

Copyright @tunnell 2026

## What is this?

A printable reference card that lets you generate a cryptographically strong password using physical randomness. Two methods are supported:

| Method | Actions | Password | Entropy | Alphabet |
|--------|---------|----------|---------|----------|
| **Coin** | 256 flips | 52 characters | 256 bits | a–z, 0–5 (32 chars) |
| **Dice** | 50 rolls of 2d6 | 50 characters | 258.5 bits | a–z, 0–9 (36 chars) |

Both methods use zero-waste encoding: coins map 5 bits to 32 characters (2⁵ = 32), dice map two d6 rolls to 36 characters (6 × 6 = 36).

## Why?

- **Verifiably random**: Coin flips and dice rolls are observable physical entropy sources. No CSPRNG, no `/dev/urandom`, no hardware RNG to trust.
- **Air-gapped**: The entire process happens on paper. No computer touches the key material until you type it in.
- **Auditable**: The procedure is simple enough to verify by hand. Anyone can check that the mapping is a bijection and that no entropy is lost.

## Files

| File | Purpose |
|------|---------|
| `physical-entropy-password-generator.html` | The printable reference card with lookup tables, procedures, worksheets, and security notes. Open in any browser. |
| `README.md` | This file. |
| `LICENSE` | License. |

## Usage

1. Open `physical-entropy-password-generator.html` in a browser (works fully offline — no JavaScript dependencies, no network requests).
2. Print it out, or use it on-screen.
3. Choose **Coin** or **Dice** tab.
4. Follow the procedure:
   - **Coin**: Flip 256 times, look up each 5-bit group in Table A (plus 1 final bit in Table B).
   - **Dice**: Roll two dice 50 times, look up each pair in Table D.
5. Insert a `.` every 5 characters for readability.
6. Enter the password (dots included) into your software.

## Security Considerations

The reference card includes detailed, research-backed security notes with full academic citations.

### Coin bias is negligible
- **Bartoš et al. (2023/2025)**: 350,757 flips by 48 people using 44 different coins — measured same-side bias of **50.8%**. Heads-vs-tails: 50.0% (no bias). Entropy cost: 0.036 bits over 256 flips.
- **Diaconis, Holmes & Montgomery (2007)**: Identified the precession mechanism causing same-side bias.
- **Von Neumann extractor**: Optional debiasing technique that produces perfectly unbiased output at ~4 flips per fair bit.

### Dice bias is negligible and unknowable
- **Campbell & Wimsatt (2019)**: Detecting whether a die is unfair requires ~3,000 rolls. Most commodity d6 dice tested fair.
- **Key insight**: An attacker doesn't know which dice you used or their specific bias. Each die's imperfections are unique and small.
- **No debiasing needed**: A ~1–2% bias per face, spread across 50 rolls, reduces entropy by a fraction of a bit.

### Why coins or dice, not digital RNGs
- **Physical objects can't be backdoored**: A coin from your pocket or dice from a board game has no supply chain to intercept.
- **Digital RNGs have been catastrophically compromised**: Dual_EC_DRBG (NSA backdoor, 2006–2013), Debian OpenSSL (CVE-2008-0166, 20 months of ~15-bit entropy), Intel RDRAND (unauditable, CrossTalk vulnerability).
- **Physical randomness is observable and verifiable**: You can see every flip or roll. No firmware, no trust required.

### Critical technique notes
- **Coins**: Always FLIP, never SPIN. Spinning introduces large biases (~55% tails for US pennies).
- **Dice**: Must bounce and tumble — don't drop flat or slide. Use a dice tray or box lid.

### Physical security
- **Paper impressions**: ESDA recovers writing through 7+ pages. Write on isolated sheets; shred 8 pages if you used a notepad.
- **Electromagnetic emanations**: Keyboard EM radiation recoverable at 20m through walls (Vuagnoux & Pasini, 2009). Use interior rooms and auditable hardware.
- **Shoulder surfing**: 100% success rate in unprotected scenarios. Use a "bedsheet SCIF" for visual privacy during generation and entry.
- **Destruction**: Cross-cut shredding minimum (DIN P-4). For high security: wet pulping or burning to complete ash.

### Cryptographic strength
- **256-bit security**: Both methods exceed 256 bits of entropy, providing ~128-bit post-quantum security (Grover's algorithm).
- **KDF required**: Software must apply PBKDF2/Argon2/HKDF (standard in VeraCrypt, LUKS, KeePass).

### Prior art
Builds on Diceware (Reinhold, 1995), EFF wordlists (Bonneau, 2016), Glacier Protocol, ColdCard dice rolls, BlueWallet manual entropy, Sia Foundation's coins-in-a-cup method (Vorick, 2020), and ICANN DNSSEC key ceremonies.

## Contributing

Issues and PRs welcome. This is a simple reference card — the main value is in correctness and clarity. If you spot an error in the mapping tables or security guidance, please open an issue.

## License

See [LICENSE](LICENSE).
