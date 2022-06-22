# HyteraDMRUSB
Reverse Engineering the Hytera DMR USB packet structure.

When 'Forward to PC' is enabled on a Hytera DMR radio, a RNDIS network is created over USB and packets are forwarded to the PC.

This github project attempts to document this packet structure.

Long term plan is to be able to encode and decode these packets for use in other projects (eg DMR sms gateway or GPS logger).

Note, this isn't RDAC, IPSC protocol for repeaters, just a plain mobile.

# Help!
Please, I'm stuck right now and have been stuck in the same place for a year. Anyone familier with DMR packets could get me over this initial hurdle and get this documentation moving on.

Current Status :
---------------

With @smarek's help we have confirmed it is Hytera's Dmr Application Protocol and his OK-DMR library successfully decodes it.
The protocol definition is in @smareks's https://github.com/OK-DMR/dmr-kaitai/blob/master/okdmr/kaitai/hytera/hytera_dmr_application_protocol.ksy
Data is transmitted as Hex.
For visual inspection, convert hex to binary and split into 8 bit rows as per the examples.

These appear to be standard ETSI packets and simply looking at them we can easily spot some data however there appear to be some fundermental differences.

# Data Found :
1) The first byte in hex describes the packet :
message_header_types:
    0x02: radio_control_protocol
    0x08: location_protocol
    0x09: text_message_protocol
    0x11: radio_registration
    0x12: telemetry_protocol
    0x13: data_transmit_protocol
    0x14: data_delivery_states
2) All packets end with 0x03
3) Logical Link ID's (LLID - The to and from radio network IP addresses).
4) Standard Text can easily be spotted and decoded.

# Issues :

2) Packet structure doesn't appear to match any of the 12 byte ETSI structures.

Thoughts
--------

I would assume that the first byte describes the ETSI type of packet, from that we should be able to calculate CRC and data rate type (3/4?) to remove extra bits and leave us with a standard ETSI packet. Going on from that should be fairly simple.

# Examples
In the examples folder are some sms comparison examples with my current thoughts embeded.
