# Ortolan

**[Use it here](https://tunnell.github.io/ortolan/)** — works offline, no dependencies.

Generate truly random 256-bit keys using dice (or coins) — no electronics, no software RNG, no trust required.

**Why physical randomness?** Digital random number generators have trust problems. The NSA [backdoored Dual_EC_DRBG](https://en.wikipedia.org/wiki/Dual_EC_DRBG) for seven years. [Debian's OpenSSL](https://www.debian.org/security/2008/dsa-1571) generated breakable keys for 20 months. Intel's [RDRAND is unauditable](https://en.wikipedia.org/wiki/RDRAND) silicon. Many devices — especially embedded systems, hardware wallets, and air-gapped machines — can't guarantee quality randomness at all.

The fix: trade randomness from mathematics on a deterministic system for something in the physical world. Dice under a blanket. You can *see* every roll. No firmware, no supply chain, no trust required.

**Why "Ortolan"?** The [ortolan bunting](https://en.wikipedia.org/wiki/Ortolan_bunting#Culinary_use) is a small bird traditionally eaten under a napkin. This tool recommends generating your password under a blanket for visual privacy. The bird is now protected by the EU — please don't eat them.

Copyright @tunnell 2026

## What is this?

A printable reference card that lets you generate a cryptographically strong password using physical randomness. Two methods are supported:

| Method | Actions | Password | Entropy | Alphabet |
|--------|---------|----------|---------|----------|
| **Dice** | 50 rolls of 2d6 | 50 characters | 258.5 bits | a–z, 0–9 (36 chars) |
| **Coin** | 256 flips | 52 characters | 256 bits | a–z, 0–5 (32 chars) |

Both methods use zero-waste encoding: dice map two d6 rolls to 36 characters (6 × 6 = 36), coins map 5 bits to 32 characters (2⁵ = 32).

## Why?

- **Verifiably random**: Dice rolls and coin flips are observable physical entropy sources. No CSPRNG, no `/dev/urandom`, no hardware RNG to trust.
- **Air-gapped**: The entire process happens on paper. No computer touches the key material until you type it in.
- **Auditable**: The procedure is simple enough to verify by hand. Anyone can check that the mapping is a bijection and that no entropy is lost.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The printable reference card with lookup tables, procedures, worksheets, and security notes. Open in any browser. |
| `entropy-test.html` | Entropy analyzer — test your dice or coins for fairness before generating a password. |
| `README.md` | This file. |
| `LICENSE` | License. |

## Usage

1. Open `index.html` in a browser (works fully offline — no JavaScript dependencies, no network requests).
2. Print it out, or use it on-screen.
3. Choose **Dice** or **Coin** tab.
4. Follow the procedure:
   - **Dice**: Roll two dice 50 times, look up each pair in Table D.
   - **Coin**: Flip 256 times, look up each 5-bit group in Table A (plus 1 final bit in Table B).
5. Insert a `.` every 5 characters for readability.
6. Enter the password (dots included) into your software.

## Security Considerations

The reference card includes detailed, research-backed security notes with full academic citations.

### Dice bias is negligible and unknowable
- **Campbell & Dolan (2019)**: Detecting whether a die is unfair requires ~3,000 rolls. Most commodity d6 dice tested fair.
- **Key insight**: An attacker doesn't know which dice you used or their specific bias. Each die's imperfections are unique and small.
- **No debiasing needed**: A ~1–2% bias per face, spread across 50 rolls, reduces entropy by a fraction of a bit.

### Coin bias is negligible
- **Bartoš et al. (2023/2025)**: 350,757 flips by 48 people using 46 different currencies — measured same-side bias of **50.8%**. Heads-vs-tails: 50.0% (no bias). Entropy cost: 0.047 bits over 256 flips.
- **Diaconis, Holmes & Montgomery (2007)**: Identified the precession mechanism causing same-side bias.
- **Von Neumann extractor**: Optional debiasing technique that produces perfectly unbiased output at ~4 flips per fair bit.

### Why dice (or coins), not digital RNGs
- **Physical objects can't be backdoored**: Dice from a board game or a coin from your pocket has no supply chain to intercept.
- **Digital RNGs have been catastrophically compromised**: Dual_EC_DRBG (NSA backdoor, 2006–2013), Debian OpenSSL (CVE-2008-0166, 20 months of ~15-bit entropy), Intel RDRAND (unauditable, CrossTalk vulnerability).
- **Physical randomness is observable and verifiable**: You can see every roll or flip. No firmware, no trust required.

### Critical technique notes
- **Dice**: Must bounce and tumble — don't drop flat or slide. Use a dice tray or box lid.
- **Coins**: Always FLIP, never SPIN. Spinning introduces large biases (~55% tails for US pennies).

### Physical security
- **Paper impressions**: ESDA recovers writing through up to 6 sheets. Write on isolated sheets; shred 7 pages if you used a notepad.
- **Electromagnetic emanations**: Keyboard EM radiation recoverable at 20m through walls (Vuagnoux & Pasini, 2009). Use interior rooms and auditable hardware.
- **Shoulder surfing**: 100% success rate in unprotected scenarios. Use a "bedsheet SCIF" for visual privacy during generation and entry.
- **Destruction**: Cross-cut shredding minimum (DIN P-4). For high security: wet pulping or burning to complete ash.

### Cryptographic strength
- **256-bit security**: Both methods exceed 256 bits of entropy, providing ~128-bit post-quantum security (Grover's algorithm).
- **KDF required**: Software must apply PBKDF2/Argon2/HKDF (standard in VeraCrypt, LUKS, KeePass).

### Prior art
Builds on Diceware (Reinhold, 1995), EFF wordlists (Bonneau, 2016), Glacier Protocol, ColdCard dice rolls, BlueWallet manual entropy, and Sia Foundation's coins-in-a-cup method (Vorick, 2020).

## Contributing

Issues and PRs welcome. This is a simple reference card — the main value is in correctness and clarity. If you spot an error in the mapping tables or security guidance, please open an issue.

## License

See [LICENSE](LICENSE).
