# ErgoTree Functions

> This page is a WIP. Please see [ErgoTree.pdf](https://storage.googleapis.com/ergo-cms-media/docs/ErgoTree.pdf) for full details.

$$
115 & \hyperref[sec:serialization:operation:ConstantPlaceholder]{\lst{ConstantPlaceholder}} & \parbox{4cm}{\lst{placeholder:} \\ \lst{(Int)} \\ \lst{  => T}} & Create special ErgoTree node which can be replaced by constant with given id. \\
\hline
        116 & \hyperref[sec:serialization:operation:SubstConstants]{\lst{SubstConstants}} & \parbox{4cm}{\lst{substConstants:} \\ \lst{(Coll[Byte], Coll[Int], Coll[T])} \\ \lst{  => Coll[Byte]}} & ... \\
\hline
        122 & \hyperref[sec:serialization:operation:LongToByteArray]{\lst{LongToByteArray}} & \parbox{4cm}{\lst{longToByteArray:} \\ \lst{(Long)} \\ \lst{  => Coll[Byte]}} & Converts \lst{Long} value to big-endian bytes representation. \\
\hline
        123 & \hyperref[sec:serialization:operation:ByteArrayToBigInt]{\lst{ByteArrayToBigInt}} & \parbox{4cm}{\lst{byteArrayToBigInt:} \\ \lst{(Coll[Byte])} \\ \lst{  => BigInt}} & Convert big-endian bytes representation (Coll[Byte]) to BigInt value. \\
\hline
        124 & \hyperref[sec:serialization:operation:ByteArrayToLong]{\lst{ByteArrayToLong}} & \parbox{4cm}{\lst{byteArrayToLong:} \\ \lst{(Coll[Byte])} \\ \lst{  => Long}} & Convert big-endian bytes representation (Coll[Byte]) to Long value. \\
\hline
        125 & \hyperref[sec:serialization:operation:Downcast]{\lst{Downcast}} & \parbox{4cm}{\lst{downcast:} \\ \lst{(T)} \\ \lst{  => R}} & Cast this numeric value to a smaller type (e.g. Long to Int). Throws exception if overflow. \\
\hline
        126 & \hyperref[sec:serialization:operation:Upcast]{\lst{Upcast}} & \parbox{4cm}{\lst{upcast:} \\ \lst{(T)} \\ \lst{  => R}} & Cast this numeric value to a bigger type (e.g. Int to Long) \\
\hline
        140 & \hyperref[sec:serialization:operation:SelectField]{\lst{SelectField}} & \parbox{4cm}{\lst{selectField:} \\ \lst{(T, Byte)} \\ \lst{  => R}} & Select tuple field by its 1-based index. E.g. \lst{input._1} is transformed to \lst{SelectField(input, 1)} \\
\hline
        143 & \hyperref[sec:serialization:operation:LT]{\lst{LT}} & \parbox{4cm}{\lst{<:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Returns \lst{true} is the left operand is less then the right operand, \lst{false} otherwise. \\
\hline
        144 & \hyperref[sec:serialization:operation:LE]{\lst{LE}} & \parbox{4cm}{\lst{<=:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Returns \lst{true} is the left operand is less then or equal to the right operand, \lst{false} otherwise. \\
\hline
        145 & \hyperref[sec:serialization:operation:GT]{\lst{GT}} & \parbox{4cm}{\lst{>:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Returns \lst{true} is the left operand is greater then the right operand, \lst{false} otherwise. \\
\hline
        146 & \hyperref[sec:serialization:operation:GE]{\lst{GE}} & \parbox{4cm}{\lst{>=:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Returns \lst{true} is the left operand is greater then or equal to the right operand, \lst{false} otherwise. \\
\hline
        147 & \hyperref[sec:serialization:operation:EQ]{\lst{EQ}} & \parbox{4cm}{\lst{==:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Compare equality of \lst{left} and \lst{right} arguments \\
\hline
        148 & \hyperref[sec:serialization:operation:NEQ]{\lst{NEQ}} & \parbox{4cm}{\lst{!=:} \\ \lst{(T, T)} \\ \lst{  => Boolean}} & Compare inequality of \lst{left} and \lst{right} arguments \\
\hline
        149 & \hyperref[sec:serialization:operation:If]{\lst{If}} & \parbox{4cm}{\lst{if:} \\ \lst{(Boolean, T, T)} \\ \lst{  => T}} & Compute condition, if true then compute trueBranch else compute falseBranch \\
\hline
        150 & \hyperref[sec:serialization:operation:AND]{\lst{AND}} & \parbox{4cm}{\lst{allOf:} \\ \lst{(Coll[Boolean])} \\ \lst{  => Boolean}} & Returns true if \emph{all} the elements in collection are \lst{true}. \\
\hline
        151 & \hyperref[sec:serialization:operation:OR]{\lst{OR}} & \parbox{4cm}{\lst{anyOf:} \\ \lst{(Coll[Boolean])} \\ \lst{  => Boolean}} & Returns true if \emph{any} the elements in collection are \lst{true}. \\
\hline
        152 & \hyperref[sec:serialization:operation:AtLeast]{\lst{AtLeast}} & \parbox{4cm}{\lst{atLeast:} \\ \lst{(Int, Coll[SigmaProp])} \\ \lst{  => SigmaProp}} & ... \\
\hline
        153 & \hyperref[sec:serialization:operation:Minus]{\lst{Minus}} & \parbox{4cm}{\lst{-:} \\ \lst{(T, T)} \\ \lst{  => T}} & Returns a result of subtracting second numeric operand from the first. \\
\hline
        154 & \hyperref[sec:serialization:operation:Plus]{\lst{Plus}} & \parbox{4cm}{\lst{+:} \\ \lst{(T, T)} \\ \lst{  => T}} & Returns a sum of two numeric operands \\
\hline
        155 & \hyperref[sec:serialization:operation:Xor]{\lst{Xor}} & \parbox{4cm}{\lst{binary_|:} \\ \lst{(Coll[Byte], Coll[Byte])} \\ \lst{  => Coll[Byte]}} & Byte-wise XOR of two collections of bytes \\
\hline
        156 & \hyperref[sec:serialization:operation:Multiply]{\lst{Multiply}} & \parbox{4cm}{\lst{*:} \\ \lst{(T, T)} \\ \lst{  => T}} & Returns a multiplication of two numeric operands \\
\hline
        157 & \hyperref[sec:serialization:operation:Division]{\lst{Division}} & \parbox{4cm}{\lst{/:} \\ \lst{(T, T)} \\ \lst{  => T}} & Integer division of the first operand by the second operand. \\
\hline
        158 & \hyperref[sec:serialization:operation:Modulo]{\lst{Modulo}} & \parbox{4cm}{\lst{\%:} \\ \lst{(T, T)} \\ \lst{  => T}} & Reminder from division of the first operand by the second operand. \\
\hline
        161 & \hyperref[sec:serialization:operation:Min]{\lst{Min}} & \parbox{4cm}{\lst{min:} \\ \lst{(T, T)} \\ \lst{  => T}} & Minimum value of two operands. \\
\hline
        162 & \hyperref[sec:serialization:operation:Max]{\lst{Max}} & \parbox{4cm}{\lst{max:} \\ \lst{(T, T)} \\ \lst{  => T}} & Maximum value of two operands. \\
\hline
        182 & \hyperref[sec:serialization:operation:CreateAvlTree]{\lst{CreateAvlTree}} & \parbox{4cm}{\lst{avlTree:} \\ \lst{(Byte, Coll[Byte], Int, Option[Int])} \\ \lst{  => AvlTree}} & Construct a new authenticated dictionary with given parameters and tree root digest. \\
\hline
        183 & \hyperref[sec:serialization:operation:TreeLookup]{\lst{TreeLookup}} & \parbox{4cm}{\lst{treeLookup:} \\ \lst{(AvlTree, Coll[Byte], Coll[Byte])} \\ \lst{  => Option[Coll[Byte]]}} &  \\
\hline
        203 & \hyperref[sec:serialization:operation:CalcBlake2b256]{\lst{CalcBlake2b256}} & \parbox{4cm}{\lst{blake2b256:} \\ \lst{(Coll[Byte])} \\ \lst{  => Coll[Byte]}} & Calculate Blake2b hash from \lst{input} bytes. \\
\hline
        204 & \hyperref[sec:serialization:operation:CalcSha256]{\lst{CalcSha256}} & \parbox{4cm}{\lst{sha256:} \\ \lst{(Coll[Byte])} \\ \lst{  => Coll[Byte]}} & Calculate Sha256 hash from \lst{input} bytes. \\
\hline
        205 & \hyperref[sec:serialization:operation:CreateProveDlog]{\lst{CreateProveDlog}} & \parbox{4cm}{\lst{proveDlog:} \\ \lst{(GroupElement)} \\ \lst{  => SigmaProp}} & ErgoTree operation to create a new \lst{SigmaProp} value representing public key
of discrete logarithm signature protocol.
        \\
\hline
        206 & \hyperref[sec:serialization:operation:CreateProveDHTuple]{\lst{CreateProveDHTuple}} & \parbox{4cm}{\lst{proveDHTuple:} \\ \lst{(GroupElement, GroupElement, GroupElement, GroupElement)} \\ \lst{  => SigmaProp}} &  ErgoTree operation to create a new SigmaProp value representing public key
of Diffie Hellman signature protocol.
Common input: (g,h,u,v)
        \\
\hline
        209 & \hyperref[sec:serialization:operation:BoolToSigmaProp]{\lst{BoolToSigmaProp}} & \parbox{4cm}{\lst{sigmaProp:} \\ \lst{(Boolean)} \\ \lst{  => SigmaProp}} & ... \\
\hline
        212 & \hyperref[sec:serialization:operation:DeserializeContext]{\lst{DeserializeContext}} & \parbox{4cm}{\lst{executeFromVar:} \\ \lst{(Byte)} \\ \lst{  => T}} & ... \\
\hline
        213 & \hyperref[sec:serialization:operation:DeserializeRegister]{\lst{DeserializeRegister}} & \parbox{4cm}{\lst{executeFromSelfReg:} \\ \lst{(Byte, Option[T])} \\ \lst{  => T}} & ... \\
\hline
        218 & \hyperref[sec:serialization:operation:Apply]{\lst{Apply}} & \parbox{4cm}{\lst{apply:} \\ \lst{((T) => R, T)} \\ \lst{  => R}} & Apply the function to the arguments.  \\
\hline
        227 & \hyperref[sec:serialization:operation:GetVar]{\lst{GetVar}} & \parbox{4cm}{\lst{getVar:} \\ \lst{(Byte)} \\ \lst{  => Option[T]}} & Get context variable with given \lst{varId} and type. \\
\hline
        234 & \hyperref[sec:serialization:operation:SigmaAnd]{\lst{SigmaAnd}} & \parbox{4cm}{\lst{allZK:} \\ \lst{(Coll[SigmaProp])} \\ \lst{  => SigmaProp}} & Returns sigma proposition which is proven when \emph{all} the elements in collection are proven. \\
\hline
        235 & \hyperref[sec:serialization:operation:SigmaOr]{\lst{SigmaOr}} & \parbox{4cm}{\lst{anyZK:} \\ \lst{(Coll[SigmaProp])} \\ \lst{  => SigmaProp}} & Returns sigma proposition which is proven when \emph{any} of the elements in collection is proven. \\
\hline
        236 & \hyperref[sec:serialization:operation:BinOr]{\lst{BinOr}} & \parbox{4cm}{\lst{||:} \\ \lst{(Boolean, Boolean)} \\ \lst{  => Boolean}} & Logical OR of two operands \\
\hline
        237 & \hyperref[sec:serialization:operation:BinAnd]{\lst{BinAnd}} & \parbox{4cm}{\lst{&&:} \\ \lst{(Boolean, Boolean)} \\ \lst{  => Boolean}} & Logical AND of two operands \\
\hline
        238 & \hyperref[sec:serialization:operation:DecodePoint]{\lst{DecodePoint}} & \parbox{4cm}{\lst{decodePoint:} \\ \lst{(Coll[Byte])} \\ \lst{  => GroupElement}} & Convert \lst{Coll[Byte]} to \lst{GroupElement} using \lst{GroupElementSerializer} \\
\hline
        239 & \hyperref[sec:serialization:operation:LogicalNot]{\lst{LogicalNot}} & \parbox{4cm}{\lst{unary_!:} \\ \lst{(Boolean)} \\ \lst{  => Boolean}} & Logical NOT operation. Returns \lst{true} if input is \lst{false} and \lst{false} if input is \lst{true}. \\
\hline
        240 & \hyperref[sec:serialization:operation:Negation]{\lst{Negation}} & \parbox{4cm}{\lst{unary_-:} \\ \lst{(T)} \\ \lst{  => T}} & Negates numeric value \lst{x} by returning \lst{-x}. \\
\hline
        241 & \hyperref[sec:serialization:operation:BitInversion]{\lst{BitInversion}} & \parbox{4cm}{\lst{unary_~:} \\ \lst{(T)} \\ \lst{  => T}} & Invert every bit of the numeric value. \\
\hline
        242 & \hyperref[sec:serialization:operation:BitOr]{\lst{BitOr}} & \parbox{4cm}{\lst{bit_|:} \\ \lst{(T, T)} \\ \lst{  => T}} & Bitwise OR of two numeric operands. \\
\hline
        243 & \hyperref[sec:serialization:operation:BitAnd]{\lst{BitAnd}} & \parbox{4cm}{\lst{bit_&:} \\ \lst{(T, T)} \\ \lst{  => T}} & Bitwise AND of two numeric operands. \\
\hline
        244 & \hyperref[sec:serialization:operation:BinXor]{\lst{BinXor}} & \parbox{4cm}{\lst{^:} \\ \lst{(Boolean, Boolean)} \\ \lst{  => Boolean}} & Logical XOR of two operands \\
\hline
        245 & \hyperref[sec:serialization:operation:BitXor]{\lst{BitXor}} & \parbox{4cm}{\lst{bit_^:} \\ \lst{(T, T)} \\ \lst{  => T}} & Bitwise XOR of two numeric operands. \\
\hline
        246 & \hyperref[sec:serialization:operation:BitShiftRight]{\lst{BitShiftRight}} & \parbox{4cm}{\lst{bit_>>:} \\ \lst{(T, T)} \\ \lst{  => T}} & Right shift of bits. \\
\hline
        247 & \hyperref[sec:serialization:operation:BitShiftLeft]{\lst{BitShiftLeft}} & \parbox{4cm}{\lst{bit_<<:} \\ \lst{(T, T)} \\ \lst{  => T}} & Left shift of bits. \\
\hline
        248 & \hyperref[sec:serialization:operation:BitShiftRightZeroed]{\lst{BitShiftRightZeroed}} & \parbox{4cm}{\lst{bit_>>>:} \\ \lst{(T, T)} \\ \lst{  => T}} & Right shift of bits. \\
\hline
        255 & \hyperref[sec:serialization:operation:XorOf]{\lst{XorOf}} & \parbox{4cm}{\lst{xorOf:} \\ \lst{(Coll[Boolean])} \\ \lst{  => Boolean}} & Similar to \lst{allOf}, but performing logical XOR operation between all conditions instead of \lst{&&} \\
\hline
$$