### URLScheme

URLScheme can be used to control Hodor through other apps or create shortcuts.

#### Open Packet Capture

Example:

```hodor://open?record=true&rewrite=true```

| Parameter | Optional Value | Description |
| --- | --- | --- |
| record | true or false | Enables or disables the packet capture function |
| recordrule | name of capture rule | Switches to the corresponding capture rule based on its name |
| rewrite | true or false | Enables or disables the rewriting function |
| rewriterule | name of rewrite rule | Switches to the corresponding rewrite rule based on its name |
| proxy | host:port | Switches to the corresponding proxy server based on its address and port |
| advance | true or false | Enables or disables advanced functionality |
| lan | true or false | Enables or disables local network packet capture functionality |

#### Close Packet Capture

```hodor://shutdown``` 



***Finally, Due to the various combinations of transmission control in the HTTP protocol, the author may have overlooked some aspects during testing. If you find that a certain function is not working according to the documentation or does not meet your expectations, please contact us via email at `hodorsoft@outlook.com`. Writing this software was not easy, and if you find it useful, we hope you can leave a positive review on the AppStore. Your support is our greatest motivation for future updates.***
