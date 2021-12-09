# Default Connections

Hexavalent makes various connections to check for internet connectivity,
download component updates, and more. They aren't "spyware" connections like
people would have you believe; they're often essential connections or can be
easily disabled.

## Component Updates

Hexavalent will make connections to download component updates for the browser.

*   https://update.googleapis.com/service/update2/json
*   http://update.googleapis.com/service/update2/json

## Autocomplete

Typing into the omnibox returns search suggestions.

*   https://www.google.com/complete/search

## Promo Service

Hexavalent will automatically download promotions if the default search engine
is Google. It's not really a concern due to the ability to easily switch the
default search engine.

*   https://www.google.com/async/newtab_promos

## Safe Browsing

// destination: GOOGLE_OWNED_SERVICE
