* Each time a function calls itself, the current state is saved on the stack, and the new call begins. Once the base case is reached, the function starts returning back, one call at a time
* recursion requires additional stack space as compared to iteration, and recursion maybe slower due to function call overhead.
* recursion ends on hitting the base case while iteration ends when it hits the false case

### Memory management in recursion
* next function call is before returning value, so stack frame for each existing call is placed on top of the existing stack frames
* once the topmost stack frame is removed after returning value it comes back to the previous stack frame, where the previous call was made, compiler uses an instruction pointer to keep track of this location to return when the current call is returned
* stack might overflow due to infinite recursion or unnecessary depth, so it terminates abnormally

### Types of recursion 
1. direct recursion:
   * head recursion: body statements include base case check, followed by next function call then any operations
   * tail recursion: function performs its task first then calls the next recursive function
   * tree recursion: function calls itself more than once , like a call_funct(n-1) followed by call_function(n-1) so after the base case returns it calls itself once more
                            call_function(3) .1
            call_function(2) .2                                     call_function(2).5
    call_function(1).3     call_function(1) .4            call_function(1) .6     call_function(1) .7

* nested recursion: calling a function whose value comes from a called function , instead of a simple call_function(11), call_function(call_function(10))

1. indirect recursion: function doesnt directly call itself but calls another function to call itself
[[Function call stack]]
