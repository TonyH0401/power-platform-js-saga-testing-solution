# Introduction

**JS Saga Testing** is a model-driven **Power Platform** solution containing multiple model-driven applications such as **Caladan Housing**, etc.

# Development Note

There are numberous methods of version control a Power Platform solution/application, Power Platform also supported it natively. However, here are some of the methods I implemented due to its flexibility and ease of usage.

- Export the Power Platform manually.
  - This is the easiest method for version control. Once exported, it will be a `.zip` file, unzip it and push to your favourite version control repo.
  - The downside of this method is the size of the repo can grow exponentially which can exceed the size limit of a version control repo such as GitHub. Each time you modify the solution, you need to export, unzip and push the whole unzip solution to your version control repo, which can be a hassle.
  - If you need to import it, you just need to zip the folder (without the `README.md` file) and import the solution like normal.
- Export using Azure DevOps + Power Platform Tools.
  - The solution is conveniently converted into code with controlled size, it supports managed and unmanaged solution exportation and it can also be integrated with the import pipeline.
  - Because it's used with Azure DevOps, it's locked down with Azure Repo, you can move it to other version control repo such as GitHub but it would be a hassle. Setting it up can be quite complicated but once it's running, the result will be guaranteed.
  - If you need to import it, you just need to create/use the import pipeline. If your repo has a `README.md` file, remember to remove it or not.

For this solution, I will use "Export using Azure DevOps + Power Platform Tools" method.
