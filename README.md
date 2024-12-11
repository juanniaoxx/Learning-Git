

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

- git使用`SHA-1` hash的手段检测文件/文件夹的完整性，并通过其索引文件。

> ##### .gitignore 的规则
>
> - Blank lines or lines starting with # are ignored.
> - Standard glob patterns[^1] work, and will be applied recursively throughout the entire working tree.
> - You can start patterns with a forward slash (/) to avoid recursivity.
> - You can end patterns with a forward slash (/) to specify a directory.
> - You can negate a pattern by starting it with an exclamation point (!).

[^1]: 类似于简化的正则表达式

[关于gitignore的案例](https://github.com/github/gitignore)

### 常用指令的介绍

> #### `git log`
>
> 不带任何参数的git log会按时间倒序展示所有commit记录，包括作者、SHA-1值、commmit message、时间等等。
>
> 常用参数
>
> - `-p` / `--patch` 用于显示每次commit的具体差异 
>   - 可以加上参数 `-n`具体显示几条commit
>   - ![image-20241211121922690](/home/zhw/.config/Typora/typora-user-images/git_log_p_example.png)
> - `--stat` 简要展示汇总信息
>   - ![image-20241211122144031](/home/zhw/.config/Typora/typora-user-images/git_log_stat_example.png)
> - `--pretty=options` 可以修改输出的格式
>   - `oneline` 将每次commit的输出在一行上
>   - `shor`\\`full`\\`fuller` 展示简短\\完整\\更多信息
>   - `format:"参数"` 
>     - `git log --pretty=format:"%h - %an, %ar: %s"`
>     - ![image-20241211122612010](/home/zhw/.config/Typora/typora-user-images/git_log_format_example.png)
>     - ![image-20241211122650986](/home/zhw/.config/Typora/typora-user-images/table_for_pretty_format.png)
>     - `--graph` 会绘制一个漂亮的ASCII branch and merge history
>   - ![image-20241211123110863](/home/zhw/.config/Typora/typora-user-images/table_for_git_log_option.png)

