简介

本项目仓库是从 https://github.com/bitcoin/bitcoin fork而来，fork本仓库时原项目bitcoin的master分支处于Bitcoin Core的0.16.2发布版之后又提交了若干个commit的状态，master分支的具体commit号是0df9b0aed23127acd12d9ed6a008c12be47b1cd9。

本项目的dev分支是从master分支checkout出来的，开发新功能时都从dev分支checkout出新的topic branch进行开发，各个topic branch都合并到dev分支。
dev分支也会定期从 https://github.com/bitcoin/bitcoin 的master分支更新源码。

本项目的master分支不再单独从 https://github.com/bitcoin/bitcoin 的master分支更新源码，只会从dev分支合并更新代码，
master分支作为本项目的版本发布分支，始终与线上的版本是保持同步的。
