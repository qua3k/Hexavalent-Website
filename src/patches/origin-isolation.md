# Origin Isolation

Historically, Chrome has limited the access each renderer process has to
documents from the same scheme and eTLD+1
([Site Isolation](https://www.chromium.org/Home/chromium-security/site-isolation)),
instead of origins because:

1.  It would maintain compatibility with sites that use `document.domain` to
    allow cross-origin DOM access.
1.  Isolating by origin was considered prohibitively expensive.

However, this meant that sites hosting user content on a subdomain and sensitive
data on another were still very vulnerable to speculative execution side
channels.

Strict origin isolation brings the process boundary in line with the Same-Origin
Policy, and
[upstream is attempting to enable origin isolation](https://crbug.com/1259920)
after deprecating `document.domain`.

## See also

*   [https://www.spookjs.com/](https://www.spookjs.com/)

Credits: the Hexavalent team
