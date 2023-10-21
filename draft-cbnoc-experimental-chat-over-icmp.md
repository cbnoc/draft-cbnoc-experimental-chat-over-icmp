---
title: "Chat over ICMP"
category: exp

docname: draft-cbnoc-experimental-chat-over-icmp-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "cbnoc/draft-cbnoc-experimental-chat-over-icmp"
  latest: "https://cbnoc.github.io/draft-cbnoc-experimental-chat-over-icmp/draft-cbnoc-experimental-chat-over-icmp.html"

author:
 -
    fullname: hikalium
    organization: CBNOC
    email: hikalium@hikalium.com

normative:

informative:


--- abstract

This document defines a Chat over ICMP protocol.


--- middle

# Introduction

Chat over ICMP protocol uses extra IP [@!RFC791] datagram bytes that are not used by ICMP [@!RFC792] to transport messages.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Specification

## Format

A structure of Chat over ICMP datagram is as follows :

```
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Type      |     Code      |          Checksum             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Topic ( first 4 bytes )                                   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Topic ( last  3 bytes )                   |  NUL (0x00)   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Message ...
+-+-+-+-+-
```

IP Fields (derived from ICMP):

Addresses

  The ip address of the source in a chat message will be the
  destination of the chat message.  If a sender wants to
  broadcast the message across the Topic space, the ip address
  of the destination should be a broadcast address.

IP Fields (derived from ICMP):

Type

  0 for a chat message. In ICMP, this value means an echo reply
  message.

Code

  0

Checksum

  The checksum is the 16-bit ones's complement of the one's
  complement sum of the ICMP message starting with the ICMP Type.
  For computing the checksum , the checksum field should be zero.
  If the total length is odd, the received data is padded with one
  octet of zeros for computing the checksum.  This checksum may be
  replaced in the future.

Addresses

  The address of the source in an echo message will be the
  destination of the echo reply message.  To form an echo reply
  message, the source and destination addresses are simply reversed,
  the type code changed to 0, and the checksum recomputed.

Topic

  The Identifier and Sequence Number fields defined by ICMP is
  repurposed to represent Topic of the chat. Topic act as an
  identifier of a chat room so the receiver can categorize messages
  based on the value.


# Security Considerations

Chat over ICMP protocol does not define any protection of message bytes. Therefore, it MUST NOT be used to carry sensitive data which should be securely transported. An implementation should consider that the data is not protected in any ways and it should give appropriate notice to its users about that risk.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
