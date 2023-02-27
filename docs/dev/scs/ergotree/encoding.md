# ErgoTree Encoding

## VLQ encoding

```scala
public final void putULong(long value) {
    while (true) {
        if ((value & ~0x7FL) == 0) {
            buffer[position++] = (byte) value;
            return;
        } else {
            buffer[position++] = (byte) (((int) value & 0x7F) | 0x80);
            value >>>= 7;
        }
    }
}
```

## ZigZag encoding

Encode a ZigZag-encoded 64-bit value. ZigZag encodes signed integers into values that can be efficiently encoded with **varint**. (Otherwise, negative values must be sign-extended to 64 bits to be **varint** encoded, thus always taking 10 bytes in the buffer.

Parameter **n** is a signed 64-bit integer. This Java method returns an unsigned 64-bit integer stored in a signed int because Java has no explicit unsigned support.

```scala
public static long encodeZigZag64(final long n) {
    // Note: the right-shift must be arithmetic
    return (n << 1) ^ (n >> 63);
}
```


