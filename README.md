# Tracking Number Detector

A tiny, dependency-free web tool that guesses the courier behind a tracking number the moment you paste it. Everything runs in the browser: no build step, no backend, no data leaves the page.

**Live:** deploy in one click on Vercel (see below), then track any parcel at [instantparcels.com](https://instantparcels.com).

## What it does

Paste a tracking number and the tool normalizes it, matches it against an ordered list of carrier formats, and where the format carries a verification digit it confirms the match by recomputing that digit. Results are labelled by confidence:

- **Confirmed**: the format has a check digit and it passes (UPS, USPS, and the UPU S10 postal family).
- **Likely**: a distinctive prefix or country-code suffix, but no check digit to verify.
- **Possible**: a plain numeric shape shared by several carriers; needs a real lookup to resolve.

It recognizes UPS, USPS, FedEx, DHL Express and eCommerce, Royal Mail, PostNL, DPD, Evri, Canada Post, and every national post that uses the international S10 standard (identified by the two-letter country suffix). The page also includes a written guide to how tracking-number formats work and how to build your own detector.

## Deploy on Vercel

This is a static site, so no configuration is needed.

1. Push this repo to your GitHub account.
2. In Vercel, choose **Add New Project** and import the repo.
3. Framework preset: **Other**. Leave build command empty and output directory as the root.
4. Deploy. Vercel serves `index.html` at your project URL.

You can also drag the folder onto Vercel or run `vercel` from the Vercel CLI.

## Files

- `index.html`: the entire app and content in one self-contained file.
- `vercel.json`: static config so Vercel serves `index.html` at the root.

## Tech notes

The detector is plain JavaScript. Detection is a normalize-then-match-then-verify pipeline: specific patterns (like the `1Z` UPS prefix) are tested before generic numeric ones so a twelve-digit number is not misclassified. The three check-digit algorithms (S10 modulo-11, USPS MOD 10, and the UPS 1Z scheme) are implemented inline and are tested against known-valid reference numbers.

## About

Built as a free utility for developers, online sellers, and support teams. For actual live tracking across 600+ carriers and postal operators, use [InstantParcels](https://instantparcels.com).

## License

MIT. Use it, fork it, embed it.
