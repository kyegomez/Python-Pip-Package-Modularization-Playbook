# Python Pip Package Modularization Playbook

## Introduction
Modularization is crucial for maintaining and understanding code in Python packages. This playbook provides guidelines for modularizing imports in a Python pip package and dealing with git-cloned repositories as part of your main folder.

## 1. Package Structure

The typical structure of a Python package is as follows:

```
your_package/
|---- your_package/
|     |---- __init__.py
|     |---- module1.py
|     |---- module2.py
|     |---- subpackage1/
|          |---- __init__.py
|          |---- module3.py
|---- setup.py
|---- README.md
```

The `__init__.py` files are necessary to make Python treat the directories as containing packages. 

## 2. Modularizing Imports

Python has a specific way to structure your imports, depending on where the modules are located.

- If `module1` wants to import `module2`, you would add `from . import module2` at the top of `module1.py`.

- If `module3` inside `subpackage1` wants to import `module1` from the parent package, you would add `from .. import module1` at the top of `module3.py`.

Following this structure allows you to keep your imports clean and understandable, which is crucial for maintaining the package.

## 3. Best Practices for Imports

- Always use absolute names for your imports, as they are clear and not prone to confusion. For instance, `from your_package import module1` is better than `import module1`.

- Explicit is better than implicit. From PEP 8, "Wildcards (from . import *) should be avoided as they make it unclear which names are present in the namespace."

- Group your imports in the following order: Standard library imports -> Related third-party imports -> Local application/library-specific imports. Include a blank line between each group of imports.

- Keep your codebase DRY (Don't Repeat Yourself). If you find that you are repeating import statements across multiple files, consider refactoring your package layout.

## 4. Dealing with Git-Cloned Repositories

When you clone a repository inside your main folder, you add an external dependency to your package. It's not a good practice to include git-cloned repositories in your package, because:

- It makes your package size unnecessarily large.
- It makes version control harder.
- The cloned repository may have its own dependencies that conflict with yours.

It's better to add such a repository as a dependency in your `setup.py` or `requirements.txt` file. This way, when your package is installed, pip will also install these dependencies. 

However, if you must use a git-cloned repository inside your package, you can treat it as a subpackage. To import modules from this repository, use the relative import method described above.

## 5. Tutorials
There are several good tutorials that can guide you through creating your own Python package:

- The [Python Packaging User Guide](https://packaging.python.org/tutorials/packaging-projects/)
- The [Hitchhiker’s Guide to Python](https://docs.python-guide.org/writing/structure/)
- The [Official Python documentation](https://docs.python.org/3/tutorial/modules.html#packages)

Remember that good code is readable, maintainable, and reusable. Structuring your package in a clear, logical way is key to achieving these goals.
