# Assignment-3--lexical-scoping

makeCacheMatrix <- function(x = numeric()) {

        # holds the cached value or NULL if nothing is cached
        # initially nothing is cached so set it to NULL
        cache <- NULL

        # store a matrix
        setMatrix <- function(newValue) {
                x <<- newValue
                # since the matrix is assigned a new value, flush the cache
                cache <<- NULL
        }

        # returns the stored matrix
        getMatrix <- function() {
                x
        }

        # cache the given argument 
        cacheInverse <- function(solve) {
                cache <<- solve
        }

        # get the cached value
        getInverse <- function() {
                cache
        }

        # return a list. Each named element of the list is a function
        list(setMatrix = setMatrix, getMatrix = getMatrix, cacheInverse = cacheInverse, getInverse = getInverse)
}

#this is followed up by the inverse of special matrix

cacheSolve <- function(y, ...) {
        # get the cached value
        inverse <- y$getInverse()
        # if a cached value exists return it
        if(!is.null(inverse)) {
                message("getting cached data")
                return(inverse)
        }
        # otherwise get the matrix, caclulate the inverse and store it in
        # the cache
        data <- y$getMatrix()
        inverse <- solve(data)
        y$cacheInverse(inverse)

        # return the inverse
        inverse
}

solution

a$getMatrix();
	#>      [,1] [,2]
	#> [1,]    1   12
	#> [2,]    2   13

	cacheSolve(a)
	#> [,1]        [,2]
	#> [1,] -1.1818182  1.09090909
	#> [2,]  0.1818182 -0.09090909

	# the 2nd time we run the function,we get the cached value
	cacheSolve(a)
	#> getting cached data
	#> [,1]        [,2]
	#> [1,] -1.1818182  1.09090909
	#> [2,]  0.1818182 -0.09090909
        
        
        # the matrix can be created after calling a `makeCacheMatrix`
without arguments.

a$setMatrix( matrix(c(1,2,12,13), nrow = 2, ncol = 2) );
	a$getMatrix();
	#>      [,1] [,2]
	#> [1,]    1   12
	#> [2,]    2   13

	cacheSolve(a)
	#> [,1]        [,2]
	#> [1,] -1.1818182  1.09090909
	#> [2,]  0.1818182 -0.09090909

	# the 2nd time we run the function, we get the cached value
	cacheSolve(a)
	#> getting cached data
	#> [,1]        [,2]
	#> [1,] -1.1818182  1.09090909
	#> [2,]  0.1818182 -0.09090909
