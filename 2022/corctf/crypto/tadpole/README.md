# tadpole

tadpoles only know the alphabet up to b... how will they ever know what p is?

[tadpole.py](tadpole.py) [output.txt](output.txt)

# solution

if we review [tadpole.py](tadpole.py) we can see that:

```python
p = bytes_to_long(open("flag.txt", "rb").read())
assert isPrime(p)

a = randbelow(p)
b = randbelow(p)

def f(s):
    return (a * s + b) % p

print("a = ", a)
print("b = ", b)
print("f(31337) = ", f(31337))
print("f(f(31337)) = ", f(f(31337)))
```

the flag was converted into a long number prime number - variable `p`. <br>
after that, `a` and `b` were generated randomly to numbers that is less than `p`. <br>
the function `f` is defined as follows: <br>
1. take `s` - a number
2. calculate `a` times `s`, add `b` and calculate this result modulo `p`. <br>

the script print `a` and `b` and the result of running the function `f` with two numbers as `s`,
those numbers are `31337` and the result of `f(31337)` which is known because it is given
in [output.txt](output.txt):

```python
a =  7904681699700731398014734140051852539595806699214201704996640156917030632322659247608208994194840235514587046537148300460058962186080655943804500265088604049870276334033409850015651340974377752209566343260236095126079946537115705967909011471361527517536608234561184232228641232031445095605905800675590040729
b =  16276123569406561065481657801212560821090379741833362117064628294630146690975007397274564762071994252430611109538448562330994891595998956302505598671868738461167036849263008183930906881997588494441620076078667417828837239330797541019054284027314592321358909551790371565447129285494856611848340083448507929914
f(31337) =  52926479498929750044944450970022719277159248911867759992013481774911823190312079157541825423250020665153531167070545276398175787563829542933394906173782217836783565154742242903537987641141610732290449825336292689379131350316072955262065808081711030055841841406454441280215520187695501682433223390854051207100
f(f(31337)) =  65547980822717919074991147621216627925232640728803041128894527143789172030203362875900831296779973655308791371486165705460914922484808659375299900737148358509883361622225046840011907835671004704947767016613458301891561318029714351016012481309583866288472491239769813776978841785764693181622804797533665463949
```

now, we want to get the flag, so I will be using the opposite function of `bytes_to_long`
which is `long_to_bytes`, but to get the flag I need to find `p`.

basically I can calculate `f(s)` for the same number but without performing the modulo operation because I don't know `p`.

I will declare this function as `new_f`:

```python
def new_f(s):
    return a * s + b
```

so i calculate the next values:

```python
a = 7904681699700731398014734140051852539595806699214201704996640156917030632322659247608208994194840235514587046537148300460058962186080655943804500265088604049870276334033409850015651340974377752209566343260236095126079946537115705967909011471361527517536608234561184232228641232031445095605905800675590040729
b = 16276123569406561065481657801212560821090379741833362117064628294630146690975007397274564762071994252430611109538448562330994891595998956302505598671868738461167036849263008183930906881997588494441620076078667417828837239330797541019054284027314592321358909551790371565447129285494856611848340083448507929914
f_result_with_31337 = 52926479498929750044944450970022719277159248911867759992013481774911823190312079157541825423250020665153531167070545276398175787563829542933394906173782217836783565154742242903537987641141610732290449825336292689379131350316072955262065808081711030055841841406454441280215520187695501682433223390854051207100
f_result_with_f_result_with_31337 = 65547980822717919074991147621216627925232640728803041128894527143789172030203362875900831296779973655308791371486165705460914922484808659375299900737148358509883361622225046840011907835671004704947767016613458301891561318029714351016012481309583866288472491239769813776978841785764693181622804797533665463949
new_f_result_with_31337 = new_f(31337)
new_f_result_with_f_result_with_31337 = new_f(f_result_with_31337)
```

I know that `new_f_result_with_31337 = f_result_with_31337 + p*n1` when I don't know what is `n1`,
and I also know that `new_f_result_with_f_result_with_31337 = f_result_with_f_result_with_31337 + p*n2` 
when I also don't know what is `n2`, but I can calculate the difference:

```python
difference_1 = new_f_result_with_31337 - f_result_with_31337
difference_2 = new_f_result_with_f_result_with_31337 - f_result_with_f_result_with_31337
```

and the next thing I know is that `difference_1 = p*n1`, `difference_2 = p*n2`. <br>
so `difference_1+difference_2 = p*(n1+n2)` and this sum can be factorized using prime numbers, <br>
and I know that one of the factors is going to be `p`, to solve it I just use the function `gcd`
that calculates for me the greatest common divisor to get `p` will be the greatest common divisor.

```python
p = math.gcd(difference_1, difference_2)
print(long_to_bytes(p))
```

which outputs: <br>
`b'corctf{1n_m4th3m4t1c5,_th3_3ucl1d14n_4lg0r1thm_1s_4n_3ff1c13nt_m3th0d_f0r_c0mput1ng_th3_GCD_0f_tw0_1nt3g3rs} <- this is flag adm'`

the flag was:

`corctf{1n_m4th3m4t1c5,_th3_3ucl1d14n_4lg0r1thm_1s_4n_3ff1c13nt_m3th0d_f0r_c0mput1ng_th3_GCD_0f_tw0_1nt3g3rs}`