# (E)mail Client for Limited or Blocked Internet

[(E)mail Client for Limited or Blocked Internet](https://www.ergoforum.org/t/e-mail-client-for-limited-or-blocked-internet/134)

There are two motivations for this post.

1. Some countries, such as China and Belarus, are already blocking Tor. We can expect that some countries will try to block cryptocurrency protocols similarly in the future. 

2. [Internet just being restored in Iran after week-long shutdown](https://netblocks.org/reports/internet-restored-in-iran-after-protest-shutdown-dAmqddA9) caused by unrest. Previously there were partial or complete shutdowns in Egypt, Ethiopia, Sudan, and Turkey. 

However, people have the right to store value available, whether the value is under threat from monetary policies, political instability, or war. With digital communications and digital gold, we could solve this problem. 


As a possible solution for Bitcoin, [Blockstream satellite network](https://blockstream.com/satellite/) could be used; however, the satellite signal could be jammed. Another workaround that I propose is to use email (which is last to be blocked usually) or other low-bandwidth and not very interactive means of communication (fax, modem call over a landline to a bulletin board system, mail).

So assume Alice is willing to buy *X* ergs from Bob (paying with cash), but the Internet is limited or does not work in their area. Bob owns a box protected by a public key (stored locally). Then the protocol could be as follows.

1. Bob is creating a transaction from his box, which is creating a new box where *X* ergs are locked by the condition "Before deadline: Bob's signature and spending transaction have an output of *X* ergs which belongs to Alice's public key; After deadline: Bob's signature". I will refer to the new box as the "deal box" further. Please note that outputs with respective identifiers are known for a signed transaction.

2. Bob sends the transaction over (e)mail to a gateway. The gateway sends efficient [NiPoPoW](https://nipopows.com/) proof for a header having enough confirmations + proof of box membership against state digest from the header. This proof is small, tens of kilobytes. For better security, Bob may also ask another gateway for header proof. 

3. Bob shows the proof to Alice. Alice checks proofs and ensures that the deadline will not likely be met when a new transaction with their deal reaches the Ergo blockchain. Bob signs the new transaction: spending the deal box created in step 1 and creating the output box for Alice.

4. Now, Alice sends the transaction signed by Bob to the gateway and gets the proof of inclusion from it. 

With proofs of such size (tens of kilobytes), email/fax / ADSL modem or even paperwork is acceptable for communication between the users and the gateways.
