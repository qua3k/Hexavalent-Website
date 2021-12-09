# WebUI Hardening

Most of the WebUI is extremely privileged with unprompted access to the
camera/microphone. The existing WebUI is really insecure and doesn't really
feature any meaningful defenses; the Content-Security-Policy is terribly lax and
doesn't provide any significant security.

It's something we're aware of but aren't going to be actively pursuing rewriting
it with a sane CSP with Trusted Types as that work is already being done by
Microsoft and any effort we expend on the issue would be wasted time.
