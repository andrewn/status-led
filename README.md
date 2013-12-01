Status LED
===

** This is a first attempt, accepted statuses are hard-coded into the server. **

Uses an RGB LED to indicate status. A set of status names are mapped to various transitions.

Usage
---

The LED itself is managed via a single long-running process. You should specify a path to a socket, the file should not exist.

    $ status-led-server /run/status-led.sock
    Ready to accept

"Ready to accept" indicates that the server has connected to a UNIX socket and is ready to receive messages.

To change the LED status, use the `status-led` command, specifying the same socket path:

    $ status-led /rub/status-led.sock app-running
    State changed to <app-running>

The LED should then change to reflect this state.

States
---

A set number of states is configured. Passing in an unrecognised state will return the a state unknown message.

Upstart
---

A set of `upstart` configs in `upstart/`manage the transitions between different statuses. For example, `status-led/app-running` will trigger the `app` status  when the networking service is up and the radiodan-example_master app starts.

The `status-led/server` itself will be started as early as possible in the boot sequence.
