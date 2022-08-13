# msfrog-generator

The vanilla msfrog is hard to beat, 
but this webapp allows you to make it even better!
[https://msfrog-generator.be.ax/](https://msfrog-generator.be.ax/)

# solution

this is the site:

![site](site.png)

you can add emojis to the frog and then click generate. <br>
You can find the next message in the html source code:

```html
<!-- NOTE: There is no (intended) vuln in the frontend, please don't waste your time digging into the JS ;)  -->
```

let's check the request that is sent by clicking the `Generate` button:

![regular request](regular_request.png)

maybe lets gey and place `flag.png` ?

![flag.png in json](flag_png_in_json.png)

now I get different response:

![flag.png response](flag_png_response.png)

we are given a hint that this string is passed to a shell command,
after trying to use the `type` field of the json to inject command unsuccessfully,
we tried to inject command using the other variables that are passed, for example: the `x` variable:

![injecting whoami in x field](whoami_in_x.png)

and we get successful output!

![whoami response](whoami_response.png)

now we know how to execute a command to read the flag:

![reading the flag](reading_the_flag.png)

the flag is:

`corctf{sh0uld_h4ve_r3nder3d_cl13nt_s1de_:msfrog:}`
