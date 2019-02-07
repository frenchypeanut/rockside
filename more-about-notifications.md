# Tell me more about mail notifications


### What are notifications?

Notification are a means to let the user know that an unusual event happened in Rockside. It takes the form of an email with the relevant information that is sent to an address specified by the user.

To be able of activating notifications you need to setup an SMTP server on rockside. See [Advanced configuration (SMTP, Certificates, Data dir...)](installation/advanced-setup.md)

### Which services are using notifications?

For this release,  notifications use to monitor slaves and nodes managed by Rockside.

### What will trigger a notification?

A notification is sent to the user when a slave could not be contacted by the api for more than a minute. Regarding nodes, a notification will be sent if the node stops running or if a gap of more than 3 blocks between the current and the highest block occurs.

### How do I activate/deactivate notifications for a slave?

From the list of slaves, turn on the switch button by clicking on it to activate notification for the corresponding slave. To deactivate notifications, turn off the switch button by clicking on it once more

### How do I activate/deactivate notifications for a node?

From the list of nodes, turn on the switch button by clicking on it to activate notification for the corresponding node. To deactivate notifications, turn off the switch button by clicking on it once more.

### Where can I choose the email address will receive the notifications?

At the top right of the screen, click on your profile name to display a dropdown menu. From there click on Notification to display the notification center page. You can then enter the email you wish to use for receiving notifications.

### Are notifications for slaves and nodes sent to the same email address?

Yes, for the current release.
