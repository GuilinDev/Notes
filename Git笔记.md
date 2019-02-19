# Git笔记

最小配置:
```text
git config --global user.name "your_name"
git config --global user.email "your_email@domain.com"
```

## ~/.gitconfig文件
Git存储全局配置选项的文件。通过~/.gitconfig文件可以做很多事情，包括定义别名，永久的打开（或关闭）一些特定的命令选项，还可以修改Git如何工作的方面（例如：git diff使用哪个diff算法，或者默认使用什么类型的的合并策略）。你甚至可以按条件地基于路径包含其他配置文件到一个仓库！使用“man git-config”查看所有细节。

## ~/.gitconfig文件
git config 命令中的—global告诉Git更新“global”配置，也就是~/.gitconfig发现的这个配置。当然，拥有一个全局的配置代表了一个本地配置，如果省略—global选项，git config 会更新这个仓库自己的配置，这个配置文件存储在.git/config。

在.git/config中设置的选项会推翻在~/.gitconfig文件中的对应设置。因此，例如，如果需要在一个特定的仓库中使用一个不同的邮箱地址，可以运行“git config user.email "also_you@example.com"”。然后，你在这个仓库中提交会使用单独配置的这个邮箱地址。如果使用一个工作的电脑在开源项目中工作，但是希望在这个项目中使用个人的邮箱地址，而其他在主Git配置中仍然使用工作邮箱，这一点是非常有用的。

在~/.gitconfig中可以设置的任何东西，都可以在.git/config中设置来对这个仓库做特定设置。在接下来的技巧中，当提到在~/.gitconfig文件中添加什么东西，同时也说明可以在特定的仓库的.git/config中添加来设置那个选项。

~/.gitconfig可以做别名，创建别名的工作原理就像shell命令行里的别名——设置一个新的命令名称来调用一个或者多个其他的命令，这些命令通常包括一些特定的选项或标识。别名对于经常使用的那些又长又复杂的命令行非常有效。可以使用git config命令来定义别名——例如，执行”git config —global —add alias.st status”命令后，会使得执行git st与执行git status做的是同样的事情——然而，我发现当定义别名的时候，只需要直接在~/.gitconfig文件里编辑通常会更加容易。

如果这么做，~/.gitconfig文件就是一个INI文件，INI是一种带有特定段落的基础键值对文件格式。添加一个别名时，将改变[alias]段落。例如：上面提到的定义相同的git st别名，需要添加下面这段代码：
```text
[alias]
st = status
```