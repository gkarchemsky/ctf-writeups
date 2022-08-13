# BASIC

This guy keeps insulting my girlfriend!
His last message confused me, though!
Can you help me decode it?

`/Rn/X7n#bUc.rjzh,|eEsg,?&QI;@^ARm}UKOkICi#X.ixEmN]D`

# SOLUTION

we got a string that looks like it was encodes somehow,
I used [this](https://www.dcode.fr/cipher-identifier) cipher identifier site
to understand that this message was encoded using `Base91`.

so I decoded it using [this](https://www.dcode.fr/base-91-encoding) site and got the flag.

`TFCCTF{sh3's_4_10..._but_0n_th3_ph_sc4l3}`
