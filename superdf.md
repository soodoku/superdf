# Define the MyDataFrame class

    SuperDataFrame <- setRefClass(
      "MyDataFrame",
      fields = list(
        data = "data.frame",
        version = "character",
        author = "character",
        notes = "character"
      ),
      methods = list(
        initialize = function(data, version = "", author = "", notes = "") {
          .self$data <- data.frame(data)
          .self$version <- version
          .self$author <- author
          .self$notes <- notes
        },
        addVersion = function(newVersion) {
          .self$version <- newVersion
        },
        addAuthor = function(newAuthor) {
          .self$author <- newAuthor
        },
        addNotes = function(newNotes) {
          .self$notes <- newNotes
        }
      )
    )

### Create an instance of SuperDataFrame

    df <- SuperDataFrame$new(data = data.frame(A = c(1, 2, 3), B = c(4, 5, 6)))

    # Set the version, author, and notes
    df$addVersion("1.0")
    df$addAuthor("John Doe")
    df$addNotes("Some additional information")

    # Access the custom attributes
    print(df$version)  # Output: 1.0

    ## [1] "1.0"

    print(df$author)  # Output: John Doe

    ## [1] "John Doe"

    print(df$notes)  # Output: Some additional information

    ## [1] "Some additional information"

    # Perform regular data.frame operations
    df$data$C <- df$data$A + df$data$B
    print(df$data)

    ##   A B C
    ## 1 1 4 5
    ## 2 2 5 7
    ## 3 3 6 9

    # Save the object to an RDS file
    saveRDS(df, file = "mydataframe.rds")

    # Load the object from the RDS file
    df_restored <- readRDS(file = "mydataframe.rds")
    df_restored$version

    ## [1] "1.0"
