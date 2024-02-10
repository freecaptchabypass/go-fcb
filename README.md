# go-fcb

Go-lang wrapper for freecaptchabypass.com service which provides real-time captcha-to-text solving.

This wrapper was implemented based on FCB API documentation here https://freecaptchabypass.com/developers/

As the documentation describes, the service receives a url and a recaptcha key, solves it and then return the gRecaptchaResponse key, that needs to be submitted in the website that has the captcha you are trying to solve, in the parameter g-recaptcha-response.

Usually, the recaptcha key can be found in a parameter like that:
```
<div class="g-recaptcha" data-sitekey="6Lc_aCMTAAAAABx7u2W0WPXnVbI_v6ZdbM6rYf16"></div>
```

Example usage:
```
package main

import (
    "fmt"
    "github.com/freecaptchabypass/go-fcb"
)

func main() {
    // Go to https://freecaptchabypass.com/cp/ to get your key
    c := &fcb.Client{APIKey: "your-key-goes-here"}

    key, err := c.SendRecaptcha(
        "http://http.myjino.ru/recaptcha/test-get.php", // url that has the recaptcha
        "6Lc_aCMTAAAAABx7u2W0WPXnVbI_v6ZdbM6rYf16", // the recaptcha key
    )
	if err != nil {
        fmt.Println(err)
	}else{
        fmt.Println(key)
    }    
}

```

Here's the example for regular catpchas (image to text):
```
package main

import (
    "fmt"
    "github.com/freecaptchabypass/go-fcb"
)

func main() {
    // Go to https://freecaptchabypass.com/cp/ to get your key
    c := &fcb.Client{APIKey: "your-key-goes-here"}

    text, err := c.SendImage(
        "your-base64-string", // the image file encoded to base64
    )
	if err != nil {
        fmt.Println(err)
	}else{
        fmt.Println(text)
    }  
}


```
