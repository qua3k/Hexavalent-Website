# Miscellaneous

These topics may get their own page later on.

## Automatic Variable Initialization

Using an uninitialized variable results in undefined behavior. This
[compiler option](https://lists.llvm.org/pipermail/cfe-dev/2020-April/065221.html)
automatically initializes variables with either zero or a pattern to reduce the
impact of those issues. It's something the Chromium authors have already enabled
by default but we're going to be using zero var init instead of the pattern as
we're focused on mitigating bugs, not finding them. It's also a lot faster than
pattern var init and should cause fewer problems overall.

## Battery Status API

The Battery Status API allows sites to determine the user agent's battery level,
charging status, time until fully charged, and time until fully discharged. We
stub it out to always return 100% and charging.

## Do Not Track

Do Not Track is a HTTP request header designed to advertise the user agent's
tracking preference. It has dubious benefit as it doesn't actually do anything
to prevent tracking on a technical level – there isn't any legislation requiring
sites to respect it.

## HTTPS-Only Mode

The HTTPS-only mode really won't break many sites at all – the interstitial is
easily understood and it exposes an option for users to visit legacy sites.

## JIT Compilation

The JIT engine has been a source of numerous vulnerabilities, with it
accounting for roughly half of V8 exploits. The introduction of RWX pages
prevents mitigations such as ACG from being enabled in the renderer process. We
expose a flag to easily toggle JIT compilation and are looking into lifting
Vanadium's site setting patch.

## Origin Isolation

Historically, Chrome has limited the access each renderer process has to
documents from the same scheme and eTLD+1 (site isolation) due to origin
isolation being considered prohibitively expensive and incompatibility with
sites using `document.domain` to allow cross-origin DOM access. It's still an
issue for sites not sufficiently cross-origin isolated with COEP/COOP,
rendering them vulnerable to cross-origin speculative execution side channels
due to origins sharing address space. Strict Origin Isolation brings the process
boundary in line with the same-origin policy and is likely going to be enabled
by default upstream due to `document.domain` usage dropping significantly.

## Signed Integer Overflow

Signed integer overflow is undefined behavior. Hexavalent is temporarily using
`-fwrapv` to prevent issues stemming from reliance on undefined behavior as the
performance impact of
`-fsanitize=shift,signed-integer-overflow -fsanitize-trap=shift,signed-integer-overflow`
is deemed to be currently unacceptable.

## WebRTC IP Handling

WebRTC enables users to communicate peer-to-peer in real time, and it does so by
using the Interactive Connectivity Establishment (ICE) protocol. In turn, ICE
uses techniques such as STUN and TURN to enumerate interfaces and determine the
best route, leading the server to learn more about the local network
configuration than a typical HTTP request, such as the client's `RFC1918`
addresses.

However, the largest concern stems from the fact that the default configuration
reveals clients' ISP public address even when they are behind a proxy. We expose
a toggle to change the IP handling mode and set the default to
"Default Route Only".
