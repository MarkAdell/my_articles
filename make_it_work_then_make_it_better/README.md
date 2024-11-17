# Make It Work, Then Make It Better

In software engineering, the principle "Make it work, then make it better" highlights a practical yet disciplined approach to building reliable software. The process begins by focusing on making the code functional and ensuring it meets the requirements. After that, the code is revisited for refactoring and polishing, all before submitting it for review or delivering it to customers.

The first phase is about (as they say) writing code for computers, where the primary goal is to produce a working solution that produces the expected output. The second phase shifts the focus to humans, refining the code for other developers who will read, use, and maintain it.

This doesn't mean completely ignoring code quality in the first phase, but if I were to estimate, I'd say it takes about 30% of the focus at this stage, depending on the context.

## Make It Work

**Prioritizing Functionality**: Ensuring the program works as intended. This might involve hardcoded values, inefficiencies, unhandled exceptions, etc., but that's okay for now.

**Speed Over Perfection**: Delivering a working solution quickly allows us to validate our approach before investing time in enhancing it.

**Understanding the Problem**: Writing quick, functional code helps developers gain a better understanding of the problem's details.

## Make It Better

Here are some key areas to focus on:

**Clear Naming**: Assigning clear and descriptive names to variables, functions, and classes that reflect their intent.

**Code Style**: Adhering to coding standards and guidelines to ensure consistency and readability.

**Code Design**: Following established design principles like SOLID to enhance code maintainability.

**Architecture**: Revisiting the architecture decisions to ensure they suit the specific feature requirements.

**Testing**: Writing automated tests of the appropriate type (unit, integration, etc.) to ensure the code behaves as expected and prevents new updates from breaking existing functionality.

**Logging**: Adding meaningful logs to improve visibility and aid debugging.

**Error Handling**: Ensuring exceptions are handled correctly and gracefully to maintain stability and reliability.  

**Comments**: Adding comments where necessary to clarify non-obvious logic.

**Performance**: Ensuring that the code is efficient and scalable as needed.

# Conclusion

"Make it work, then make it better" encourages developers to focus on solving problems pragmatically before striving for perfection. Write the messy first draft, but don't forget to come back and polish it into a masterpiece!

It's very common for the second phase to be ignored altogether, and this is exactly how technical debt accumulates. Be sure to follow both phases while building software, as this **at least** ensures that the software quality will not degrade over time, which, in my experience, is an achievement in itself.

It's worth noting that **this is not only a programming principle**; you can apply it in many aspects of life. In fact, I followed this approach while writing this blog. Here is what I did:
- I wrote a quick draft. (phase 1)
- I used chatGPT to do some enhancements and rephrasings. (phase 2)
- I made several iterations on chatGPT's output to make it simpler and more relevant. (phase 2)