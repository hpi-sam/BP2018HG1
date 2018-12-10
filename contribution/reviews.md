# How to do a Review?

In this bachelors project we require a review or pairprogramming for every PR that is being merged.  
But what should such a review look like? What should it include? What should the reviewer look for?

## Topics to focus on:
-  **Understanding**: One of the most important benefits a review can provide is code understanding. Focus on reading every single line that has been altered and actually understanding what it does. If you have trouble with something, don't hesitate to ask. If you manage to understand by yourself but took to long, suggest a refactoring or even just renaming of variables. Team members that will later have to alter that code will thank you for it.
-  **Testing**: Try to see if all the important effects are roustly tested. And also check if test code quality is high. Nobody wants to test if the test quality is meh. And if no tests are being written then the quality of our production code base will also suffer. Test Code Quality might very well be more important than the quality of the code base itself.
-  **Correctness**: Does the PR actually do what was requested in the Issue? Does it make a lot of assumptions about the Issue? Did you maybe think it should do it differently? Mention these things! The intent of a story might not always be clear to everyone, and it's always better to ask an additional question than to just hope for the best.
-  **Code Style**: Luckily most of this should be done by our autoconfigured linters. But if someone disabled them for whatever reason or you find additional style complains (like inconsistent use of  ' and ") mention these.
-  **Code Quality**: This goes hand in hand with **understanding** good code explains itself, good code doesn't need many comments. Good code is not 25 lines in one method. To keep a project adaptable and easy to change later on. Code quality is very very very important. If you aren't very sure on this, *Clean Code, by Robert C. Marting* is in our office, feel free to take a look.

If you keep these points in mind during reviews everyone will benefit more. So do them often, and do them fast!