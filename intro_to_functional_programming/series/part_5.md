# Yet another introduction to Functional Programming (Part Five)

Welcome to the fifth and final part of our series of articles on Functional Programming. In the previous part, we discussed First-class functions and Higher-order functions. In this part, we will show how we can utilize all the functional programming concepts that we covered within object-oriented programming code.

Be sure to check our previous parts:

- [Yet another introduction to Functional Programming (Part One)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_1.md)
- [Yet another introduction to Functional Programming (Part Two)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_2.md)
- [Yet another introduction to Functional Programming (Part Three)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_3.md)
- [Yet another introduction to Functional Programming (Part Four)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_4.md)

## Can functional programming be used within OOP code?

Definitely! You can make use of several functional programming concepts while writing object-oriented code, such as immutability, pure functions, and higher-order functions.

Let's see a Java example where **all** the concepts we talked about in the previous articles are applied:

```java
import java.util.List;
import java.util.stream.Collectors;

public class BranchService {
    private BranchRepository branchRepository;

    public BranchService(BranchRepository branchRepository) {
        this.branchRepository = branchRepository;
    }

    public List<String> getActiveBranches(int storeId) {
        List<Branch> branches = branchRepository.getBranchesByStoreId(storeId);
        List<String> formattedBranches = formatBranches(branches);
        return formattedBranches;
    }

    private List<String> formatBranches(List<Branch> branches) {
        return branches.stream()
                .filter(branch -> branch.isActive())
                .map(branch -> branch.getName().toUpperCase())
                .collect(Collectors.toList());
    }
}
```

This is a simple service class that has a public method `getActiveBranches`, which retrieves data from some data store, then applies a series of manipulations to the retrieved data before it returns it.

Functional programming concepts applied in this class:
- Preserving the **Immutability** of the `branches` list retrieved from the data store.
- Creating a **Pure Function** `formatBranches` that accepts the list of branches and returns a new list with the desired transformations.
- The `formatBranches` function is implemented in a **Declarative** manner, making use of **Higher-order functions**.

## Conclusion

This concludes the last part of our series. There is still much more to learn about functional programming. Feel free to dive deeper into this beautiful paradigm. The aim of this series of articles was to explain the basic principles that you can start applying today, making your code more maintainable and resistant to bugs.

## References

- https://github.com/xgrommx/awesome-functional-programming
- https://dzone.com/articles/about-immutability-in-object-oriented-programming
- https://www.youtube.com/watch?v=0if71HOyVjY
- https://www.youtube.com/watch?v=e-5obm1G_FY