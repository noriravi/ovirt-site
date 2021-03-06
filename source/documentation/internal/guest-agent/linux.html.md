---
title: Linux
category: ovirt-guest-agent
authors: vfeenstr
wiki_category: Ovirt_guest_agent
wiki_title: OVirt Guest Agent/Single Sign On/Linux
wiki_revision_count: 5
wiki_last_updated: 2012-12-11
---

<!-- TODO: Content review -->

# Linux

## An overview how the single sign on process works on GNU/Linux systems

![](Ovirt-guest-agent-sso-linux2.png "Ovirt-guest-agent-sso-linux2.png")

1.  VDSM sends a 'login' message to the oVirt Guest Agent
2.  The oVirt Guest Agent daemon/service receives the message and creates a 6 character long random token
3.  The Guest Agent creates a UNIX Domain Socket on '\\x00/tmp/ovirt-cred-channel' and listens to it for 5 seconds to receive
4.  The Guest Agent triggers the Credentials UserAuthenticated signal which the GDM/KDM plug-ins are subscribing to
5.  Once triggered, the KDM/GDM plugin initiates a new login by using the gdm-ovirtcred pam stack
6.  The pam module requests the Token from the GDM module
7.  The pam module sends the Token to the ovirt-cred-channel UNIX Domain socket
8.  The pam module receives the username/password combination and reaches the login information down the pam stack
9.  If the login credentials are valid, the user is authenticated and the Desktop session started

<Category:Ovirt_guest_agent>
