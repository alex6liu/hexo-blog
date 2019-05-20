---
title: svn and git
date: 2019-05-16 14:52:34
tags: [cvs, l1]
---

## Knows main characteristics of centralized VCSs, can name most popular Centralized VCSs (SVN, etc.)

Centralized VCS systems are designed with the intent that there is One True Source that is Blessed, and therefore Good. All developers work (checkout) from that source, and then add (commit) their changes, which then become similarly Blessed.

## Knows main characteristics of Distributed VCSs, can name most popular Distributed VCSs (Git, Mercurial, etc.)

Distributed VCS systems are designed with the intent that one repository is as good as any other, and that merges from one repository to another are just another form of communication. Any semantic value as to which repository should be trusted is imposed from the outside by process, not by the software itself.

## Knows main differences between Centralized and Distributed VCS

1.集中式版本控制系统（CVS,SVN）

有一个中央服务器，干活的时候，用的都是自己的电脑，需要先从中央服务器获取最新的版本，然后开始干活，干完活了，再把自己的修改推动给中央服务器。

缺点：需要联网的情况下才能使用，上传速度慢。

2.分布式版本控制系统（最常见的Git）

分布式版本控制系统没有中央服务器，每个人的电脑上都用一个完整的版本库，只要交换对方的修改就行，把各自的修改推送给对方。分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

优点：安全性高，不需要联网

## Understands difference between Rebase and Merge Git commands

[link](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)