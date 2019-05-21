---
title: Base IT knowledge l1
date: 2019-05-14 15:59:48
tags: [base, l1]
---

## Clean Code

### code authoring basics: coding and naming conventions

- Use intention revealing names
- Use pronounceable names

### important 'code smells'
### refactoring basics

The basic rules of refactoring are very useful during any refactoring activity:

- when we have tests covering the code
- for changing just the structure of the code
- without changing the functionality

## Computer science fundamentals

### Data structures: stack, array, linked list, queue, bag
### Basic algorithms: elementary sort
### Algorithms complexity basics
### Merge and quick sort
### Hash tables; hash functions
### Priority queue/heap
### Union-find structure and algorithm

## Version control principles

### version control fundamentals, centralized vs distributed
### svn basic usage: checkout, update, commit, merge, conflict resolution
### git basic usage: clone, branches, merging, push, pull
### git comparison to svn

## Automation concepts

### command-line scripting
### powershell scripting
### using msbuild for buiding automation
### Continuous integration setup and usage (cruise control, teamcity)
### overview of other scripting platforms (python, node.js, csipts)

## Computer science

### Divide-and-conquer algorithms generalization
### Graph data structure, BFS, DFS algorithms
### Greedy algorithms: Minimal spanning tree, shortest path

## Computers and networks

### Network fundamentals, OSI model

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/base/osi-model.png)

### transport level protocols: IP, TCP, configuration
### presentatin level protocols: https
### application level protocols: http, ftp, smtp, dns
### using utils: ping, nslookup, tracert, telnet, curl

## Xml concepts

### Xml overview

可扩展标记语言（英语：Extensible Markup Language，简称：XML）

XML设计用来传送及携带数据信息，不用来表现或展示数据，HTML则用来表现数据，所以XML用途的焦点是它说明数据是什么，以及携带数据信息。

- 丰富文件（Rich Documents）- 自定文件描述并使其更丰富
  - 属于文件为主的XML技术应用
  - 标记是用来定义一份资料应该如何呈现
- 元数据（Metadata）- 描述其它文件或网络资讯
  - 属于资料为主的XML技术应用
- 标记是用来说明一份资料的意义
  - 配置文档（Configuration Files）- 描述软件设置的参数

### XPath concepts

XPath即为XML路径语言（XML Path Language），它是一种用来确定XML文档中某部分位置的计算机语言。

XPath基于XML的树状结构，提供在数据结构树中找寻节点的能力。

最简单的XPath如下：`/A/B/C`

### XSD concepts

XSD (XML Schema Definition)，指出如何形式描述XML文档的元素。

XSD用来描述一组规则──一个XML文件必须遵守这些规则，才能根据该schema‘合法（Valid）’。

## Advanced computer science

### strings algorithms: sort, substring search, regular expressions, compression
### dynamic programming
### nonlinear programming
### memory-management (garbage collection)
### data indexing

## Cryptography

### cryptography algorithms: symmetrical, asymmetrical
### applications: .net cryptolibrary, crypto++, else?

## Trees

### binary search trees
### balanced search trees: b-tree, red-black-tree, avl