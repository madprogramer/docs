# Troubleshooting
## Why is the bridge bot not accepting invites?

If the bridge starts up successfully, but inviting the bot doesn't work and the
logs don't show any errors, it usually means the homeserver isn't sending
events to the appservice. There are a few potential reasons this can happen:

* There was a misconfiguration in the appservice address/hostname/port config
  or the homeserver can't reach the appservice for some other reason. The
  homeserver logs should contain errors in this case (grep for `transactions` in
  Synapse's `homeserver.log`).
* The bridge was down for longer than a few minutes and the homeserver backed
  off. The homeserver should retry after some time. If it still doesn't work
  after an hour or so (exact backoff depends on how long the bridge was down),
  check the homeserver logs.
* Synapse messed up and silently broke the appservice. This is quite rare, but
  you should check [matrix-org/synapse#1834](https://github.com/matrix-org/synapse/issues/1834)
  if nothing else works.