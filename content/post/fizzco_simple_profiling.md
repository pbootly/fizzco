+++
author = "Matthew Thomas"
title = "FizzCo: Simple Go Profiling"
date = "2022-08-20"
tags = [
"fizzco",
]
series = [ "fizzco" ]
+++

# Go Profiling - Using built in testing packages

## The app
So looking at the application on the face of it there doesn't appear to be a whole lot to it, which at least from my perspective makes it pretty difficult to get into the meat of performance issues. 

It's apparent that the real gains are going to be from the for loop:

```go
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
```

We effectively have three conditionals:

* If a number is divisible by 5 and 3, print "FizzBuzz"
* If a number is divisible by 5, print "Buzz"
* Finally, if a number is divisible by 3, print "Fizz"

There are a few places I'd like to look at later to structure this logic in a more readable way (at least to me), but for now we'll focus on understanding the performance here, so that we can repeatably test for our change impact.

Another thing to note here is it looks like the algorithm has a time complexity of O(n), being linear is going to prove challenging to improve. Then again, BuzzCo must be doing _something_ different.

## A small restructure

I don't want to get too much change into the code just yet, but I've taken the first codebase and split it into three files:
- main.go // This now simply takes the arguments and passes it to a function fizzBuzz/
- fizz_buzz.go // this has our for loop above, taking the iterations in from main.go
- fizz_buzz_test.go // This has currently one benchmark function for us to check CPU profiles.

With that in mind, our benchmark function looks like so:
```go
func BenchmarkFizzBuzz100(b *testing.B) {
	for i := 0; i < b.N; i++ {
		fizzBuzz(100)
	}
}
```
It simply runs the `fizzBuzz` function with 100 iterations b.N times. Whats neat about this is put quite succinctly from [the go docs:](https://pkg.go.dev/testing)

>During benchmark execution, b.N is adjusted until the benchmark function lasts long enough to be timed reliably. 

## Our simple profile

With that setup, I can generate profiles with the following command:
`go test -cpuprofile benchmark.cpu.pb.gz -bench .`

Then I can visualise things with a browser using:
`go tool pprof -http=:6061 benchmark.cpu.pb.gz`

![Flamegraph](/post/images/fizzco-flame-1.png)

With this all setup, we can start looking at what impact our changes make. Not bad for my first day, though I did skip lunch so I guess I'll call it there. As I'm closing stuff down, I notice an unread notification on slack from a Kiefer S.

> "Hey Bob, wondering if I can grab you tomorrow at 0900, there's ITS-1709 on in > JIRA and Keith assured me it would be done EOB Tuesday, which is tomorrow, > would be great to see what your thoughts are on a 24 hour turnaround?

_Shit_. I totally forgot about the JIRA tickets. Well I'll get myself home and maybe take a scan through after dinner. With a quick reply to Kiefer agreeing the morning meet would be okay I power down and get ready for bumper to bumper all the way home.