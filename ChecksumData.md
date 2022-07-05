Checksum data

Single Byte 8 bits

Sorce of information :
https://github.com/OK-DMR/ok-dmrlib/blob/master/okdmr/dmrlib/hytera/pdu/hdap.py#L46

    def get_hdap_checksum(checked_data: bytes) -> bytes:
        """
        Get 1-byte checksum for opcode through payload fields
        """

        csum: int = 0
        for byteval in checked_data:
            csum = (csum + byteval) & 0xFF

        return bytes([((csum ^ 0xFF) + 0x33) & 0xFF])


Lets break this up

# not sure what this does yet surely it doesn't set it to integer.
        csum: int = 0

# loop through the data add it and then bitwise & with 0xFFs
        for byteval in checked_data:
            csum = (csum + byteval) & 0xFF
            
# Take the total XOR with OxFF, add 0x33 and lastly & with OxFF
        return bytes([((csum ^ 0xFF) + 0x33) & 0xFF])
