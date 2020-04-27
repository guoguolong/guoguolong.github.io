---
title: Git workflow suggestion for Web Application
tags: [git]
date: 2020-04-27 14:00:00
categories: [IT]
---

Git工作流程种类繁多，常见的有：

> Git flow: http://nvie.com/posts/a-successful-git-branching-model/
> Github flow: [scottchacon.com/2011/08/31/github-flow.html](http://scottchacon.com/2011/08/31/github-flow.html)
> Gitlab flow: http://doc.gitlab.com/ee/workflow/gitlab_flow.html

三种流程各有特点，无所谓哪个更好，各有特色。鉴于我司各个技术层次工程师现状和项目种类，我们需要定义组织内特有的git流程，并分级、分阶段实施.

前面提到我司项目种类，主要是两大类：

>  \- 上线类项目：有master分支并被TMP控制权限的Web项目。
>
>  \- 非上线类项目：分支任意设置，通过 gitbucket 系统直接管控分支权限（如果需要），但通过非tmp渠道上线的项目（如npm包引用、app渠道发布）。

## A. 上线类项目的git流程

### 三个Level的简化流程

#### Level 1: 遵从TSP/SVN发布流程(并行合并到master)

{% asset_img "level1.png" "Level 1" %}


远程仓库分支看起来：

```
master branch test
```

#### 关键特征

- master作为发布分支
- 多个迭代的功能可能同时存在于每一个分支.
- 每个迭代开发团队自行进行分支合并

#### 基本工作流程

1. JIRA自动创建git项目：默认创建好branch、test、master分支(master分支等同于svn的stable分支)
2. branch分支：总是在branch下开发——实质含义是：开发时期代码总是共用远程branch分支，至于本地对应分支名是任意的，虽然我建议你使用同名branch作为本地分支.
3. test分支：开发完提交到远程branch，开发人员测试通过后，合并到test分支提交给测试人员 —— 和svn一样，是使用cherry pick合并，不是全量合并！否则你会把别人branch上的代码也合并过去.
4. master分支：测试人员将test分支部署测试完毕后，亲自或授权开发人员合并到master分支：建立JIRA单，走TMP发布流程申请权限，然后提交合并代码到master分支.
5. 发布：通过TMP发布maser分支代码到PRE，测试通过后再发布到PRD，

如果遵从上面的步骤，你几乎与tmp/svn发布项目有完全一样的感受——tmp/svn有的问题，这里都存在！ 该git流程设置存在一个更致命的问题：tmp/svn上线功能的时候，能明确指定jira号对应的更新文件，以免误发他人的文件到线上；而git(无论Jenkins还是docker部署)只能指定head或特定版本号发布，这将几乎无法避免地带上他人合并到master但还没发布的代码.

BTW，在这个流程中，没有提及使用任何工具code review，实质是: 真的和tmp/svn方式一样—— 在你合并到master分支前，告诉code reviewer自己提交的代码版本号，code reviewer择机git pull下来进行查看，间接或者直接修改后提交。

注：对于极微团队，分支间同步更粗糙的方式是：全量合并，前提要保证远程开发分支代码在合并前可构建运行.

#### Level 2: cherry pick串行合并到master

{% asset_img "level2.png" "Level 2" %}


远程仓库分支看起来：

```
master branch test
```

Level 2是在Level 1的基础上的改进，以下仅介绍差异：

#### 关键特征

- 设置Merger 角色：专门负责合并test到master分支.

#### 基本工作流程

1. test分支：假设有F1、F2两个特性均到了test分支，当天都测试通过后，分别向Merger提交了merge到master分支的请求，要求上线。
2. maste分支：Merger收到多个合并请求，根据业务安排，Merger同一时刻仅能选择1个特性合并到master，然后测试发布，直接该特性上线完成，才能继续合并第2个合并请求，反复前面的过程，直至所有特性测试发布完成.
   1. 因为test分支仍然同时存在多个迭代团队功能特性，比如Merger在选择合并F1到master分支操作时，必须使用cherry-pick，即：仅合并F1提交的版本号.

#### Level 3: 全量串行合并到master

{% asset_img "level3.png" "Level 3" %}

远程仓库分支看起来：

```
master branch-f1 branch-f2 branch-f3
```

Level 3与Level 2和Level1 没有紧密的继承关系，但仍有如下关键的相似特征：

#### 关键特征

- master仍然作为发布分支并受tmp控制.
- 设置Merger 角色：专门负责合并branch-*到master分支.
- 抛弃test分支

#### 基本工作流程

Level 3 远程分支看起来如下：

1. branch-*分支：每个特征开发小组在迭代伊始，从master复制一个开发分支即branch-*分支进行开发.
   1. 开发和测试人员在同一个分支里开发和测试.
   2. 测试人员为每一个迭代创建相应的test环境，当然代码都是从相应的branch-*里拉出
2. 开发测试完成，迭代小组向Merger提交合并到master分支的申请，要求上线.
3. master分支：Merger同时收到多个合并请求，根据业务安排，Merger决定优先选择一个分支合并到master，然后测试发布，直接该特性上线完成，才能继续合并第2个合并请求，重复前面的过程，直至所有特性测试发布完成. 几个要点：
   1. 此merge和Level 2的合并同属合并，但是关键区别在于：这个合并是全量合并！举例说合并branch-f1的功能到master，既不会像cherry-pick那样把branch-f2的合并到master，也拜托了cherry-pick依次挑出相应的版本号进行合并，大大提高了合并效率和准确性。
   2. 发布完成后，对应的开发分支可以删除了。下次开发新的功能时，总是从master复制出一个新的开发分支

注：假设branch-f2分支创建的时候版本为f1，当branch-f2开发测试完成准备合并到master的时候发现f1已经在master了，必须反向合并：你应该总是在合并到master之前先反向合并master到branch-*分支，如果发现有更新，必须要进行回归测试！

### 最佳实践

1. 如果上线了一个功能，应总是给当前master的最新版本打上一个tag作为快照。尽管我们可能使用docker回滚，但是这个方式非常有助于历史回溯。
2. 向Merger提交merge申请，可使用 git 仓库的Merge Request功能，同时也实现了Code Review协作。
3. 使用git，没有hook限制提交的时候一定要输入JIRA号，tmp系统也不使用JIRA号，但是你提交变更，应该总是使用JIRA号便于历史回溯.

到Level 1、2、3在团队内实践熟练到一定阶段，我们可以考虑采用更严谨的git工作流程了.

## B. 非上线类项目的git流程

非上线类项目是指通过非tmp渠道上线的项目（如npm包引用、app渠道发布），该类项目完全通过 gitbucket 系统进行管理，包括成员权限设定、分支任意设置等。因此，该类型的项目可以无障碍地选择使用文章开头提到的git flow、github fow或gitlab flow.


