

[TOC]

# What Can We Learn from the Code in Git’s Initial Commit?

> # Todo List
>
> - [ ] 通过git的第一个源码理解git的操作
> - [ ] 完成南大的CPL-Project
> - [ ] 可选: 
>   - [ ] 学完Rust后重构git
>   - [ ] 进一步提高git的功能

## Part I 通过这片博客初步理解git的第一次提交的源码

[What Can We Learn from the Code in Git’s Initial Commit?](https://www.atlassian.com/blog/bitbucket/what-can-we-learn-from-the-code-in-gits-initial-commit)

关于git原理看[《Pro git》](https://git-scm.com/book/en/v2)

<details>
    <summary>How to Write a Git Commit Message</summary>
    <div>
        写一个优雅且能别大部分接受coomit message是很重要的事情！
        参考链接https://cbea.ms/git-commit/
    </div>
</details>

git的目录结构

├── cat-file.c `git cat-file`
├── commit-tree.c `git commit`
├── init-db.c  `git init`
├── read-cache.c 
├── read-tree.c `git read-tree`
├── show-diff.c `git diff`
├── update-cache.c `git add`
└── write-tree.c `git write-tree`

| **Git’s Initial Commit** | **Current Git Version** | **Purpose**                                                  |
| ------------------------ | ----------------------- | ------------------------------------------------------------ |
| init-db                  | git init                | Initialize a Git repository                                  |
| update-cache             | git add                 | Add a file to the staging area                               |
| write-tree               | git write-tree          | Write a new tree object to the Git repository using the content in the staging index |
| commit-tree              | git commit              | Create a new commit object in the Git repository based on the specified tree |
| read-tree                | git read-tree           | Display the contents of a tree object from the Git repository |
| show-diff                | git diff                | Show the differences between staged Git files and their corresponding working directory versions |
| cat-file                 | git cat-file            | Display the contents of objects stored in the Git repository |

<details>
    <summary>读代码真头疼呀</summary>
    <div>
       明明只有1000来行，但为感觉为已经要死了
    </div>
</details>



## 阅读《Pro git》的收获

