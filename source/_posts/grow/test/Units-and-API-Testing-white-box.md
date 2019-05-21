---
title: Units and API Testing(white box)
date: 2019-05-16 14:54:20
tags: [test, l1]
---

## Unit testing basics

### Writes unit tests

FIRST Principles of Good Unit Tests:

- [F]ast
- [I]solated
- [R]epeatable
- [S]elf-validating
- [T]imely

### Understands the purpose of unit testing

The goal of unit testing is to segregate each part of the program and test that the individual parts are working correctly. It isolates the smallest piece of testable software from the remainder of the code and determines whether it behaves exactly as you expect.

## Mocking Libraries

### Has experience with any Mocking libraries

`Sinon.js`

## TDD and BDD approaches

### Explains TDD and BDD approaches

- Test Driven Development

其倡导先写测试程序，然后编码实现其功能得名。测试驱动开发始于20世纪90年代。测试驱动开发的目的是取得快速反馈并使用“illustrate the main line”方法来构建程序。

测试驱动开发是戴两顶帽子思考的开发方式：先戴上实现功能的帽子，在测试的辅助下，快速实现其功能；再戴上重构的帽子，在测试的保护下，通过去除冗余的代码，提高代码质量。测试驱动着整个开发过程：首先，驱动代码的设计和功能的实现；其后，驱动代码的再设计和重构。

- Behavior-driven development

它鼓励软件项目中的开发者、QA和非技术人员或商业参与者之间的协作。

BDD的重点是通过与利益相关者的讨论取得对预期的软件行为的清醒认识。

这让开发者得以把精力集中在代码应该怎么写，而不是技术细节上

### Uses Test Driven Development on projects with already implemented practices

## Test Doubles

### Knows what test doubles is. Explains the difference between test doubles

- **Dummy** objects are passed around but never actually used. Usually they are just used to fill parameter lists.
- **Fake** objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an InMemoryTestDatabase is a good example).
- **Stubs** provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test.
- **Spies** are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.
- **Mocks** are pre-programmed with expectations which form a specification of the calls they are expected to receive. They can throw an exception if they receive a call they don't expect and are checked during verification to ensure they got all the calls they were expecting.

## Testing Pyramid

### Explains what Testing Pyramid is. Describes benefits versus Testing Ice-Cream.

The **test pyramid** is a way of thinking about different kinds of automated tests should be used to create a balanced portfolio. Its essential point is that you should have many more low-level UnitTests than high level BroadStackTests running through a GUI.

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/test/testing-pyramid.png)

Testing Ice-Cream 大部分都是人工测试

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/test/testing-icecream.png)