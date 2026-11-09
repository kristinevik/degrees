# Six Degrees of Kevin Bacon

How many movies apart are any two actors? This program finds the **shortest chain of co-stars** linking them, using a real IMDb-based dataset of about 1 million people and 340,000 movies.

```
$ python degrees.py large
Loading data...
Data loaded.
Name: Emma Watson
Name: Kevin Bacon
...
2 degrees of separation.
1: Emma Watson and Tom Hanks starred in The Circle
2: Tom Hanks and Kevin Bacon starred in Apollo 13
```

## How it works

The actors and movies form a graph. Each person is a node, and two people are connected if they starred in the same movie.

- **Breadth-first search** explores outward one "degree" at a time, so the first path it finds is guaranteed to be the shortest.
- **Early goal check:** the search returns as soon as the target appears among a person's co-stars, instead of waiting until that person is taken off the queue. This saves a lot of work on a graph this size.
- **Depth-first search** is also supported (`shortest_path(..., method="dfs")`). I added it to compare the two. DFS finds *a* path, but there's no guarantee it's the shortest one, which shows why BFS is the right tool here.
- If a name matches several people, the program asks which one you mean.

## Run it

No dependencies, just Python 3:

```bash
python degrees.py large   # full dataset (takes a little while to load)
python degrees.py small   # tiny dataset for quick testing
```

## Built with

Python (standard library only)
