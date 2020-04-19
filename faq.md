# Octopus Watchdog Troubleshooting FAQ

_This page was last updated on 19/4/2020_

The purpose of this page is to help you resolve common issues you may experience.

## Why the Octopus dashboard is showing more data than the app is?

Octopus Energy Watchdog will only display full days. That is, days with 48 data points, one for each half hour of the day. It also keeps into account when we change the clock, so days with 46 and 50 data points are allowed.
Unfortunately sometimes when there are glitches in the Octopus backend, some days may have 47 data points, or less. The app will NOT display them until they are complete sets. This helps you quickly spot missing data, and to raise it with Octopus.

This also means that if the API sends several lines of consumption for today (usually the early hours of the day), you will see them in the dashboard, but the app won't display them until tomorrow, when the full 48 datapoints will have been released. This is done in the interest of keeping data tidy and comparable, rather than publishing incomplete days.

## Why can't I get gas costs?

The Octopus Energy API doesn't provide a way to correlate a user with its own meters, the products and local tariffs used by said meter. For electricity it's fairly easy to find out by scraping the dev page, but for gas it isn't. You won't find the correct product names as displayed in the API on the bill, or anywhere. Because of how obscure and difficult these details are to obtain, the feature was left out, as it would raise more questions than answers.

## My consumption is delayed by more than 24 hours

Sometimes this happens to certain accounts. Unfortunately the app is only showing what the API is sending. The only caveat is that the app waits until there are 48 datapoints for a single day before displaying it (i.e. 48 half-hourly segments to make up 24 hours). Your issue is either with the meter getting stuck and not sending out data, or with Octopus Energy getting stuck and not updating the API. The only solution is to open a ticket with them, as they can look into it and fix it for you.

## When I login, the gas section is empty, or an error is returned

Log out and use the 'manual login' process. This means that the app wasn't able to correctly scrape your gas meter details from the dev page.

## I have more than one meter, what can I do?

Use the manual login process and enter manually the details of the meter(s) you want to see within the app.

## I am on the GO/Fixed/Any other tariff that isn't Agile

The app won't be very useful in this instance unfortunately.

## When will you show export tariffs?

This feature is on the roadmap, at some point in future.

## What do you do with my credentials?

Your credentials are not stored anywhere. Not even on your device. If you use the automatic login process, your phone will launch a headless browser, literally navigating to the Octopus account and dev page, and then scraping the required details (MPAN, Serial Number, Product, Tariff for electricity and gas). Once those details have been gathered, they get stored locally on your phone, while your username and password are discarded.

## Octopus stopped sending consumption data on day X, and now I have several missing days

To make the app fast, every time it starts it requests the API for all data between the last available datapoint and now. Sometimes, if Octopus gets stuck, they stop sending data (for example, on 10/1/2020). Then the issue gets fixed on 13/1/2020 and you start getting data again from that date. The missing days haven't been backfilled yet, but eventually they will come through.
When this happens, the app only looks forward and will never go back to request the missing days. The fix is easy though. Go to More -> Force Full Refresh. This will request the entire dataset for the past 60 days. Please use sparingly as it performs a lot of requests to the Octopus API.

## My gas consumption doesn't look right

It was recently brought to my attention that SMETS1 meters send consumption in kWh, while SMETS2 meters send it in cubic metres. The API just pushes numbers without specifying what you're getting. To provide some mitigation to this, if you know what are you getting back from the API, you can set a custom gas multiplier in the More section.
For example, if you're sure you have a SMETS2 meter and you're getting consumption in cubic meters, you can convert it to kWh by entering a multiplier in the settings. This value tends to hover between 11.18 and 11.22, depending on where you live, the type of gas and many other parameters.
You may be able to find this coefficient by tinkering with your meter interface, or by checking the Octopus bill.
