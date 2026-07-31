# Ortolan

A printable reference card for generating a 256-bit password from dice rolls or coin flips. No electronics, no software RNG, no trust required until you type it in — and the card walks you through the typing part too. It's meant for secrets an attacker can grind offline — disk encryption, a password manager's master key, a wallet seed — not for website logins.

**[Use it here](https://tunnell.github.io/ortolan/)**, or print it. The page works offline: check the source, disconnect, then generate your password. Printed paper is the zero-trust path; the on-screen card trusts your browser and whoever served it. Before first use, check the printed tables: every cell distinct, grid complete.

| Method | Actions | Password | Entropy | Alphabet |
|--------|---------|----------|---------|----------|
| Words | 100 rolls (20 × 5d6) | 20 words (~150 chars) | 258.5 bits | EFF large wordlist (7,776 words) |
| Dice | 50 rolls of 2d6 | 50 characters | 258.5 bits | a–z, 0–9 (36 chars) |
| Coin | 256 flips | 52 characters | 256 bits | Crockford Base32 (32 chars) |

All three encodings are zero-waste bijections: five dice rolls map onto one of 7,776 words (6⁵), each roll of two dice onto one of 36 characters (6 × 6), each group of five coin flips onto one of 32 (2⁵). The coin alphabet is Crockford's Base32, which drops i, l, o, and u so a handwritten key can't be misread. Words is the default tab because passphrases survive handwriting and typing better than random characters do; the wordlist ships in the repo as `eff_large_wordlist.txt` and is embedded in the card itself, so the printed Words tab is self-contained. Everything happens on paper, and the mapping is simple enough to check by hand. No computer touches the key until you type it in — at which point the endpoint is exactly as trusted as it is for any password; the card's phase 4 covers what that means.

## The ceremony

Six phases, in order; the trust you carry in each is tabulated at the top of the card.

1. Prepare: every device with a microphone or radio out of the room, powered off — not muted. If you tested your dice for fairness, that was another day.
2. Generate: 20 five-roll words against the EFF wordlist, 50 rolls of two dice against Table D, or 256 coin flips against Tables A and B, under the blanket. Coins: shake between cupped hands so you never know the starting side, flip, catch — never spin. For character modes, insert a `.` every 5 characters for readability (the dots carry no entropy; keeping them is a good default).
3. Verify: a second, independent lookup pass into the worksheet's Check column, then read both record copies back character by character. Unchecked, roughly one transcription in three carries a silent error.
4. Enter: type the key blind into a masked field, never displayed on a screen. From here the machine is trusted exactly as it is for any password.
5. Prove: create the encrypted volume or wallet, close it, and reopen it by typing from the copy you intend to keep — only then destroy anything.
6. Keep and destroy: two verified copies in separate places (loss, not theft, is the dominant failure mode); shred the worksheets and the seven sheets beneath them.

Technique matters more than equipment: dice must bounce and tumble (use a tray or a box lid; don't slide them), and coins must be flipped and caught, never spun. Spinning a US penny lands tails about 55% of the time. If you suspect your dice or coins anyway, [entropy-test.html](https://tunnell.github.io/ortolan/entropy-test.html) tests them for fairness. Detecting an unfair die takes about 3,000 rolls, so a quick session is reassurance rather than proof.

## Security

Digital random number generators have trust problems. The NSA [backdoored Dual_EC_DRBG](https://en.wikipedia.org/wiki/Dual_EC_DRBG) for seven years, [Debian's OpenSSL](https://www.debian.org/security/2008/dsa-1571) generated breakable keys for 20 months (CVE-2008-0166), and Intel's [RDRAND](https://en.wikipedia.org/wiki/RDRAND) is unauditable silicon. More recently, [Milk Sad](https://milksad.info/) (CVE-2023-39910) collapsed 2²⁵⁶ wallet keyspaces to 2³² by seeding a Mersenne Twister with clock time — in a key-*generation* tool, which is the point: the entropy was never the weak link. Dice from a board game have no firmware and no supply chain to trust, and you can watch every roll.

The card itself carries the full research notes with linked sources (dice and coin bias measurements, paper-impression forensics, keyboard electromagnetic emanations, shoulder surfing, destruction standards), so they are not duplicated here. The short version is that commodity dice and coins are plenty fair for this job: the largest coin-flip study to date, at 350,757 flips, found a same-side bias of just 50.8%, which costs 0.047 bits of entropy over 256 flips. Read the card's notes before generating a password you actually intend to use.

The encodings are sized to 256 bits (dice 258.5, coin 256 with the starting side randomized); under the min-entropy accounting NIST SP 800-90B applies to key material, bias typical of commodity dice and coins still leaves ~250 bits (coin) and ~255.6 (dice), about 125-bit security even against Grover's algorithm. Whatever consumes the password must apply a real KDF such as PBKDF2, Argon2, or HKDF; VeraCrypt, LUKS, and KeePass all do. That software is itself a trusted component — KeePass's CVE-2023-32784 leaked typed master passwords out of process memory.

Prior art: [Diceware](https://theworld.com/~reinhold/diceware.html) (Reinhold, 1995), the [EFF wordlists](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases) (Bonneau, 2016), Glacier Protocol, ColdCard dice rolls, BlueWallet manual entropy, and the Sia Foundation's [coins-in-a-cup method](https://sia.tech/blog/generating-cryptographically-secure-random-numbers-with-coins-and-a-cup) (Vorick, 2020). Dice entry is now mainstream in hardware signers (SeedSigner, Keystone); Ortolan differs in that you can't under-roll a fixed-length worksheet, and the conversion happens on paper where you can check it.

## The name

<img src="ortolan.jpg" align="right" width="200" alt="An ortolan bunting perched on a branch">

The [ortolan bunting](https://en.wikipedia.org/wiki/Ortolan_bunting#Culinary_use) is a small bird traditionally eaten under a napkin. This tool recommends generating your password under a blanket for visual privacy. The bird is now protected by the EU — please don't eat them.

## Contributing

Issues and PRs welcome. The card's whole value is correctness, so reports of errors in the mapping tables or the security guidance are especially appreciated.

## License

Copyright 2026 @tunnell, dedicated to the public domain under [CC0 1.0](LICENSE). Two exceptions, neither part of the dedication: the bird photo `ortolan.jpg`, by [Pierre Dalous](https://commons.wikimedia.org/w/index.php?curid=26699114) under CC BY-SA 3.0, and the wordlist `eff_large_wordlist.txt`, © the Electronic Frontier Foundation ([Joseph Bonneau, 2016](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases)), redistributed unmodified under [CC BY 4.0](https://www.eff.org/copyright).
