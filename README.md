# Ortolan

A printable reference card for generating a 256-bit password from dice rolls or coin flips. No electronics, no software RNG, no trust required.

**[Use it here](https://tunnell.github.io/ortolan/)**, or print it. The page works offline: check the source, disconnect, then generate your password.

| Method | Actions | Password | Entropy | Alphabet |
|--------|---------|----------|---------|----------|
| Dice | 50 rolls of 2d6 | 50 characters | 258.5 bits | a–z, 0–9 (36 chars) |
| Coin | 256 flips | 52 characters | 256 bits | Crockford Base32 (32 chars) |

Both encodings are zero-waste bijections: each roll of two dice maps onto one of 36 characters (6 × 6), each group of five coin flips onto one of 32 (2⁵). The coin alphabet is Crockford's Base32, which drops i, l, o, and u so a handwritten key can't be misread. Everything happens on paper, and the mapping is simple enough to check by hand. No computer touches the key until you type it in.

## Usage

1. Open the card in a browser, or print it.
2. Pick the Dice or Coin tab.
3. Dice: roll two dice 50 times and look up each pair in Table D. Coin: flip a coin 256 times and look up each group of 5 flips in Table A, plus one final bit in Table B.
4. Insert a `.` every 5 characters for readability. Keeping the dots in the final password is a good default; they carry no entropy, so dropping them is fine too, as long as you're consistent.
5. Type the password into your software.

Technique matters more than equipment: dice must bounce and tumble (use a tray or a box lid; don't slide them), and coins must be flipped and caught, never spun. Spinning a US penny lands tails about 55% of the time. If you suspect your dice or coins anyway, [entropy-test.html](https://tunnell.github.io/ortolan/entropy-test.html) tests them for fairness. Detecting an unfair die takes about 3,000 rolls, so a quick session is reassurance rather than proof.

## Security

Digital random number generators have trust problems. The NSA [backdoored Dual_EC_DRBG](https://en.wikipedia.org/wiki/Dual_EC_DRBG) for seven years, [Debian's OpenSSL](https://www.debian.org/security/2008/dsa-1571) generated breakable keys for 20 months (CVE-2008-0166), and Intel's [RDRAND](https://en.wikipedia.org/wiki/RDRAND) is unauditable silicon. Dice from a board game have no firmware and no supply chain to trust, and you can watch every roll.

The card itself carries the full research notes with linked sources (dice and coin bias measurements, paper-impression forensics, keyboard electromagnetic emanations, shoulder surfing, destruction standards), so they are not duplicated here. The short version is that commodity dice and coins are plenty fair for this job: the largest coin-flip study to date, at 350,757 flips, found a same-side bias of just 50.8%, which costs 0.047 bits of entropy over 256 flips. Read the card's notes before generating a password you actually intend to use.

Both methods give at least 256 bits of entropy (dice 258.5, coin exactly 256), which holds roughly 128-bit security against Grover's algorithm. Whatever consumes the password must apply a real KDF such as PBKDF2, Argon2, or HKDF; VeraCrypt, LUKS, and KeePass all do.

Prior art: [Diceware](https://theworld.com/~reinhold/diceware.html) (Reinhold, 1995), the [EFF wordlists](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases) (Bonneau, 2016), Glacier Protocol, ColdCard dice rolls, BlueWallet manual entropy, and the Sia Foundation's [coins-in-a-cup method](https://sia.tech/blog/generating-cryptographically-secure-random-numbers-with-coins-and-a-cup) (Vorick, 2020).

## The name

<img src="ortolan.jpg" align="right" width="200" alt="An ortolan bunting perched on a branch">

The [ortolan bunting](https://en.wikipedia.org/wiki/Ortolan_bunting#Culinary_use) is a small bird traditionally eaten under a napkin. This tool recommends generating your password under a blanket for visual privacy. The bird is now protected by the EU — please don't eat them.

## Contributing

Issues and PRs welcome. The card's whole value is correctness, so reports of errors in the mapping tables or the security guidance are especially appreciated.

## License

Copyright 2026 @tunnell, dedicated to the public domain under [CC0 1.0](LICENSE). The one exception is the bird photo, `ortolan.jpg`, which is by [Pierre Dalous](https://commons.wikimedia.org/w/index.php?curid=26699114) under CC BY-SA 3.0 and is not part of the dedication.
