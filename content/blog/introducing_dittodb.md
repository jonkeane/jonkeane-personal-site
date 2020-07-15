---
title: Introducing dittodb
date: 2020-07-13
---

Today `dittodb` was released on CRAN. It is designed to make testing database connections easy, reliable, and even fun.

There are already a number of packages that facilitate HTTP-based external services (eg [httptest](https://enpiar.com/r/httptest/), [webmockr](https://docs.ropensci.org/webmockr/)), but there haven't been good solutions for testing against databases. `dittodb` is designed to solve that: It works by recording (and editing if needed) database interactions as fixtures and then uses those fixtures for automated testing. 

Using dittodb means that one doesn't need to maintain databases on testing infrastructure (eg Travis, GitHub Actions), and can run tests quickly without the latency of connecting to a database, and can develop functions that interact with a database without constant, direct access to that same database. 

### How do I use `dittodb`?
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

Find out more at [`dittodb`'s home on the web](https://dittodb.jonkeane.com) and install it today with `install.packages("dittodb")`.

### What's in a name?


{{< figure src="/images/132.png" caption="Ditto ©Pokémon" width="125px" class="floatright" >}}

`dittodb` takes inspiration from a few sources for its name. The first, and most obvious for developers of a certain age, is the [ditto pokemon](https://www.pokemon.com/us/pokedex/ditto) known for its ability to take on the form of, and impersonate any other pokemon. Following this, `dittodb` takes on the form and properties of a databse backend, without actually being that database backend. For diffrent (likely non-overlapping) set of developers `dittodb` will recall the [spirit duplicators](https://en.wikipedia.org/wiki/Spirit_duplicator) used to make duplications of printed materials by making an artifact during the writing process that can be used to make further copies. `dittodb` is similar when it is recording fixtures: during the process of interacting with a live backend, it makes copies of the responses that can be used ~~to make further copies~~ while running tests as fixtures.

### What's coming next?

This is just the first release, there's lots more that `dittodb` can do. We are already working on adding [testthat](http://testthat.r-lib.org) like `expect_` function to assert that a specific query was made ([#116](https://github.com/jonkeane/dittodb/issues/116)). If you have a feature request or find a bug we would love you to [open an issue on GitHub.](https://github.com/jonkeane/dittodb/issues/) 





