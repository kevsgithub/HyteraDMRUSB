# HyteraDMRUSB
Reverse Engineering the Hytera DMR USB packet structure.

When 'Forward to PC' is enabled on a Hytera DMR radio a RNDIS network is created over USB and packets are forwarded to the PC.

This github project attempts to document this packet structure.

Current Status :
---------------

These appear to be standard ETSI packets and simply looking at them we can easily spot some data however there appear to be some fundermental differences.

# Data Found :
1) Logical Link ID's (LLID - The to and from radio network IP addresses).
2) Standard Text can easily be spotted and decoded.

# Issues :
1) The addresses (LLID) appear to be 28 or 32 bits (Full ip address) not the 24 bits listed in ETSI documents.
2) Packet structure doesn't appear to match any of the 12 byte ETSI structures.
