---
title: Introducing {dittodb}
date: 2020-07-19
image: _DSC1176.jpg
---

Today {dittodb} was released on CRAN. It is designed to make testing database connections easy, reliable, and even fun.

There are already a number of packages that facilitate HTTP-based external services (eg [{httptest}](https://enpiar.com/r/httptest/), [{webmockr}](https://docs.ropensci.org/webmockr/)), but there haven't been good solutions for testing against databases. {dittodb} is designed to solve that: It works by recording (and editing if needed) database interactions as fixtures and then uses those fixtures for automated testing. 

Using dittodb means that one doesn't need to maintain databases on testing infrastructure (eg Travis, GitHub Actions), and can run tests quickly without the latency of connecting to a database, and can develop functions that interact with a database without constant, direct access to that same database. 

### How do I use {dittodb}?
Say we have a database with some [`nycflights`](https://CRAN.R-project.org/package=nycflights13) data in it and we are writing functions that query this data that we want to test. 

For example, we have the simple function that retrieves one airline:

```r
get_an_airline <- function(con) {
  return(dbGetQuery(con, "SELECT carrier, name FROM airlines LIMIT 1"))
}
```

 But we want to make sure that this function returns what we expect. To do this, we first record the response we get from the production database:

```r
start_db_capturing()

con <- DBI::dbConnect(
  RMariaDB::MariaDB(),
  dbname = "nycflights"
)

get_an_airline(con)
DBI::dbDisconnect(con)

stop_db_capturing()
```

This will run the query from `get_an_airline()`, and save the response in a mock directory and file. Then, when we are testing, we can use the following:

```r
with_mock_db({
  con <- DBI::dbConnect(
    RMariaDB::MariaDB(),
    dbname = "nycflights"
  )
  
  test_that("We get one airline", {
    one_airline <- get_an_airline()
    expect_is(one_airline, "data.frame")
    expect_equal(nrow(one_airline), 1)
    expect_equal(one_airline$carrier, "9E")
    expect_equal(one_airline$name, "Endeavor Air Inc.")
  })
})
```

All without having to ever set a database up on Travis 🎉 

Find out more at [{dittodb}'s home on the web](https://dittodb.jonkeane.com) and install it today with `install.packages("dittodb")`. You can get started using {dittodb} with a package you're working on with [`use_dittodb("/path/to/package/")`](https://dittodb.jonkeane.com/reference/use_dittodb.html) which will set everything up to get started testing your database interactions.

### What else can {dittodb} do?

Because {dittodb} uses files as fixtures for database responses, it allows you to test many aspects of your data handling code, even ones that you can't (reliably) trigger with a production database. 

An example that I've run into a number of times is, some upstream process has a bug that results in data in a database that no longer conforms to the data contract you're expecting and it breaks a function that used to work. While the errant data is in the database it's easy to add error handling or data cleaning code to your function, and you can even test that it works. But once the problem is resolved (and hopefully it is quickly!), it is no longer easy to test your error-handling process reliably. With {dittodb}, however you can create any fixture you want and use it in your tests. This way you can ensure your fix not only works, but is ready for the next time you run in to the same problem (all without an emergency hot-fix of your R package). 

This is just one of many [hard-to-test things that {dittodb} and other similar testing frameworks](https://enpiar.com/2017/06/21/7-hard-testing-problems-made-easy-by-httptest/#5-rare-or-difficult-to-trigger-server-behavior) make easier.

### What's in a name?

{{< img "132.png" "Ditto ©Pokémon" "floatright" "125 px" >}}

{dittodb} takes inspiration from a few sources for its name. The first, and most obvious for developers of a certain age, is the [ditto pokemon](https://www.pokemon.com/us/pokedex/ditto) known for its ability to take on the form of, and impersonate any other pokemon. Following this, {dittodb} takes on the form and properties of a database backend, without actually being that database backend. For different (likely non-overlapping) set of developers {dittodb} will recall the [spirit duplicators](https://en.wikipedia.org/wiki/Spirit_duplicator) used to make duplications of printed materials by making an artifact during the writing process that can be used to make further copies. {dittodb} is similar when it is recording fixtures: during the process of interacting with a live backend, it makes copies of the responses that can be used ~~to make further copies~~ while running tests as fixtures.

### What's coming next?

This is just the first release, there's lots more that {dittodb} can do. We are already working on adding [{testthat}](http://testthat.r-lib.org) like `expect_` function to assert that a specific query was made ([#116](https://github.com/ropensci/dittodb/issues/116)). If you have a feature request or find a bug we would love you to [open an issue on GitHub.](https://github.com/ropensci/dittodb/issues/) 

### Special thanks
I couldn't have gotten here without the help of a bunch of folks: contributions from [Mauricio Vargas](https://pacha.dev), thoughtful reviews and comments from Helen Miller and Etienne B. Racine, [rOpenSci](https://ropensci.org) for facilitating the package review, as well as [Neal Richardson's](https://enpiar.com) [{httptest}](https://enpiar.com/r/httptest/) for inspiration.



