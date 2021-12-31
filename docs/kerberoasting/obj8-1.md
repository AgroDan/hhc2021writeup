# Introduction

This challenge was a ride and a half. From finding the AD server, to interrogating it to obtain more information and slowly pivoting from one server to another, this was a multi-step process to ultimately getting the secret documents necessary to complete the challenge. This challenge involved Kerberoasting, Password Cracking, Plundering data, using their own tools against them, and all of this performed with heavy usage of the [Impacket library](https://github.com/SecureAuthCorp/impacket). So come on along with me as I start my journey to (mostly) domain takeover! 

Unfortunately not a complete domain takeover, but I understand the reasoning behind that. You can't have random people taking over a domain or you'd have to reset the instance every 5 minutes.

Anyway, onto the pwn4g3!

Our journey starts here: [Elf University Student Registration](https://register.elfu.org/register)

![Student Registration](/img/obj8-1/img1.png)


Before I even consider entering data, first thing I'd like to do is quickly check the source of the page. So by hitting ++ctrl+u++, I can get the source code, and nothing really stands out initially...except for THIS:

```html hl_lines="8-9"
            <div class="input-field col s12 center" style="text-align: center;">
              <button class="btn white black-text waves-effect z-depth-1 y-depth-1 center" type="submit" value="submit">Submit</button>
            </div>
            <div class="col s12">
              <div class="center" style="font-size: 12px;">@ 2021 Elf University - All Rights Reserved</div>
            </div>
            <div class="col s12">&nbsp;</div>
            <!-- Remember the groups battling to win the karaoke contest earleir this year? I think they were rocks4socks,
            cookiepella, asnow2021, v0calprezents, Hexatonics, and reindeers4fears. Wow, good times! -->
          </form>
        </div>
      </div>
```

W....what? I'm sure that will come into play later!

Anyway, let's register!
