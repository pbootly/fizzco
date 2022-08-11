+++
author = "Matthew Thomas"
title = "Welcome to Fizz Co!"
date = "2022-08-10"
tags = [
"fizzco",
]
series = [ "fizzco" ]
+++

# Fizz Co, My first day.

After what seems like a lifetime of recruiter calls, failed interviews and several occurrences of wondering if technology
really is for me, I've finally secured my first developer gig. The company courteous to hire me are called Fizz Co. I couldn't
find much information online about their product, who their customers are or anything really. What I do know is
that they've been the leader in their industry for the past 10 years but have taken a few hits from an emerging startup -
Buzz Cola. 

Buzz were founded by Walt Carlson, a tech genius out of silicon valley and their marketing seems to suggest they have 
unparalleled performance compared to anything else on the market. As a result, my hiring is part of a drive by Fizz Co 
to increase the efficiency of our software stack, working as part of a product engineering team.

Induction was very quick, meeting Kathy from HR for a whistle-stop tour of the office; a bullpen full of sales people talking aggressively
into their headsets I was greeted with momentary awkward smiles, almost pitiful. After that I was handed a used laptop by Kyle, 'the IT guy'
and shown to my desk. Kyle mentioned that all relevant access and links to get started with the codebase were in my inbox.

With coffee in hand I boot the machine up, prepared to make a good impression I'm excited to get deep into the code and finally
flex my muscles with something real. The first email in my inbox is from Kathy, and there was something that was certainly news
to me.

> Subject: Welcome Bob to Fizz Co!
> 
> Hi All,
> 
> As I'm sure you're all aware, our previous software engineer recently left us to work elsewhere.
> 
> Today is Bobs first day and is going to be picking up that mantle, we know you'll absolutely smash it of course!
> 
> Please everyone join me in wishing a warm welcome to Bob!
> 
> Kind regards,
> 
> Kathy

What do they mean *previous software engineer*? 

That must've been Keith from the tech interview. I'm starting to wonder, am I the only developer here? 

Remaining optimistic I figure the code must be pretty stable if they only need one dev. Looking around at some other 
emails I see one from Kyle:
> Subject: SVN Repo Credentials
> 
> Hey Bob,
> 
> The apps source is stored on SVN, please find the server info attached.
> 
> Thanks,
> 
> Kyle

Huh, SVN and not GIT? Seems a bit legacy, but it's not a problem, hey maybe if I'm the only one maintaining it I'll find 
some time to move it over! Yeah! okay lets take a look at how they've structured things.

I spend the next 20 minutes looking around the server, I can only find a single file called main.go on trunk and there aren't any branches
that seem to have anything more. I send a reply to Kyle:

> Re: SVN Repo Credentials
> 
> Hello Kyle,
> 
> Thanks for this, I've managed to get onto the server, but I can only see a small go application. It's been a while since
> I've used SVN, can you let me know if there's something I'm obviously missing?
> 
> Thanks,
> 
> Bob

As if Kyle was awaiting my question I get an immediate reply:
> Yep, if you've got main.go that's it dude. Good luck.
> 
> Kyle

Okay, this is fine I tell myself. The code must be fairly straightforward and maybe Keith didn't think to set things up with
some defined structure. I crack open my IDE and to my amazement main.go is incredibly small:

```
package main

import (
    "fmt"
    "os"
    "strconv"
)

/*
COPYRIGHT FIZZCO LTD.
*/

func main() {
    // Get iterations on the argument parsed
    arg := os.Args[1]
    
    if len(os.Args) < 1 {
        fmt.Println("You need to enter the number of iterations you want.")
        os.Exit(23)
    }

    argVal, err := strconv.Atoi(arg)
    if err != nil {
            fmt.Println("Argument entered not a valid integer")
            os.Exit(1)
    }

    for i := 0; i <= argVal; i++ {
            if (i%5 == 0) && (i%3 == 0) {
                    fmt.Println("FizzBuzz")
            } else if i%5 == 0 {
                    fmt.Println("Buzz")
            } else if i%3 == 0 {
                    fmt.Println("Fizz")
            } else {
                    fmt.Println(i)
            }
    }
}
```
... You can't be serious. *THIS* is the product? I'm supposed to make this faster for our customers?

In my disbelief I go back to my emails, searching for something, anything that makes sense. I find a link to a JIRA board,
my thinking is that somewhere in some kind of ticket will provide the context I need. The first thing I notice is that
12 of the items in the backlog are already assigned to me, and every single one is marked as urgent priority. Thanks, Keith.

I take a deep breath, then another and pick the oldest ticket marked urgent. As I see it I realise that I'm going to need another coffee.