# ROBOTS AND MUSIC

Do you like old music?

`http://01.linux.challenges.ctf.thefewchosen.com:49491`

# SOLUTION

this site source code is:

`<title>Robots</title><pre>I hope you like robots!</pre>`

maybe based on the challenge name we should check the `robots.txt` file.
that file discovers us that there is a file at `/g00d_old_mus1c.php`, lets navigate there:

![g00d_old_mus1c output](g00d_old_mus1c_output.png)

and just like this, we got the flag:

`TFCCTF{Kr4ftw3rk_4nd_th3_r0b0ts}`
