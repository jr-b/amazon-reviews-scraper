# Amazon Reviews Scraper

Small Python script to extract / download reviews for any Amazon product as a CSV file.

Features:

- Support three countries/TLD: `.co.uk`, `.com` and `.ca`
- Retrieve up to 2100 reviews
- Deduplicate reviews
- Solve the Amazon Captcha ([https://www.amazon.com/errors/validateCaptcha](https://www.amazon.com/errors/validateCaptcha))
- Use Chrome as a headless browser

> Tested on macOS 13.6.2 using Python 3.10.12

## How to use

- Clone this repository on your computer
- Install required packages/modules with `pip install -r requirements.txt`
- Make sure you have Python 3.10+ available (`python -V`)
- From the root of this repo, run `python main.py --asin B08BRV6S41`

This script can run for a long time if your ASIN is available in all 3 countries. Go get a coffee ☕️

## Notes

As of 01/01/2024, the Amazon's frontend only allows to show 100 reviews (10 pages of 10 reviews).

To bypass this limit, we add filters to our requests (`four_star`, `two_star`, `critical`, etc.) so that we get access to more reviews.

We also fetch reviews from the three biggest countries (`['co.uk','ca','com']`).

Finally, when we have all the reviews, we delete the duplicates we might have got during the process.

The script is structured like this:

- For each countries... (3)
- For each filters... (7)
- For each pages... (up to 10)
- Get all reviews (up to 10)

I initially built this to reproduce the Ruby Amazon scraper that [Ryan Kulp built](https://github.com/ryanckulp/amz_reviews). I added some features along the way so that the Python version could fetch more reviews that the Ruby version.
