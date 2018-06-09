# bulk
Homework 07 task. [OTUS C++]

[![Build Status](https://travis-ci.org/DGolgovsky/bulk.svg?branch=master)](https://travis-ci.org/DGolgovsky/bulk)
[![Code Health](https://landscape.io/github/DGolgovsky/bulk/master/landscape.svg?style=flat)](https://landscape.io/github/DGolgovsky/bulk/master)
[ ![Download](https://api.bintray.com/packages/dgolgovsky/otus-cpp/bulk/images/download.svg) ](https://bintray.com/dgolgovsky/otus-cpp/bulk/_latestVersion)

**Task description**

Develop a program for batch processing commands. Commands are read line by line from standard input and processed by blocks by N teams. One command is one line, the value of the role does not play. If the data is over, the block is terminated forcibly.

The parameter N is passed as the only command-line parameter in
as an integer.
```
input | output
------|-------
cmd1  |
cmd2  |
cmd3  |
      | bulk: cmd1, cmd2, cmd3
cmd4  |
cmd5  |
      | bulk: cmd4, cmd5
```

The block size can be changed dynamically if before the beginning of the block and immediately after the command `{` and `}` respectively. The previous package for
this is forcibly completed.
```
input | output
------|-------
cmd1  |
cmd2  |
cmd3  |
      | bulk: cmd1, cmd2, cmd3
{     |
cmd4  |
cmd5  |
cmd6  |
cmd7  |
}     |
      | bulk: cmd4, cmd5, cmd6, cmd7
```

Such blocks can be included in each other while nesting blocks are ignored.
```
input | output
------|-------
{     |
cmd1  |
cmd2  |
{     |
cmd3  |
cmd4  |
}     |
cmd5  |
cmd6  |
}     |
      | bulk: cmd1, cmd2, cmd3, cmd4, cmd5, cmd6
```

If the data is over within the block - the blocks are ignored entirely.
```
input | output
------|-------
cmd1  |
cmd2  |
cmd3  |
      | bulk: cmd1, cmd2, cmd3
{     |
cmd4  |
cmd5  |
cmd6  |
cmd7  |
```

Together with the output to the console, the blocks should be stored in separate files with the names `bulk1517223860.log`, where `1517223860` is the time of receipt of the first commands from the block.

Detailed description on the [gh-pages](https://dgolgovsky.github.io/bulk/)

**Dockerfile**
```
FROM ubuntu:trusty
#### Bintray (by JFrog) 
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 379CE192D401AB61
#### Dmitry Golgovsky (Packages sign) 
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D5CEB8D4D5185900
#### toolchain repo key
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1E9377A2BA9EF27F
RUN echo "deb http://dl.bintray.com/dgolgovsky/otus-cpp trusty main" | sudo tee -a /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list
RUN apt update
RUN apt install -y libstdc++6 bulk
```

**OTUS** C++ online [course](https://otus.ru/lessons/razrabotchik-c++/) studying repository.

**About the course**

Being one of the most popular programming languages, C++ is widely used for software development. The scope of usage includes the creation of operating systems, a variety of applications, device drivers, applications for embedded systems, high-performance servers, and entertainment applications (games).
In the course "C++ Developer" will be considered as introductory concepts, such as automation tools, STL, innovations of `11` and `14` standards; and more complex: asynchronous programming, design patterns, distributed high-availability services architectures.
